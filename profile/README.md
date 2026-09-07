# Ardosia

Ardosia is a Rust-first server-engineering project targeting the historical **Minecraft: Pocket Edition / Windows 10 Edition Beta 0.15.10** stack.

Current compatibility target:

- Minecraft: Pocket Edition `0.15.10`
- game protocol `84`
- RakNet protocol `8`
- Rust `1.98`

## Current status

The merged private server mainline has completed the session/bootstrap path plus B0 identifiers/registries, B1 semantic world modeling, and B2 chunk source/generation contracts.

A real 0.15.10 client has been verified through the pre-chunk `ReadyForChunks` boundary on the merged line. Post-B2 integration work now covers protocol-84 chunk projection, initial player chunk streaming, chunk-interest lifecycle hardening, and first-spawn/client-wire alignment. Those post-B2 changes remain development work until they are accepted into the private mainlines; this public profile does not treat an unmerged branch as a released milestone.

## Public open-source components

### [`ardosia-raknet`](https://github.com/ardosia/ardosia-raknet)

Ardosia's reusable Apache-2.0 hardfork of `mcbe-rs/raknet-rust`.

It owns generic UDP/RakNet mechanics such as handshakes, reliability, ordering, retransmission, fragmentation/reassembly, congestion/pacing, sharded runtime behavior, transport abuse controls, and low-level telemetry. It intentionally does **not** own Minecraft packets, gameplay state, world state, or Ardosia application behavior.

The hardfork is pre-release and Git-only for now. See its repository for exact-SHA usage, upstream provenance, contribution guidance, and security reporting.

### [`ardosia-network`](https://github.com/ardosia/ardosia-network)

`ardosia-network` is the public Apache-2.0 game-agnostic facade between application code and the RakNet implementation.

It owns validated transport configuration, listener and connection lifecycle, opaque connected-payload delivery, bounded queues/backpressure, and graceful shutdown while keeping RakNet implementation types behind a small stable surface. Minecraft packet definitions, protocol sequencing, player state, gameplay, and world behavior deliberately remain outside this repository.

The crate is pre-release and remains `publish = false`; public source visibility does not imply a crates.io release. Its RakNet dependency is pinned to an exact revision of the public `ardosia-raknet` hardfork for reproducible integration.

## Private development stack

The product-specific layers remain under private development:

- **`ardosia-protocol`** — transport-independent MCPE 0.15.10 / protocol-84 semantics, wire compatibility, and protocol evidence;
- **`ardosia-server`** — application lifecycle, player-session orchestration, game/world composition, projection/streaming integration, and server policy.

Their repository visibility and licensing remain separate deliberate decisions. The Apache-2.0 licenses selected for the public RakNet and Network repositories do not automatically determine the licenses of the private Protocol or Server repositories.

## Architecture

```text
ardosia-server                 private
   |-- ardosia-protocol        private
   `-- ardosia-network         public, Apache-2.0
          `-- ardosia-raknet   public, Apache-2.0
```

The layers are intentionally separated:

- `ardosia-raknet` stays generic transport infrastructure.
- `ardosia-network` stays a game-agnostic transport facade.
- `ardosia-protocol` owns protocol-84 semantics and wire compatibility while remaining synchronous and transport-independent.
- `ardosia-server` owns player lifecycle, application policy, world/game composition, and semantic-to-wire projection orchestration.

## Roadmap

Merged private server status:

```text
A   Session bootstrap                     COMPLETE
B0  Game identifiers + registries         COMPLETE
B1  Semantic world domain                 COMPLETE
B2  Chunk source + generation contracts   COMPLETE
```

Post-B2 development is integrating B5 protocol-84 chunk projection and B6 player chunk streaming, followed by lifecycle/client-wire hardening. Persistent storage and broader gameplay remain separate later work rather than being folded into the transport/protocol layers.

Compatibility claims apply only to the historical Minecraft target above and do not imply support for current Bedrock releases. The project is pre-release.

Ardosia is an independent project and is not affiliated with Mojang Studios or Microsoft.
