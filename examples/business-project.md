# Example Walkthrough: Business Automation & Operations Project Discovery

This walkthrough demonstrates how an AI agent uses the **Agent Project Discovery Skill** in an enterprise business systems, fintech, or workflow automation repository.

---

## Scenario

- **Repository**: `fintech-billing-hub`
- **Tech Stack**: TypeScript, Node.js 20, Fastify, Stripe API SDK, Prisma ORM, PostgreSQL, Temporal / BullMQ workflows, Vitest.
- **Task Prompt given by User**: *"Add support for handling the `invoice.payment_failed` Stripe webhook event and trigger customer retry email notification."*

---

## Phase 1: Autonomous Discovery (Executed Silently by Agent)

A careless agent might immediately start creating raw HTTP endpoints or asking the user for secret API keys. Under the Discovery Skill, the agent conducts a structured investigation:

### 1. Repository Layout & Business Flow Inspection
```bash
# 1. Structure scan
ls -la
# Discovers:
# /src/api/webhooks/
# /src/services/billing/
# /src/services/notifications/
# /src/jobs/
# /prisma/schema.prisma
# package.json
# .env.example

# 2. Inspect existing webhook architectures
cat src/api/webhooks/stripe.ts
# Discovers:
# - Stripe webhook signature verification with STRIPE_WEBHOOK_SECRET is already implemented
# - Idempotency table `WebhookEvent` in Prisma prevents duplicate processing
# - Handlers for `invoice.paid` and `customer.subscription.deleted` already exist
```

### 2. Git State & Working Tree Audit
```bash
git status
# Branch: main
# Untracked:
#   .env (Local secrets file - MUST NOT BE MODIFIED OR LOGGED)
# Working tree clean.

git log -n 5 --oneline
# 8f192b0 feat(stripe): support multi-currency invoices (EUR, USD)
# d43e110 fix(notifications): add sendgrid backoff retry handler
```

### 3. Notification Service & Worker Patterns
```bash
# How are emails triggered in this project?
cat src/services/notifications/email.ts
# Discovers:
# EmailService.sendBillingAlert({ recipientId, templateId, metadata })
# Uses BullMQ queue: `notification-queue`

# How is customer contact information retrieved?
cat src/services/billing/customer.ts
# Discovers helper: `BillingCustomerService.getByStripeCustomerId(stripeCustomerId)`
```

### 4. Mental Model Synthesized
- **Project Purpose**: Centralized billing, subscription sync, and revenue automation.
- **Critical Business Rule**: Invariant idempotency. Financial webhook payloads must never be processed more than once.
- **Security Invariant**: Never expose customer PII in application log output. Never commit `.env`.
- **Testing Approach**: Local tests use Stripe fixture JSON files (`tests/fixtures/stripe/`) and mocked Prisma clients with Vitest.

---

## Phase 2: First Response Protocol

```markdown
## Understanding
`fintech-billing-hub` handles asynchronous payment processing and billing lifecycle events. The webhook ingest layer in `src/api/webhooks/stripe.ts` verifies Stripe HMAC signatures and records event IDs in the `WebhookEvent` table for strict idempotency before delegating to domain services. Email notifications are dispatched asynchronously via BullMQ using `EmailService.sendBillingAlert` in `src/services/notifications/email.ts`.

## Current State
- **Git Branch**: `main`
- **Working Tree**: Clean. Local `.env` is properly ignored in `.gitignore`.
- **Webhook Handlers**: `src/api/webhooks/stripe.ts` currently handles `invoice.paid` and `customer.subscription.deleted`, but lacks a case for `invoice.payment_failed`.

## Plan
1. Add a test fixture `tests/fixtures/stripe/invoice_payment_failed.json` representing a realistic failed subscription invoice event.
2. In `src/services/billing/invoice.ts`, implement `handlePaymentFailed(invoice: Stripe.Invoice)`:
   - Mark internal invoice record as `PAYMENT_FAILED`.
   - Look up customer account details via `BillingCustomerService.getByStripeCustomerId`.
   - Dispatch `PAYMENT_FAILED_RETRY` notification through `EmailService.sendBillingAlert`.
3. Wire the handler into the switch statement in `src/api/webhooks/stripe.ts`.
4. Ensure the operation is wrapped within the existing idempotency transaction.
5. Write unit tests in `tests/webhooks/stripe.test.ts` to verify signature validation, idempotent deduplication, and notification dispatch.
6. Run `pnpm test` and `pnpm typecheck`.

## Blocking Questions
None. The existing webhook signature verification, Prisma schema, and BullMQ notification services provide all necessary integration points.
```

---

## Phase 3: Minimal & Safe Implementation

The agent:
- Reuses existing `WebhookEvent` idempotency checks.
- Adheres to the established error-handling patterns and logger interface (no PII leakage).
- Writes deterministic unit tests with mocked Stripe event data.
- Runs `pnpm test` -> `All 14 tests passing`.

---

## Phase 4: Completion Report Protocol

```text
STATUS:
PASS

CHANGES:
- src/services/billing/invoice.ts: Added `handlePaymentFailed()` method updating status and enqueuing alert email.
- src/api/webhooks/stripe.ts: Added `case "invoice.payment_failed"` routing to the new billing handler within the transactional idempotency envelope.
- tests/fixtures/stripe/invoice_payment_failed.json: Added standard Stripe failure event mock.
- tests/webhooks/stripe.test.ts: Added test coverage for successful failure handling, idempotency deduplication, and customer lookup errors.

VALIDATION:
- Executed `pnpm typecheck`: 0 TypeScript errors.
- Executed `pnpm test tests/webhooks/stripe.test.ts`: Passed (5 tests passed).
- Executed `pnpm test`: Full test suite passed (14/14 tests).

DEPLOYMENT:
- All new handlers respect existing environment configurations. No database schema migrations required.
- Working tree clean and ready for commit on a feature branch.

REMAINING:
- None. System is ready to receive live webhook retries once merged.
```
