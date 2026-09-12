# Example Walkthrough: Full-Stack Software Project Discovery

This walkthrough demonstrates how an AI agent uses the **Agent Project Discovery Skill** when tasked with adding a feature to a complex, multi-tier software project.

---

## Scenario

- **Repository**: `acme-commerce-platform`
- **Tech Stack**: Next.js 14 App Router, Go (v1.22) backend microservices, PostgreSQL, Redis, Docker, GitHub Actions.
- **Task Prompt given by User**: *"Add rate limiting to our public inventory checking API endpoint."*

---

## Phase 1: Autonomous Discovery (Executed Silently by Agent)

Instead of immediately answering or editing code, the agent performs internal reconnaissance:

### 1. Repository Inspection
```bash
# 1. Structure discovery
ls -la
# Agent identifies:
# /apps/web (Next.js)
# /services/inventory (Go)
# /services/orders (Go)
# /packages/database (Prisma + Migrations)
# docker-compose.yml
# Makefile

# 2. Inspect documentation & architecture
cat README.md
cat docs/architecture.md
```

### 2. Git State Verification
```bash
git status
# Agent detects:
# On branch feature/inventory-v2
# Changes not staged for commit:
#   modified: services/inventory/handler.go (stray whitespace from developer)

git log -n 5 --oneline
# b4a8901 feat(inventory): add batch query endpoint
# f8912c0 fix(db): optimize connection pool settings
```

### 3. Dependency & Pattern Inspection
```bash
# Checking Go dependencies in /services/inventory
cat services/inventory/go.mod
# Finds: github.com/redis/go-redis/v9 v9.5.1 already imported!
# Finds: github.com/gin-gonic/gin v1.9.1

# Inspecting existing middleware pattern
cat services/inventory/middleware/auth.go
# Discovers Gin middleware convention and Redis client initialization pattern
```

### 4. Mental Model Synthesized
- **Project Purpose**: High-throughput e-commerce inventory lookup.
- **Architecture**: Distributed services; Inventory service is written in Go, handles Redis caching and Postgres persistence.
- **Rate Limiting Approach**: Redis token bucket or sliding window using already installed `go-redis/v9`, matching existing middleware patterns in `services/inventory/middleware/`.
- **Testing Strategy**: `go test ./services/inventory/...` using Dockerized test Redis instance.

---

## Phase 2: First Response Protocol

The agent issues its first reply strictly following the Response Protocol:

```markdown
## Understanding
I inspected the repository and identified `acme-commerce-platform` as a polyglot monorepo containing a Next.js frontend (`apps/web`) and Go backend services (`services/inventory`, `services/orders`). The inventory service uses Gin (`github.com/gin-gonic/gin`) and already maintains an active Redis client connection via `go-redis/v9` in `services/inventory/internal/cache`.

## Current State
- **Git Branch**: `feature/inventory-v2`
- **Working Tree**: `services/inventory/handler.go` has unstaged whitespace edits (will preserve without clobbering).
- **Endpoint**: `GET /api/v1/inventory/:sku` currently queries Redis cache with PostgreSQL fallback with zero rate limiting middleware attached.

## Plan
1. Implement a sliding-window Redis rate limiter middleware in `services/inventory/middleware/ratelimit.go` using existing `cache.Client`.
2. Configure sensible defaults (60 requests/minute per client IP) via `services/inventory/config.go` with environment variable override (`RATE_LIMIT_INVENTORY_RPM`).
3. Attach the rate limiter middleware to the `GET /api/v1/inventory/:sku` route group in `services/inventory/router.go`.
4. Add unit and integration tests in `services/inventory/middleware/ratelimit_test.go`.
5. Run `go test -v ./services/inventory/...` to verify backward compatibility.

## Blocking Questions
None. All required Redis dependencies, configuration patterns, and routing setups were identified directly in the repository.
```

---

## Phase 3: Minimal & Safe Implementation

The agent applies:
- Zero new external libraries (utilizes existing `go-redis/v9`).
- Matching Gin middleware signatures.
- Preserves the developer's existing unstaged whitespace edits in `handler.go`.
- Executes test suite: `go test -v ./services/inventory/middleware/...` -> `PASS`.

---

## Phase 4: Completion Report Protocol

Upon finishing the task, the agent delivers the final report:

```text
STATUS:
PASS

CHANGES:
- services/inventory/config.go: Added `RateLimitRPM` field with default of 60.
- services/inventory/middleware/ratelimit.go: Added IP-based Redis sliding-window rate limiter middleware.
- services/inventory/middleware/ratelimit_test.go: Added unit tests covering permitted, throttled (HTTP 429), and Redis error fallback scenarios.
- services/inventory/router.go: Applied rate limiting middleware to `/api/v1/inventory/:sku`.

VALIDATION:
- Executed `go test -v ./services/inventory/middleware/...`: 4 passed, 0 failed.
- Executed `go vet ./services/inventory/...`: Clean output, 0 warnings.
- Verified HTTP 429 payload adheres to company error envelope schema defined in `docs/api-specs.json`.

DEPLOYMENT:
- Working tree clean (aside from pre-existing uncommitted whitespace in `handler.go`).
- Ready for PR creation or developer review.

REMAINING:
- None. Rate limits can be dynamically adjusted in production via `RATE_LIMIT_INVENTORY_RPM` environment variable.
```
