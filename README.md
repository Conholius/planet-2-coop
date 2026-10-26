# Planet Coaster 2 — Real-Time Co-op Research

> **Project status — 2026-10-26, runtime evidence through 118; 119 prepared:** Own DLL, Named Pipes and external Python now support bidirectional live previews, manual scenery/history effects, separate-token commits during active own previews, shared-object leases/conflicts and controlled pipe recovery without duplicate actions. **Local diagnostic prototype, not a released internet alpha.**

We are investigating how two players might build in the same **Planet Coaster 2** park in real time. The current scope is supported scenery: confirmed changes, logical object mappings, guarded application and recovery. Next priorities are restarting a client while it holds an object lease (119), durable state reconciliation, and a secured remote companion connection. Internet play, a host/join lobby and automatic general recovery are not yet verified. Guests, rides, terrain, economy and full simulation synchronization remain outside the initial scope.

## Progress at a glance

| Milestone | Current evidence |
| --- | --- |
| Custom Lua mod loads | **Verified in PC2:** ACSE 0.729 loads the diagnostic mod; ForgeUtils 2.7.0's hook manager can be required. |
| ACSE world component survives park transition | **Verified:** minimal component with `Shutdown()` deactivates in `startscreenglobe` and is recreated in `tropicalworld` (diagnostic 005). |
| Editor and undo API visible in the park | **Verified:** diagnostic 006 found `worldAPIs.editors`, `CreateUndoOperationsHierarchy`, and four `api.undo` methods as functions in `tropicalworld`. **Presence checks only.** |
| Create an undo hierarchy | **Verified:** invoked successfully from our component (007/008). |
| Create, move, delete, save and reload a scenery part | **Verified for AQ_Rock_04:** diagnostics 009–025. |
| Ordered commands, duplicates and conflicts | **Verified locally:** 028/029; separate A/B replay states matched after twelve inputs in 030. |
| Native HTTP transport | **Verified:** owner-controlled loopback GET, HTTP status and text response via Kepler; active Frontier connection is not required once context is ready (037b–047). |
| Relay message exchange | **Verified on two simultaneous local clients:** later tropical-park repeat of 038, three messages each. Original sequential 038 is historical; internet testing remains pending. |
| HTTP command application | **Verified on both local clients:** scripted Create/Move/Delete and native Undo/Redo with duplicate suppression (071–076), extending the earlier local validation tests. |
| Grouped creation | **Verified for AQ_Rock_04:** 2,701 rocks / 13 commits, groups up to 500 (050–054). |
| Recovery | **Controlled two-client tests passed:** ACK refusal, TCP resets, resumed server restart and Guest checkpoint reload while Host stays alive (075–078). Arbitrary crash safety remains open. |
| Native history after reload | **Unavailable in the tested restart (064).** Move counteractions work from manually transferred action data (065). |
| Registry and performance | **Passed:** synthetic minimal/full registry tests to 100,000 entries (066), real-object queries/moves with 2,701 rocks (067/068). |
| Manual scenery over own transport | **091–094 passed:** manual Create/Move/Delete and live-session Undo/Redo; verified effects and unchanged duplicate skips. |
| Pipe and companion recovery | **095–102:** lost confirmations, real pipe cuts, 18 companion restarts, controlled saved Guest restart and ordered catch-up; 102 establishes real overlap. |
| Bidirectional edits | **103/104, 112–115:** manual supported effects/history and live dragging with receiver preview protection. **117:** peer-created objects editable under versioned leases; Move/Delete conflicts rejected before mutation. |
| Live remote preview | **106/107 passed:** independent A→B then bidirectional streams, generations, duplicate/old/echo guards and cleanup. **110/111:** visual previews combined with committed placements. |
| Independent commits and real overlap | **108–111 passed:** separate native preview tokens preserve own previews and committed remote parts after ESC. 111 coordinated automatic confirmations overlap locally in three of four rounds and remotely in all four. |
| Locked-edit recovery | **118 passed:** held lease survives pipe loss; conflicting access denied; lost application ACK retried without a second effect. **119 client restart while holding a lease is prepared only.** |
| Main-menu integration | **085 local UI proof:** persistent Koop entry and 20 open/close cycles; real lobby/session creation remains unimplemented. |
| Catalogue lookup | **Targeted queries passed (070):** avoids the 7,263-row materialization measured separately in 069. |
| Kepler decision | **082/083:** repeated native requests develop roughly one-second waits; spacing and a quiet pause affect them. Set aside as the preferred transport; the exact internal limiter remains unknown. |
| Own native communication | **084 Step 11 passed:** two local clients in separate sandboxes, Python outside, 1,000 verified messages each way and continued reverse traffic during a two-second forwarding delay. |
| Own diagnostic logger | **Passed with and without ACSEDebug:** 1,000 exact test messages each; own asynchronous file output. ACSE remains the loader; this is not a full interactive debugger. |

