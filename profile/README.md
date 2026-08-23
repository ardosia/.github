# Ardosia

Ardosia is a Rust-first server-engineering project targeting the historical **Minecraft: Pocket Edition 0.15.10 alpha** stack.

Current compatibility target:

- Minecraft: Pocket Edition `0.15.10`
- game protocol `84`
- RakNet protocol `8`

## Repositories

### `ardosia-raknet`

Ardosia-maintained RakNet transport hardfork for asynchronous UDP networking in Rust.

### `ardosia-network`

Stable Ardosia-facing networking facade and RakNet transport integration.

Historical load-testing evidence is preserved in the repository, but the former in-repository load generator and benchmark harness have been intentionally removed.

### `ardosia-protocol`

Minecraft: Pocket Edition 0.15.10 protocol 84 codecs, packet definitions, login/session state, and version-specific wire behavior. This is the next active Rust-first implementation milestone.

### `ardosia`

Legacy Java implementation retained temporarily as historical and behavioral reference material. New architecture is Rust-first and should not depend on the legacy repository.

## Architecture

```text
server / game
    |
    v
ardosia-protocol
    |
    v
ardosia-network
    |
    v
ardosia-raknet
```

Transport and game-protocol responsibilities are intentionally kept separate so each layer can be tested and evolved independently.

The active Rust repositories target a pinned modern toolchain baseline rather than a moving `stable` compiler. Compatibility claims apply only to the historical Minecraft target above and do not imply support for current Minecraft Bedrock releases.

The project is pre-release.

Ardosia is an independent project and is not affiliated with Mojang Studios or Microsoft.
