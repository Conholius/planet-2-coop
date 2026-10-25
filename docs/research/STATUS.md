# Current research status

**Updated 2026-10-25. Completed retained diagnostics reach 106; 107 code is supplied but untested. Local supported-scenery prototype, not released internet co-op.**

[Overview](../../README.md) · [Latest evidence ledger](DIAGNOSTICS_085_107.md) · [Native bridge](../networking/NATIVE_BRIDGE.md) · [Runtime history](../testing/RUNTIME_TESTS.md)

## Verified in running games

- The own profiled x64 DLL exchanges direct Lua strings, handles the tested GC pressure and provides asynchronous diagnostic output without ACSEDebug. ACSE remains the loader.
- Two local sandboxed clients communicate through separate Named Pipes and external Python. 084 Step 11 passed 1,000 verified messages each direction.
- 091–094 replicate manual Create, Move, Delete and live-session Undo/Redo, with application/world checks and unchanged duplicate skips.
- 095/096 handle lost confirmations and nine real pipe cuts/resumes per client. Corrected 097 handles 18 Python restarts; both clients, Python and supervisor complete.
- 098/099 restore a deliberately saved B checkpoint while A stays alive; B restores mappings/status and catches up three offline changes, including Delete, without resurrecting the object on a late Create.
- 100 converges but has staged release gates. 101 removes gates and completes but does not observe real overlap. **102** establishes real overlap without artificial catch-up gates: B restores through sequence 2 and applies 3–51 in order, skipping 52 duplicates.
- 103 sends manual Guest edits to Host; 104 sends each client's own three edits to the other. Logical mappings stay separate, with no unexpected publications and tested duplicate/echo suppression.
- **105 converges with only partial phase overlap.** Both clients complete; AllPhasesOverlapObserved=false. B-origin Create confirmation took about 17.79 seconds while the owner observed a wait for local-preview closure. Committing remote edits during a local preview is not solved by that result.
- **106LIVE2** displays A's live pose as a separate opaque rock/ring on B while B moves its own placement preview: 623 applied poses in two cycles, two roots created/destroyed, six stale/duplicate rejects and 8,336 own-preview checks. User visual confirmation and both native/Lua pairs plus Python complete.
- **085** proves a persistent local main-menu entry/dialog: 20 opens/closes and both completion markers. This is not a working multiplayer lobby and is deferred until the architecture is settled.

Detailed private-file anchors, counts, timing boundaries and qualifications are in the [085–107 ledger](DIAGNOSTICS_085_107.md). These are owner-run diagnostics, not an automated production QA suite. PC2 build 1.11.4.1011357 / ACSE 0.729 identify the established setup; compatibility with other executable profiles is unproven.

## Transport and performance decision

Kepler's history-dependent seconds-long waits in 082/083 were unsatisfactory for responsive editing. The exact internal limiter remains hypothetical; HTTP itself is not rejected. The preferred local boundary is own DLL → bounded asynchronous Named Pipes → external companion. Workers copy/transfer data; Lua/game API calls stay on the game thread.

106 measures **20.5641 ms mean / 34.1381 ms P95 / 61.4005 ms maximum** from Python update receipt to B readback-ACK receipt. This excludes A sampling/input delay and does not measure rendered-frame latency. Mean diagnostic callback costs are 0.012902 ms on A / 0.030214 ms on B; maximum Advance gaps are about 270/260 ms, with no unique cause established. Earlier callback gaps, including the 086/087 investigation, must not be relabelled as scene-transfer latency.

## Evidence qualifications

The retained 087 native log times out before first Python connection although its Python file completes. This retained pair cannot establish an all-participant pass or explain the earlier 657-ms gap. Historical successful claims must be checked against matched run evidence.

106 proves a resource-bound independent visual proxy for AQ_Rock_04 at scale one. It does not prove transparency, persistent scenery, safe concurrent commits or bidirectional previews. 107 is **prepared/unverified**.

Controlled checkpoint recovery does not establish atomic save/command persistence or arbitrary-crash exactly-once. Runtime entity IDs and local part IDs remain distinct from logical network IDs. Entity/transform readbacks and user visual observations are separate evidence.

## Derived architecture

Keep immutable ordered committed actions with revisions, tombstones, application proofs and checkpoint binding. Keep ephemeral preview poses in a separate generation/sequence/origin flow; latest-pose coalescing must not drop committed commands. Remote ghost rendering must not enter the ordinary undo/placement path or publish itself as a local action.

## Next milestones and unknowns

1. Run 107: simultaneous A↔B previews, independent stopping/restarting, stale generations, duplicate/echo guards and cleanup.
2. Resolve remote durable-edit application while a local preview is active; define same-object conflict authority and per-user Undo policy.
3. Add and test authenticated remote companion networking; Named Pipes are same-machine only.
4. Integrate durable metadata with matching saves, ambiguous-crash reconciliation and repair.
5. Finish lobby/baseline transfer/loading/saving UX; extend resources, scale, properties and groups.
6. Isolate the reported exit crash and measure presented frames/long-duration workloads.

Full park simulation (guests, staff, economy, paths, terrain, rides), general resource coverage, WAN play and released playable co-op remain unverified. Earlier HTTP, registry, catalogue, placement and persistence findings remain historical evidence in their existing ledgers.
