# Current research status

**Updated 2026-10-26. Runtime evidence through 118; 119 prepared only. Local supported-scenery prototype, not released internet co-op.**

[Overview](../../README.md) · [Latest evidence ledger](DIAGNOSTICS_107_119.md) · [Earlier native ledger](DIAGNOSTICS_085_107.md) · [Native bridge](../networking/NATIVE_BRIDGE.md)

## Verified in running games

- Own build-profiled x64 DLL, direct Lua strings, GC controls, bounded asynchronous Named Pipes and own logger work without ACSEDebug. ACSE remains the loader; Python runs outside both local Sandboxie boxes.
- 091–094 replicate manual Create/Move/Delete and live-session Undo/Redo. 095–102 cover controlled lost-ACK/pipe/Python/saved-Guest recovery and ordered catch-up; 102 records actual catch-up overlap.
- 103/104 establish reverse and separate-object bidirectional editing. 105 converges but has only partial overlap and a preview-related wait.
- 106 proves A→B independent visual proxies. **107** completes bidirectional previews across independent generations with duplicate/old/echo rejection and cleanup.
- **108/109** commit remote placements with separate native preview tokens while the receiver's own uncommitted preview remains active. Cancelling the own preview retains committed remote objects. 109 proves remote application/commit overlap, not local manual input overlap.
- **110** combines live previews and manual Create; **111** automatically confirms prepared ordinary placements and records local commit overlap in three of four rounds, remote application/commit overlap in all four. Each client ends with eight objects and no ghosts.
- **112/113** cover confirmed Moves and live dragging with Commit/Cancel in both directions while the receiver retains its own placement preview. Existing parts are edited; no replacement part is created for a Move.
- **114** shortened A→B Delete proves source absence before publication, one remote deletion, unchanged duplicate skips and preserved own preview.
- **115** transfers nine manual source history steps as explicit receiver counteractions during B's own preview; late Create cannot resurrect the deleted object. This does not certify receiver native undo-stack equivalence.
- **117 Test 5** permits cross-creator Move/Delete with versioned per-object leases, rejects Move/Delete conflicts before game operations, verifies ESC rollback/release, suppresses old Creates and ends with matching registries and no locks.
- **118** recovers both pipes without restarting games/Python: held Move lease preserved through disconnect, conflicting access denied, baseline verified after ESC; lost post-application ACK retried without a second commit. Receiver own preview stays active; final state matches and all participants complete.
- **085** local persistent menu/dialog proof remains archived; it is not a real host/join lobby.

## Important incomplete and historical results

116 connected and processed 101 commands but terminated on its own-object edit restriction. It is not a completion pass; 117 addresses shared-object authority. Earlier failed revisions of 107–118 are superseded only by the explicitly identified successful runs in the ledger.

The retained 087 native/Python pair is not a matched completion pass and cannot explain the earlier 657-ms gap. 101's completion did not prove overlap; 105's completion did not prove all-phase overlap.

## Transport and latency

Kepler's history-dependent seconds-long waits in 082/083 were unsatisfactory for responsive editing. Exact internal throttling remains hypothetical; HTTP itself is not rejected. The preferred local boundary is Lua → own DLL → asynchronous Named Pipes → external Python. Workers copy/transfer data and write logs; game APIs remain on the game thread.

107 preview receipt→readback ACK means: **20.45 ms A→B / 21.47 ms B→A**. 117 verified-command receipt→receiver verified ACK: **85.37 ms mean / 113.05 ms max**, with lock acquisition measured separately. 118 B application verification: **79.10 ms**. Its **2,124.39-ms** command receipt→confirmed ACK includes an intentionally injected two-second interruption and is not normal transport latency.

Readbacks do not measure displayed frames. Callback execution, Advance spacing, initialization, sampling, native operation completion and end-to-end confirmation are different intervals. Aggregate Advance gaps remain unattributed; fast diagnostic callbacks do not prove stutter-free rendering.

## Derived architecture

Keep immutable committed commands, versions, outcomes, mappings and tombstones separate from generation/sequence-based ephemeral previews. Separate native preview tokens isolate the tested remote actions from local placement previews. Acquire object leases before mutation; preserve uncertain ownership through disconnect and reject stale lease releases.

Creator identity is not exclusive editing ownership. A logical network key maps to a local Part-/Entity-ID; native IDs may differ between clients or change after reconstruction. Applied-command status and park-save inclusion are different facts.

## Next work

1. **119, prepared only:** restart the client holding an unconfirmed edit while the other client/Python continue; validate a matching loaded baseline, restore mappings/status and retire the old lease before issuing a fresh one. No 119 save has been authorized or performed.
2. Authenticated/encrypted companion networking across two computers; local Named Pipes are not a WAN transport.
3. Durable metadata/checkpoint integration, unknown commit outcomes, mismatched-save repair, late join and safe retention.
4. Collaborative Undo policy/rebasing, more resources/properties/scale/groups and broader failure/soak testing.
5. Host/join/baseline-transfer/loading/saving UX; revisit 085 after the architecture settles.
6. Isolate the reported exit crash and measure presented frames under realistic load.

Established setup: PC2 1.11.4.1011357 / ACSE 0.729. Compatibility across executable builds, arbitrary-crash exactly-once effects, full park simulation and a released playable internet mod remain unverified.
