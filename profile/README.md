# Ardosia

Ardosia is a Rust-first server-engineering project targeting the historical **Minecraft: Pocket Edition 0.15.10 alpha** stack.

Current compatibility target:

- Minecraft: Pocket Edition `0.15.10`
- game protocol `84`
- RakNet protocol `8`
- Rust `1.98`

## Current status

The Rust stack has completed its first real-client milestone through the pre-chunk session boundary. A real MCPE 0.15.10 client can discover the server, establish a RakNet 8 connection, complete protocol-84 Login/bootstrap, negotiate chunk radius, and reach `ReadyForChunks(8)`.

**B0 identifiers and the frozen built-in block registry are complete. B1 world-domain modeling is the next active product mission.** World/chunk serialization and initial chunk streaming are not implemented yet, so the real client currently remains on the terrain-loading screen after the pre-chunk path.

## Public open-source component

### [`ardosia-raknet`](https://github.com/ardosia/ardosia-raknet)

Ardosia's first public reusable component is an Apache-2.0 hardfork of `mcbe-rs/raknet-rust`.

It owns generic UDP/RakNet mechanics such as handshakes, reliability, ordering, retransmission, fragmentation/reassembly, congestion/pacing, sharded runtime behavior, transport abuse controls, and low-level telemetry. It intentionally does **not** own Minecraft packets, gameplay state, world state, or Ardosia application behavior.

The hardfork is pre-release and Git-only for now. See its repository for exact-SHA usage, upstream provenance, contribution guidance, and security reporting.

## Private development stack

The rest of the active Rust stack remains under private development for now:

- **`ardosia-server`** — application lifecycle, player-session orchestration, game/world composition, and server policy;
- **`ardosia-protocol`** — transport-independent MCPE 0.15.10 / protocol-84 semantics, wire compatibility, and protocol evidence;
- **`ardosia-network`** — small game-agnostic facade between the application and RakNet transport.

Their repository visibility and licensing are separate decisions from the public RakNet hardfork. This organization profile does not imply that those private repositories are currently distributed as open source.

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
- `ardosia-server` owns player lifecycle, application policy, and world/game composition.

The current roadmap continues from B1 world-domain boundaries through chunk sourcing/generation, storage, resident snapshots/cache, protocol-84 chunk projection, and initial chunk streaming.

Compatibility claims apply only to the historical Minecraft target above and do not imply support for current Bedrock releases. The project is pre-release.

Ardosia is an independent project and is not affiliated with Mojang Studios or Microsoft.