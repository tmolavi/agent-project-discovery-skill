# Example Walkthrough: Machine Learning & Research Project Discovery

This walkthrough demonstrates how an AI agent uses the **Agent Project Discovery Skill** in a scientific research, deep learning, or data science repository.

---

## Scenario

- **Repository**: `neuro-protein-folding`
- **Tech Stack**: Python 3.11 (`pyproject.toml` managed with `uv`), PyTorch 2.4, Hugging Face `transformers`, Weights & Biases (W&B), DVC (Data Version Control), pytest.
- **Task Prompt given by User**: *"Add gradient checkpointing to the multi-head cross-attention layer to reduce VRAM during training on large sequence lengths."*

---

## Phase 1: Autonomous Discovery (Executed Silently by Agent)

The agent avoids immediately editing neural network definitions and systematically audits the repository environment:

### 1. Repository Layout & Artifact Inspection
```bash
# 1. Structure scan
ls -la
# Agent identifies:
# /configs (hydra yaml configs)
# /data (DVC tracked symlinks and .dvc pointer files)
# /models (PyTorch neural network architectures)
# /experiments (MLflow/W&B logging utilities)
# pyproject.toml
# uv.lock

# 2. Inspect README and experimental documentation
cat README.md
cat docs/experiments.md
```

### 2. Git & DVC State Verification
```bash
git status
# Branch: experiment/attn-optimization
# Untracked files:
#   runs/pretrain_run_42/checkpoints/best.pt (Active local training checkpoint!)

# Check commit history
git log -n 5 --oneline
# 3c91d8a chore(config): increase sequence length to 4096
# e902b11 feat(models): integrate FlashAttention-2
```

### 3. Environment & Hardware Awareness
```bash
# Check pyproject.toml and existing dependencies
grep -E "torch|transformers|hydra" pyproject.toml
# Discovers:
# torch >= 2.4.0
# hydra-core == 1.3.2

# Check how models are instantiated
cat configs/model/transformer.yaml
# Finds gradient_checkpointing flag already exists in config schema, but defaulted to false!
```

### 4. Mental Model Synthesized
- **Project Purpose**: Protein sequence structure prediction under long context lengths ($L \ge 4096$).
- **Architecture**: Custom PyTorch Transformer with FlashAttention-2 kernel integration.
- **VRAM Constraints**: Backprop activations explode at $L=4096$; gradient checkpointing allows trade-off of $\approx 25\%$ compute overhead for $\approx 60\%$ activation memory reduction.
- **Critical Invariant**: Model forward pass tensor output and checkpoint serialization schema must remain strictly identical. Do not overwrite or modify `runs/pretrain_run_42/` checkpoints.

---

## Phase 2: First Response Protocol

The agent generates its first response adhering to the Discovery Response Protocol:

```markdown
## Understanding
`neuro-protein-folding` is a PyTorch-based sequence modeling codebase using Hydra for configuration management and DVC for data tracking. The model core lives in `models/transformer.py`, where multi-head cross-attention is computed for sequence lengths up to 4096 tokens. The repository already uses `torch.utils.checkpoint.checkpoint` in feedforward blocks, but cross-attention currently stores full activation tensors during the forward pass.

## Current State
- **Git Branch**: `experiment/attn-optimization`
- **Working Tree**: Clean git state; local directory contains active training run weights at `runs/pretrain_run_42/checkpoints/` which will remain strictly untouched.
- **Config**: `configs/model/transformer.yaml` already has a placeholder `gradient_checkpointing: false` attribute.

## Plan
1. Update `models/transformer.py` in `CrossAttentionBlock.forward()` to support conditional checkpointing via `torch.utils.checkpoint.checkpoint(..., use_reentrant=False)` when `self.gradient_checkpointing` is enabled.
2. Ensure `use_reentrant=False` is used to maintain compatibility with PyTorch 2.4 autograd and mixed-precision tensors.
3. Write a unit test in `tests/test_checkpointing.py` verifying:
   - Output tensors with and without gradient checkpointing are numerically identical within tolerance (`torch.allclose(atol=1e-6)`).
   - Peak GPU/CPU memory allocation decreases when checkpointing is enabled on dummy tensors of shape `(2, 4096, 512)`.
4. Run `pytest tests/test_checkpointing.py` and existing test suite `pytest tests/test_models.py`.

## Blocking Questions
None. Architecture, configuration structure, and PyTorch versions were resolved from repository inspection.
```

---

## Phase 3: Minimal & Safe Implementation

The agent:
- Modifies `models/transformer.py` using non-reentrant checkpointing (modern PyTorch standard).
- Adds unit tests checking exact output equivalence.
- Runs verification tests using `uv run pytest`.

---

## Phase 4: Completion Report Protocol

```text
STATUS:
PASS

CHANGES:
- models/transformer.py: Enabled `torch.utils.checkpoint.checkpoint(self._cross_attention_inner, ..., use_reentrant=False)` inside `CrossAttentionBlock.forward()` guarded by `self.gradient_checkpointing`.
- configs/model/transformer.yaml: Documented `gradient_checkpointing: true` option.
- tests/test_checkpointing.py: Added unit tests for numerical parity (`atol=1e-6`) and memory footprint verification.

VALIDATION:
- Executed `uv run pytest tests/test_checkpointing.py`: 2 passed in 1.12s.
- Executed `uv run pytest tests/test_models.py`: 18 passed in 4.85s.
- Verified zero degradation on existing model checkpoints or tensor serialization formats.

DEPLOYMENT:
- Untracked files and active checkpoints in `runs/` preserved untouched.
- Branch `experiment/attn-optimization` clean and ready for commit.

REMAINING:
- Optional: Can benchmark activation reduction against full distributed FSDP run in staging cluster.
```
