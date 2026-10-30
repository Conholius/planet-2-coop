# Build Together — Planet Coaster 2 co-op research

> **Status — 2026-10-30:** Two real local clients can build with supported scenery and grid groups through our own DLL, Named Pipes and external Python. The private **Build Together** lobby supports either player as host, one-time invitations, explicit guest approval, shared DLC checks and coordinated tropical-park loading. **Internet play on two PCs is the next planned step; it is not implemented or verified yet.**

This is an experimental local building prototype, not a released internet alpha or full park-simulation multiplayer. Guests, rides, paths, terrain, economy and AI are outside the proven scope. ACSE remains the loader; our own logger replaces the diagnostic dependence on ACSEDebug, not the entire engine debugger.

## Verified local progress

| Area | Current evidence |
| --- | --- |
| Native communication and logging | Build-profiled x64 DLL, direct Lua strings, bounded asynchronous Named Pipes and own file logger; actual two-client message/edit tests without ACSEDebug. |
| Manual scenery | Create, Move, Delete and supported history effects in both directions; source/receiver readbacks, logical identities, duplicate and own-echo suppression. |
| Preview coexistence | Bidirectional visual proxies and separate-token committed placements; receiver own previews retained in tested cases (107–115). |
| Authority and recovery | Shared-object/group leases and conflict no-ops; controlled pipe, Python, client and combined restarts (117–121). Checkpoint recovery is not arbitrary-crash exactly-once. |
| Resource properties | Multiple scenery resources, actual scale preservation during Move, named RGB channels and corrected reset-to-default (122/123). |
| Grid buildings | Walls/groups, whole-group translation/rotation, manual Split/Merge and history effects; complete initialized editor-grid checks and remote commit/checkpoint separation (124–128). |
| Concurrent group work | Specific parallel/conflict/history variants of 129 complete. Its retained early free-building failure is not relabeled as a pass. |
| Mixed building | 130 final run: 43 settled commands, 86 duplicate records, matching completion reports, no open locks/errors; loose scenery and grid groups together. |
| Shared DLC catalogue | Both inventories 7,263 entries; 5,282 jointly allowed entries, 1,981 excluded. Both filters confirmed before free building. |
| Private lobby | Host selectable on A or B; invitation, pending request, reject/approve, one guest, readiness and local park-start/build integration. Wrong/consumed codes rejected. |
| Current interface | English Build Together panels and code hints; vertically stacked actions; corrected game-UI readiness gate. Five-button Host view measured inside bounds and visually accepted by the owner. |
| Internet connection | **Planned only:** Python-to-Python TCP/TLS with IPv4 and IPv6, no VPN app for the first test; optional future relay fallback. |

## Start here

- [Current status and limits](docs/research/STATUS.md)
- [Build Together lobby, UI corrections and runtime evidence](docs/networking/BUILD_TOGETHER_LOBBY.md)
- [119–130 diagnostic ledger](docs/research/DIAGNOSTICS_119_130.md)
- [Direct IPv4/IPv6 internet plan — not implemented](docs/networking/INTERNET_PLAN.md)
- [Documentation guide](docs/README.md), [runtime index](docs/testing/RUNTIME_TESTS.md), [open questions](docs/research/OPEN_QUESTIONS.md)

## What “verified” means here

The owner ran two actual game clients on one Windows PC and supplied private logs/state plus visual observations. Matching run identities, native/world readbacks and final outcomes are checked; isolated Completed labels or API names are insufficient. Offline mock/regression tests cover transport/UI logic separately. No second-PC internet acceptance run has occurred.

The latest menu-only test reports both LuaCompleted/NativeCompleted pairs, PythonCompleted and state Completed true, with gameChanges/saveCalls zero. Three false layout samples remain recorded during view transitions; later samples pass and the owner reports no visible button problem. This is not an every-frame layout or stutter guarantee.

Coordinated park start currently loads the same tropical template on both clients. It does not transfer an arbitrary host save. Durable host-save workflow, arbitrary crash reconciliation, late join and general collaborative Undo rebasing remain open. Native IDs and preview tokens are process-local; mod-defined object keys and versions provide the cross-client identity.

## Architecture and compatibility

Current tested path: **Game Lua → own DLL → local Named Pipe → external Python coordinator → peer pipe/DLL/Lua**. Game APIs remain on the game thread. Kepler was set aside because measured history-dependent one-second waits were unsatisfactory; its exact internal limiter is unknown. [Native bridge](docs/networking/NATIVE_BRIDGE.md) · [Measurements](docs/networking/BENCHMARKS.md).

Reported tested setup includes Windows/Steam PC2 **1.11.4.1011357**, **ACSE 0.729** and **ForgeUtils 2.7.0**. The native interface is tied to a verified executable profile; an unsupported game update must fail compatibility checks. Early diagnostics used ACSEDebug 0.014; current own-logger/lobby runs do not require it. The previously reported game-exit crash reporter remains unisolated; successful channel completion is not proof of crash-free game shutdown.

Earlier 005/006 lifecycle tests ran in copied installations outside Sandboxie; later two-client tests use the documented local sandbox arrangement. Do not transfer isolation claims between those runs. [Sandboxie notes](docs/ISOLATED-INSTALLATION.md).

This repository publishes research summaries, not raw private logs, developer-specific paths, invitation secrets, saves, game binaries/assets, OVL/OVS archives or whole decompiled scripts. Original prototype files remain in the private development workspace while portable packaging is prepared. No public ready-to-install release is claimed.

## Research history

[Evidence index](docs/research/EVIDENCE.md) · [Chronological log](docs/research/LOG.md) · [107–119 historical ledger](docs/research/DIAGNOSTICS_107_119.md) · [Recovery/history](docs/networking/RECOVERY_AND_HISTORY.md) · [Placement](docs/placement/README.md) · [Serialization](docs/serialization/README.md) · [Prototype acceptance plan](docs/prototype/PLAN.md) · [Contribution rules](AGENTS.md)

## Credits and acknowledgements

- **[ACSE — Advanced Cobra Script Extender](https://github.com/OpenNaja/ACSE)** (OpenNaja and contributors) — Lua scripting-extension work; [license](https://github.com/OpenNaja/ACSE/blob/main/LICENSE).
- **[Cobra Tools](https://github.com/OpenNaja/cobra-tools)** (OpenNaja and contributors) — Cobra archive and file research; [documentation](https://opennaja.github.io/cobra-tools/).
- **[ForgeUtils](https://github.com/Distantz/ForgeUtils)** (Distantz and contributors) — PC2 Lua/JavaScript tooling and catalogue builders; [documentation](https://forgeutils.distantz.com), [license](https://github.com/Distantz/ForgeUtils/blob/main/LICENSE).
- **[Frontier Modding Club](https://discord.gg/Su4jXKk)** — linked by the ACSE project; community reference material is credited, **not redistributed**.

These are research dependencies and comparative examples, not endorsements or evidence of finished co-op.