The successful 005/006 logs came from a **copied test installation launched outside Sandboxie**. They establish PC2 behavior in that copied installation, **not** validation of the fully sandboxed launch path. A separate Sandboxie setup is documented below. See the [runtime test record](docs/testing/RUNTIME_TESTS.md).

## Where to start

- **[Documentation guide](docs/README.md)** — a map of the project by topic.
- **[Current research status](docs/research/STATUS.md)** — concise verified findings, limitations and next milestone.
- **[Runtime tests (through 118, 119 prepared)](docs/testing/RUNTIME_TESTS.md)** — what was actually tested, failures and controls.
- **[Scenery placement and undo](docs/placement/README.md)** — the path toward creating a durable park object.
- **[Sandboxie test setup](docs/ISOLATED-INSTALLATION.md)** — separate host/guest boxes, token compatibility and isolation caveats.
- **[Prototype plan](docs/prototype/PLAN.md)** — acceptance criteria for one replicated scenery part.

For historical experiments and traceability: [research log](docs/research/LOG.md), [evidence index](docs/research/EVIDENCE.md), [open questions](docs/research/OPEN_QUESTIONS.md).

## What we know — and what we do not

Our component now uses the scenery hierarchy, create/edit/destroy operations, completed previews and single commits. Creation, movement and deletion were checked after local save/manual reload. Two identical rocks can be addressed independently. Commands reject tested ordering errors and conflicting ID reuse. See the [007–034 diagnostic ledger](docs/research/DIAGNOSTICS_007_034.md).

Diagnostic 030 matched canonical states without networking. The later 038 repeat and 071–082 now establish simultaneous local clients, scripted replicated operations and one ordinary confirmed host placement. [Native HTTP transport](docs/networking/TRANSPORT.md) works with a ready Kepler user context; [latency profiling](docs/networking/HTTP_LATENCY_080_082.md) and 083 record native-request delays. [The DLL/Named-Pipe bridge](docs/networking/NATIVE_BRIDGE.md) now carries actual manual scenery effects, controlled recovery and bidirectional edits. The [085–107 evidence ledger](docs/research/DIAGNOSTICS_085_107.md) preserves the earlier native results; the [107–119 ledger](docs/research/DIAGNOSTICS_107_119.md) records bidirectional previews, independent commits, actual overlap, shared-object conflicts and locked-edit pipe recovery. Remote computers, client restart while holding a lease and automatic durable recovery remain open.

Read the [050–068 evidence ledger](docs/research/DIAGNOSTICS_050_068.md), [recovery/history findings](docs/networking/RECOVERY_AND_HISTORY.md), [035–049 evidence ledger](docs/research/DIAGNOSTICS_035_049.md), [transport/editor measurements](docs/networking/BENCHMARKS.md) and [proposed HTTP synchronization design](docs/networking/HTTP_SYNC_DESIGN.md). The complete product architecture remains proposed; the [069–082 ledger](docs/research/DIAGNOSTICS_069_082.md) preserves HTTP history and the [085–107 evidence ledger](docs/research/DIAGNOSTICS_085_107.md) documents the newer native path.

