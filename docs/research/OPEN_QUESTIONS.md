# Open questions and next experiments

**Updated 2026-10-26.** [Status](STATUS.md) · [107–119 evidence](DIAGNOSTICS_107_119.md)

## Immediate: restart a lease holder — 119 prepared

118 recovers a live game's pipe and in-memory state. A dead client loses its Lua state, active tool and native preview token; this is a different recovery boundary.

Proposed test: keep A/Python alive; stop B while it holds an unconfirmed Move; deny A a conflicting edit; reload a matching B baseline; verify committed world state and resolve local mappings before restoring command status; invalidate the previous process's lease and allow a new operation under a fresh identifier. Replayed old commands/releases must not mutate or unlock newer work.

No implementation/run is certified for 119. A reproducible test is expected to need one new B baseline save before editing, subject to explicit owner authorization. Rebuilding the interactive drag is optional; restoring consistent committed state and resolving ownership are required.

## Preview and editor scope

107–111 establish bidirectional proxies plus separate-token committed placements; 112–115 establish Move/live drag/cancel/Delete/history application with receiver preview protection. These close the earlier narrow coexistence blocker.

Still open: preview cleanup after arbitrary world/process failures, stalled peers, queue overload, long sessions, multiple tools/resources, scale/properties/groups, transparent/nonselectable visualization and presented-frame latency. A prefab visual is not a persistent park object.

## Authority and Undo

117 proves cross-creator Move/Delete, first-valid-request/versioned leases and tested conflicts; 118 adds two controlled disconnect points. Still open: dead-process ownership retirement, broader stale/late-message combinations, fair admission, authority migration and malicious/unauthorized peers.

115 receiver counteractions do not synchronize native history. 117's limited per-actor history/revision policy is not general collaborative Undo rebasing. Define behavior when another actor has changed the same object.

## Remote transport and product workflow

- Implement authentication/encryption and test two computers; Named Pipes are same-machine only.
- Preserve intended Host session → Guest join → compatible baseline/load → Host-controlled save workflow.
- 085 proves a local menu/dialog, not admission, park transfer or network lobby; defer polishing until architecture is ready.
- Package profile-compatible binaries, endpoint permissions, clean startup/shutdown and actionable error handling.

## Durability and lifecycle

Completed checkpoint tests do not establish an atomic transaction spanning native commit, status journal, application ACK and park save. Unknown crash outcomes, mismatched saves, automatic persistent metadata, repair, late join, history/tombstone compaction and arbitrary shutdown still require evidence.

The recurring game-exit crash remains unisolated. Compare clean/no-mod, ACSE-only and own-DLL lifecycle controls; do not assign a cause from in-test completion. Own logging cannot capture every pre-load crash or replace native crash dumps.

## Measurement and QA

- 109 remote overlap is not local input overlap. 111 demonstrates actual local overlap in three of four coordinated automatic rounds.
- 116 is incomplete; 117 Test 5 and 118 have matching completions.
- Obtain a matched corrected 087 pair before certifying it or explaining the earlier 657-ms gap.
- Separate callback time, scheduling gaps, initialization, source sampling, effect verification and rendered latency.
- 118 confirmation includes a deliberate two-second outage; do not compare it with normal Kepler/pipe timings as a speed regression.
- Broaden realistic parks, sustained traffic, GC/allocation/failure profiling and automated regression coverage. Synthetic 100,000-entry registers are not 100,000 real-object tests.

Kepler's exact pacing mechanism, full simulation synchronization, arbitrary-crash exactly-once and a released internet alpha remain unverified.
