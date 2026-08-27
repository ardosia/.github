# Ardosia

Ardosia is a Rust-first server-engineering project targeting the historical **Minecraft: Pocket Edition 0.15.10 alpha** stack.

Current compatibility target:

- Minecraft: Pocket Edition `0.15.10`
- game protocol `84`
- RakNet protocol `8`
- Rust `1.98`

## Current status

The first real-client Rust milestone is complete through the pre-chunk session boundary. A real MCPE 0.15.10 client can discover the server, establish a RakNet 8 connection, complete protocol-84 Login/bootstrap, negotiate chunk radius, and reach `ReadyForChunks(8)`.

The client currently remains on the terrain-loading screen because world/chunk serialization and initial chunk streaming have not been implemented yet. **B0 game identifiers and registries is the next active product mission.**

## Repositories

### `ardosia-server`

Active Rust server/application layer. Owns application lifecycle, player-session orchestration, admission and chunk-radius policy, and the composition boundary for upcoming world/chunk systems.

### `ardosia-protocol`

Transport-independent MCPE 0.15.10 / protocol-84 semantic and wire compatibility layer. Exposes semantic ingress/session operations while keeping codec machinery private, and preserves protocol-84 wire evidence.

Login/JWS claims are structurally parsed but remain explicitly **unverified**; parsing is not authentication.

### `ardosia-network`

Small game-agnostic networking facade over the RakNet implementation. Owns validated transport configuration, listener/connection lifecycle, opaque connected-payload send/receive operations, backpressure outcomes, and graceful shutdown without interpreting MCPE packets.

### `ardosia-raknet`

Standalone Ardosia-maintained hardfork of `mcbe-rs/raknet-rust`. Owns UDP/RakNet mechanics such as handshakes, reliability, ordering, retransmission, fragmentation, congestion/pacing, sharding, abuse controls, and low-level transport behavior.

### `ardosia`

Frozen legacy Java implementation retained as historical, behavioral, protocol, and storage reference material for the Rust-first rewrite. New architecture does not depend on the Java object model.

## Architecture

```text
ardosia-server
   |-- ardosia-protocol
   `-- ardosia-network
          `-- ardosia-raknet
```

The layers are intentionally separated:

- RakNet stays generic transport infrastructure.
- `ardosia-network` stays a game-agnostic transport facade.
- `ardosia-protocol` owns protocol-84 semantics and wire compatibility while remaining synchronous and transport-independent.
- `ardosia-server` owns player lifecycle, application policy, and future world/game composition.

The next roadmap sequence begins with B0 identifiers/registries, followed by world/chunk domain boundaries, deterministic chunk sourcing/storage, protocol-84 chunk projection, and initial chunk streaming.

Compatibility claims apply only to the historical Minecraft target above and do not imply support for current Bedrock releases. The project is pre-release.

Ardosia is an independent project and is not affiliated with Mojang Studios or Microsoft.
