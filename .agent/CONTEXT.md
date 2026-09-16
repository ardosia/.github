# Public Organization Context

## Purpose
This repository owns Ardosia's public GitHub organization profile/metadata. It is not a runtime implementation repository.

## Public project target
Ardosia is a Rust-first compatibility project targeting Minecraft: Pocket Edition / Windows 10 Edition Beta 0.15.10, game protocol 84, and RakNet 8.

Public reusable components include:
- `ardosia-network` — Apache-2.0 game-agnostic transport facade.
- `ardosia-raknet` — Apache-2.0 generic RakNet hardfork.

Private repositories contain the application/server, game-protocol semantics, native evidence, and frozen Java reference.

## Workflow
Substantial project work follows the Project-provided `PROJECT_WORKFLOW.md`. Repository-local operational state uses `.agent/{CONTEXT,STATE,DECISIONS,NEXT}.md`.

## Documentation policy
Durable cross-repository documentation is being centralized in `ardosia/ardosia-docs`. The GitHub `profile/README.md` is an operational public profile surface and may remain as a concise stable pointer/overview rather than a detailed project-status ledger.