An earlier custom world component caused a crash during the menu-to-park transition. A later minimal component that included `Shutdown()` passed that transition; because other probes were removed at the same time, **we cannot attribute the fix solely to `Shutdown()`**. Full history: [runtime tests](docs/testing/RUNTIME_TESTS.md).

## Compatibility and safety

The runtime logs identify **PC2 1.11.4.1011357**, **ACSE 0.729**, **ForgeUtils 2.7.0** and **ACSEDebug 0.014**. The cross-game ACSEDebug package captured log messages, but its **debug GUI and native helpers are not verified safe in PC2**; avoid the GUI. The exact package provenance should not be inferred from the logs. The newer own-logger and Step-11 messaging tests run without ACSEDebug. The owner still reports a crash reporter at game exit; its cause is unknown and successful in-test channel closure is not proof of crash-free game shutdown.

Use only backed-up, disposable installs and test parks. The [Sandboxie notes](docs/ISOLATED-INSTALLATION.md) describe a past startup compatibility setting, `UnstrippedToken=y`, which **reduces token isolation**. It does not prove a Denuvo defect or establish full cloud/save isolation. Do not use the old diagnostic launcher without checking its mod-restoration side effects.

This repository contains our own notes, not redistributed game binaries, assets, dumps, OVL/OVS files, decompiled scripts, private logs or credentials. Respect third-party licenses and service protections; do not bypass anti-cheat.

## Project reference pages

| Area | Page |
| --- | --- |
| Lua / world architecture | [Architecture](docs/architecture/OVERVIEW.md) |
| Editing / undo / creation | [Placement](docs/placement/README.md) and [ACSE + ForgeUtils research](docs/placement/ACSE_FORGEUTILS.md) |
| Current local transport and diagnostics | [Own DLL, Named Pipes and external companion](docs/networking/NATIVE_BRIDGE.md) |
| Transport history | [Native HTTP contract and service dependence](docs/networking/TRANSPORT.md) |
| Replication semantics | [Identity, application acknowledgements and recovery](docs/networking/HTTP_SYNC_DESIGN.md) (historical HTTP design; transport-independent guards retained) |
| Performance | [HTTP, editor, registry and query measurements](docs/networking/BENCHMARKS.md), [080–082 latency analysis](docs/networking/HTTP_LATENCY_080_082.md) |
| Recovery and history | [ACKs, checkpoints and counteractions](docs/networking/RECOVERY_AND_HISTORY.md) |
| Saving / persistence | [Serialization](docs/serialization/README.md) |
| Tools and decompilation | [Modding references](docs/modding/README.md) |
| Contribution / evidence rules | [AGENTS.md](AGENTS.md) |
| Co-op Anything inspiration | [Co-op Anything](https://github.com/cranebeaker/coop-anything) and [PC2 research issue #74](https://github.com/cranebeaker/coop-anything/issues/74) |

## Credits and acknowledgements

- **[ACSE — Advanced Cobra Script Extender](https://github.com/OpenNaja/ACSE)** (OpenNaja and contributors) — Lua scripting-extension work; [license](https://github.com/OpenNaja/ACSE/blob/main/LICENSE).
- **[Cobra Tools](https://github.com/OpenNaja/cobra-tools)** (OpenNaja and contributors) — Cobra archive and file research; [documentation](https://opennaja.github.io/cobra-tools/).
- **[ForgeUtils](https://github.com/Distantz/ForgeUtils)** (Distantz and contributors) — PC2 Lua/JavaScript tooling and catalogue builders; [documentation](https://forgeutils.distantz.com), [license](https://github.com/Distantz/ForgeUtils/blob/main/LICENSE).
- **[Frontier Modding Club](https://discord.gg/Su4jXKk)** — linked by the ACSE project; community reference material is credited, **not redistributed**.

These are research dependencies and comparative examples, not endorsements or evidence of finished co-op.
