# Current Public Metadata State

Last updated: 2026-09-16
Current milestone: workflow/documentation migration
Current branch: `main`
Current head before harness migration: `99baf5fa4057992c1740d07d37d47cbd7993a8b7`

## Working
- Public organization profile describes the fixed historical compatibility target and public transport repositories.
- Public reusable transport repositories remain separate from private application/protocol/evidence layers.

## Partially working
- The current public profile contains detailed status prose that can become stale as private implementation branches/main evolve.
- It should be reduced to a stable overview/pointer as central documentation is established.

## Broken / failing
- No runtime behavior exists in this metadata repository.

## Validation status
- Runtime/build/tests: **NOT APPLICABLE** for this metadata-only repository.
- Profile/content review in this migration round: **PASS** by direct file inspection.

## Current blocker
- Central documentation migration is **BLOCKED** until `ardosia/ardosia-docs` exists. The current connector cannot create repositories.

## Active work
- Install `.agent/` harness.
- Replace stale public project-status detail with a concise stable profile.
- Link to central docs once the destination repository exists and its visibility/link policy is decided.
