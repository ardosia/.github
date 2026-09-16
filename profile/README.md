# Ardosia

Ardosia is a Rust-first server-engineering project targeting the historical **Minecraft: Pocket Edition / Windows 10 Edition Beta 0.15.10** stack.

Fixed compatibility target:

- Minecraft: Pocket Edition / Windows 10 Edition Beta `0.15.10`
- game protocol `84`
- RakNet protocol `8`
- Rust `1.98` for the active Rust stack

## Public components

- [`ardosia-raknet`](https://github.com/ardosia/ardosia-raknet) — Apache-2.0 standalone RakNet hardfork. It owns generic UDP/RakNet transport behavior and intentionally contains no Minecraft gameplay semantics.
- [`ardosia-network`](https://github.com/ardosia/ardosia-network) — Apache-2.0 game-agnostic listener/connection/payload facade over the pinned RakNet hardfork.

Private repositories contain the application/server, protocol-84 semantics, frozen native evidence, and frozen Java compatibility reference.

The project is single-version and evidence-driven: direct evidence for the frozen target, wire fixtures, reference implementations, and real-client acceptance are kept distinct rather than treated as interchangeable proof.

Detailed engineering state is intentionally not maintained in this public profile. Ardosia is an independent project and is not affiliated with Mojang Studios or Microsoft.
