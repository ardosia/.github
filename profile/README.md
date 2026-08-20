# Ardosia

Ardosia is an experimental, Rust-first server stack targeting the historical **Minecraft: Pocket Edition 0.15.10** protocol.

The project is being rebuilt as small, independently testable components with clear boundaries between transport, game protocol, and server behavior.

```text
        Ardosia
           |
     game / server
           |
  ardosia-protocol
   MCPE protocol 84
           |
   ardosia-network
      UDP + RakNet
```

## What we care about

Ardosia is being developed around a few non-negotiable engineering goals:

- protocol correctness before compatibility shortcuts;
- performance measured with repeatable benchmarks;
- security and bounded resource behavior from the transport layer upward;
- explicit architectural boundaries between RakNet and the MCPE game protocol;
- data-driven optimization instead of speculative rewrites.

## Current status

Development is **pre-release** and currently private.

The active rewrite targets:

- Minecraft: Pocket Edition `0.15.10`;
- game protocol `84`;
- RakNet protocol `8`;
- a Rust-first networking and protocol stack.

No compatibility with current Minecraft Bedrock releases is implied.

## Historical scope

Ardosia intentionally targets an old Pocket Edition protocol for research, preservation, experimentation, and server-engineering work.

Ardosia is an independent project and is **not affiliated with Mojang Studios or Microsoft**.
