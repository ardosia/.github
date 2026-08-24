# Ardosia

Ardosia is a Rust-first server-engineering project targeting the historical **Minecraft: Pocket Edition 0.15.10 alpha** stack.

Current compatibility target:

- Minecraft: Pocket Edition `0.15.10`
- game protocol `84`
- RakNet protocol `8`

## Repositories

### `ardosia-raknet`

Ardosia-maintained standalone RakNet transport hardfork for asynchronous UDP networking in Rust.

### `ardosia-network`

Stable Ardosia-facing networking facade and RakNet transport integration.

Historical load-testing evidence is preserved in the repository, but the former in-repository load generator and benchmark harness were intentionally removed.

### `ardosia-protocol`

Minecraft: Pocket Edition 0.15.10 protocol-84 codecs and compatibility layer. The first Rust protocol kernel/login milestone is implemented, including bounded primitive/framing support, structural Login decoding, PlayStatus, Disconnect, Batch, malformed-input hardening, and preserved protocol-84 wire evidence.

Login/JWS data remains explicitly unverified; structural parsing is not authentication.

### `ardosia-server`

Reserved Rust server/game/session layer. The repository exists but remains intentionally empty until its first bounded architecture is approved. It is expected to own game/session orchestration above the independently testable protocol and network layers.

### `ardosia`

Legacy Java implementation retained as historical and behavioral reference material. New architecture is Rust-first and does not depend on the legacy repository.

## Architecture

Conceptually:

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

The diagram is a logical stack, not a requirement that every crate directly depends on the next one. `ardosia-protocol` is currently synchronous and transport-independent with no Tokio, `ardosia-network`, or direct `ardosia-raknet` dependency. The future server/session integration may depend on both protocol and network while keeping RakNet internals below the networking facade.

Transport, game-protocol, and game/server responsibilities are intentionally kept separate so each layer can be tested and evolved independently.

The active Rust repositories use pinned modern toolchains rather than a moving `stable` compiler. Compatibility claims apply only to the historical Minecraft target above and do not imply support for current Minecraft Bedrock releases.

The project is pre-release.

Ardosia is an independent project and is not affiliated with Mojang Studios or Microsoft.
