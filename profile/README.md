# Ardosia

Ardosia is a Rust-first server-engineering project targeting the historical **Minecraft: Pocket Edition / Windows 10 Edition Beta 0.15.10** stack.

Current compatibility target:

- Minecraft: Pocket Edition / Windows 10 Edition Beta `0.15.10`
- game protocol `84`
- RakNet protocol `8`
- Rust `1.98`

## Status model

Ardosia separates **merged baseline**, **active private development**, and **historical evidence**. Repository default branches describe merged state; private feature/integration branches may be substantially ahead and are not presented as released milestones until accepted.

The merged private server `main` line has completed session/bootstrap plus B0 identifiers/registries, B1 semantic world modeling, and B2 chunk source/generation contracts. Active private development has moved beyond initial chunk streaming into gameplay/world-simulation compatibility work, including persistence/lifecycle, inventory and block interaction slices, entity/world integration, time/weather/random-tick accounting, and native stored-light parity. Those details remain development-branch state until merged.

A real 0.15.10 client has been used as an acceptance oracle for compatibility-sensitive milestones. Compatibility claims are kept narrower than implementation progress: branch code, reverse-engineering evidence, and an actual client smoke test are treated as separate proof layers.

## Repository map

### Public open-source components

#### [`ardosia-raknet`](https://github.com/ardosia/ardosia-raknet)

Reusable Apache-2.0 hardfork of `mcbe-rs/raknet-rust`. It owns generic UDP/RakNet mechanics such as handshakes, reliability, ordering, retransmission, fragmentation/reassembly, congestion/pacing, sharded runtime behavior, transport abuse controls, and low-level telemetry. It intentionally does **not** own Minecraft packets, gameplay state, world state, or Ardosia application behavior.

The hardfork is pre-release and Git-only. Ardosia consumers pin an exact verified revision rather than following a moving branch.

#### [`ardosia-network`](https://github.com/ardosia/ardosia-network)

Public Apache-2.0 game-agnostic facade between application code and RakNet. It owns validated transport configuration, listener/connection lifecycle, opaque connected-payload delivery, bounded queues/backpressure, and graceful shutdown while keeping RakNet implementation types behind a small public surface.

The crate remains pre-release and `publish = false`.

### Private development and evidence repositories

- **`ardosia-protocol`** — synchronous, transport-independent MCPE 0.15.10 / protocol-84 semantics, codecs, fixtures, and protocol evidence.
- **`ardosia-server`** — application lifecycle, player/session orchestration, gameplay/world composition, persistence, simulation, semantic-to-wire projection, and chunk streaming.
- **`ardosia-mcpe-dump`** — server-relevant reverse-engineering evidence extracted from the frozen 0.15.10 x86 target; findings distinguish confirmed binary/asset evidence from unresolved semantics.
- **`ardosia`** — frozen Java implementation retained as a historical compatibility/reference oracle, not the architecture template for the Rust rewrite.

The private repositories have independent licensing/governance decisions. Apache-2.0 on the public RakNet and Network repositories does not implicitly license the private layers.

## Architecture

```text
ardosia-server                 private application/game/world layer
   |-- ardosia-protocol        private protocol-84 semantics/wire
   `-- ardosia-network         public, Apache-2.0 transport facade
          `-- ardosia-raknet   public, Apache-2.0 RakNet hardfork

ardosia-mcpe-dump              private native compatibility evidence
ardosia                        private frozen Java reference
```

The boundaries are intentional:

- `ardosia-raknet` stays generic transport infrastructure.
- `ardosia-network` stays a game-agnostic transport facade.
- `ardosia-protocol` owns protocol-84 semantics and wire compatibility while remaining synchronous and transport-independent.
- `ardosia-server` owns player lifecycle, application policy, gameplay/world behavior, persistence/simulation, and semantic-to-wire orchestration.
- evidence repositories preserve target behavior without becoming runtime dependencies by default.

## Development discipline

The target is single-version by design. New work should preserve exact historical behavior where evidence exists and remain conservative where it does not. Native evidence, stored-wire fixtures, legacy Java behavior, and later Bedrock documentation are not treated as interchangeable proof sources.

Merged status should be read from repository default branches. Active work should be read from the branch actually pinned/consumed by its parent repository, and old dated plans should not be used as current roadmap state.

Compatibility claims apply only to the historical target above and do not imply support for current Bedrock releases. The project is pre-release.

Ardosia is an independent project and is not affiliated with Mojang Studios or Microsoft.
