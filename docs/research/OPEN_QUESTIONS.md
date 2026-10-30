# Open questions and next experiments

**Reviewed 2026-10-30.** [Status](STATUS.md) · [119–130 evidence](DIAGNOSTICS_119_130.md) · [Lobby](../networking/BUILD_TOGETHER_LOBBY.md)

## Immediate: direct internet play on two PCs

The owner chose no VPN application and requires both IPv4 and IPv6. [Detailed proposed transport and acceptance gates](../networking/INTERNET_PLAN.md).

- Implement and test Python-to-Python TCP/TLS with verified host identity and private one-guest admission. Remote PIDs are not identities; keep native process/image checks local.
- Define versioned invitations carrying endpoint/port, server/room identity and a one-time secret; extend the present short-field limit. No lookup/rendezvous service currently exists.
- Keep local DLL polling independent of WAN RTT. Separate local pipe sessions, remote room binding and application outcomes, including embedded sessions in fragmented payloads.
- Bound connection attempts, queues, frame/reassembly sizes and timeout behavior. Preserve commands/order/leases under uncertainty; do not blindly replay ambiguous effects.
- Test reachable IPv4 and IPv6 routes independently. Router port-forwarding support does not guarantee provider-side reachability; a future optional relay can cover some otherwise inaccessible peers.
- Package required original code portably; current companion imports archived diagnostic bases and developer-specific launch paths. A second PC needs its own game and matching supported native profile, not a copied game distribution.

No WAN runtime test, encrypted remote implementation, automatic port mapping or relay service is certified.

## Durability and product flow

119–121 close their controlled lease-holder/Python/combined restart cases. They do not establish an atomic transaction across native commit, command record and park save. Unknown crash outcomes, stale/mismatched saves, durable custom metadata, repair, late join and retention/compaction remain open.

The lobby now implements admission, shared DLC, readiness and common-template loading. Arbitrary host park transfer, final host-controlled saving and permission/repair UX are still unimplemented. A complete game process restart is not automatically a supported resume of the new private lobby.

## Editing coverage and history

123 properties and 124–130 group work supersede the old broad statement that all scale/color/group support is untested. Remaining scope includes arbitrary resources, all custom grids, blueprints/dependencies, more editor/tool paths, history after another actor changes the same group, and long concurrent sessions.

128 native-history boundary fixes and later own counteraction history do not prove identical native undo stacks or unrestricted collaborative rebasing. Keep all affected group locks, complete editor-grid reconstruction and command identity/version checks explicit.

The retained early 129-Free failure must remain distinguished from completed 129 stages and later 130 mixed-building evidence. A visible DLC model on an unlicensed peer must never be used as entitlement proof. A remote client ownership declaration is not independently verified Steam licence authentication.

## UI, measurements and lifecycle

The owner accepts the current English stacked-button layout. Retain the three false transition samples as a measurement caveat, not a new visible defect claim. Literal label/hint rendering is not proven solely by completion flags.

The input-startup error is corrected by the game module's readiness promise, distinct from browser engine readiness; delayed-order regression and a successful owner run support that fix. Continue testing control-context/menu cleanup and world transitions under failure.

Separate callback work, startup, scheduling gaps, network RTT, effect readback and displayed-frame latency. Cross-PC one-way measurements need synchronized clocks or an alternative measurement design. No linear extrapolation from 100,000 synthetic records or 2,701 simple rocks to arbitrary parks.

The reported exit crash remains unisolated. Own logging and successful BYE drain do not prove crash-free process shutdown. Long soaks, realistic mixed parks, broader automated game regressions and presented-frame capture remain needed. Kepler's exact pacing mechanism remains hypothetical.
