# Public Metadata Decisions

## D-0001 — Keep the public organization profile stable and concise
Status: Accepted
Date: 2026-09-16

### Context
Detailed implementation status changes faster than organization metadata and has become stale before.

### Decision
Use `profile/README.md` for a stable public project overview and public repository boundary, not as the authoritative engineering continuation ledger.

### Consequences
Operational state lives in `.agent`; durable detailed documentation belongs in `ardosia-docs` once available.

## D-0002 — Preserve public/private repository boundary descriptions
Status: Accepted
Date: 2026-09-16

### Decision
Public metadata may describe the roles of private layers at a high level but must not expose private operational details merely to mirror the internal harness.

## D-0003 — Centralize durable documentation
Status: Accepted
Date: 2026-09-16

### Decision
Use `ardosia/ardosia-docs` for durable cross-repository documentation; keep this repo's profile README only as an operational GitHub UI surface.

## D-0004 — PROJECT_WORKFLOW.md governs substantial work
Status: Accepted
Date: 2026-09-16

### Decision
Use the Project-provided inline single-agent durable-state workflow and exact validation reporting.
