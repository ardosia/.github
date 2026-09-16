# Current Public Metadata State

Last updated: 2026-09-16
Current milestone: stable public metadata after centralized documentation migration
Current branch: `main`

## Working
- `.agent/` workflow harness is installed.
- Public organization profile contains only stable project/target/repository-boundary information rather than detailed implementation status.
- Public reusable transport repositories remain separate from private application/protocol/evidence layers.
- `ardosia/ardosia-docs` exists and is private; detailed central engineering documentation therefore is intentionally not linked from the public organization profile.

## Partially working
None for the current metadata scope.

## Broken / failing
- No runtime behavior exists in this metadata repository.

## Validation status
- Runtime/build/tests: **NOT APPLICABLE** for this metadata-only repository.
- Public profile content review: **PASS** by direct inspection; no profile content change was needed in the final centralization round.

## Current blocker
None.

## Active work
- Keep the public profile synchronized only when stable public repository roles or fixed target facts change.
- Do not mirror private implementation status or private central documentation into the public profile.
