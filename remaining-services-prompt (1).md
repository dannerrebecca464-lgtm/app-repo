Follow the procedure rules already in place for this project (updated Rule 3 — build all remaining services in this pass, no stopping between each).

Build the remaining services now — confirm first which of these are already built vs. not; build only what's genuinely missing:
1. **API Gateway** — single entry point, routes to IAM (built) and stubs/placeholders clearly marked as not-yet-implemented for Wallet/Ledger and Notification, calls IAM's `POST /validate` for auth (does not reimplement JWT verification locally), basic in-memory rate limiting, `GET /health` (liveness only).
2. **Wallet/Ledger** — `check_balance` and `transfer_funds` endpoints, double-entry bookkeeping (append-only ledger pattern), holds KYC/verification status, publishes a transfer event to the message broker on successful transfer.
3. **Notification** — consumes transfer events off the message broker, sends mock email/SMS (log output is fine, no real delivery), no DB required.

**Language: Python for all three, matching IAM's stack** (FastAPI/SQLAlchemy/Alembic where relevant, pytest for tests, same config-via-env and health-check patterns) — per the updated Rule 3, no mixing languages between services.

Reminders:
- No Dockerfile or `.dockerignore` for either service — note what I'll need for each at the end instead.
- Keep both trivially simple per the golden rule — no saga/rollback logic, no fraud/risk checks, no real email/SMS integration.
- Wallet/Ledger connects to Postgres and the message broker the same way IAM/Gateway would (via env vars from config, per the 12-Factor pattern already established) — assume Postgres and RabbitMQ (or Redis) will be deployed via Helm, so the app just needs connection strings from env.
- Include `tests/` for pure logic in each service (e.g., balance calculation, ledger entry creation) same as the earlier services.
- Ask me now if anything is ambiguous (e.g., exact ledger entry schema, what "KYC status" needs to look like) rather than guessing.

When all are done, give me **one total summary covering API Gateway, Wallet/Ledger, and Notification together**, organized per service (not per file), per the updated Rule 4 format: what it does, key endpoints, deliberate simplifications/tradeoffs, and Dockerfile requirements.
