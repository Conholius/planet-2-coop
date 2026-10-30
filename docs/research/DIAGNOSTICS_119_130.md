# Diagnostics 119–130: recovery, properties and building groups

**Reviewed 2026-10-30. Owner-run tests with two actual local PC2 clients, own DLL/Named Pipes/external Python, without ACSEDebug. No internet result is claimed.**

[Current status](STATUS.md) · [Earlier ledger](DIAGNOSTICS_107_119.md) · [Build Together lobby](../networking/BUILD_TOGETHER_LOBBY.md)

## Evidence classification

The tables summarize retained private Python RESULT records, state snapshots and matching native client SUMMARY/completion records. Original logs, identifiers, saves, binaries and extracted game code are not published. A pass applies to the identified corrected run, not every revision carrying the same diagnostic number. Completed flags are considered together with operation/readback evidence.

## 119–123: controlled recovery and multiple scenery resources

| Diagnostic / retained result | Verified in running games | Boundary |
| --- | --- | --- |
| **119**, `Python119.log`, matching A and both Guest phases | Guest game process restarted during a held edit; matching existing checkpoint loaded, two command records restored, old lease mutation/release rejected, five duplicate deliveries skipped on restored B. Only one new remote Move committed; both ended at (20,5,10), revision 3; all participants complete. | Reviewed corrected run reused an earlier authorized save; no additional save. Opening a new tropical park instead of the matching checkpoint failed and is not a pass. Not general arbitrary-crash recovery. |
| **120**, `Python120.log`, `Monitor120.log`, `State120.json`, matching clients | Two injected Python restarts, three boots total; same session restored, held edit/ESC rollback reconciled, old release rejected, receiver applies once. Both clients and supervisor complete. | Game processes remain alive; measured restart confirmation includes the deliberate outage. |
| **121**, `Python121.log`, `Monitor121.log`, `State121.json`, A plus both Guest phases | Combined game/Python restart: dead Guest incarnation retired, two checkpoint command records restored, unconfirmed drag discarded, old mutation/release rejected and new Move applied once. All complete; zero saves requested. | Explicit matching baseline and controlled fault points; no general save/commit/status atomicity. |
| **122**, `Python122.log` and matching native pair | Seven distinct resources, 19 accepted Create/Move/Delete commands, 19 duplicate skips and 19 own echoes skipped. No open reservations/errors; all complete. | Tested resources, not the entire catalogue or all object classes; properties/groups/history not certified by this run. |
| **123**, final `Python123.log`, `State123.json`, matching native pair | Four resources, 18 commands, 18 duplicate/echo skips. Actual scale and semantic RGB channels transferred; property-only changes and reset-to-default validated. One protected application per client; all complete. | Scale is preserved during remote Move; named channels remain strictly checked. The empty channel is treated separately rather than weakening named-channel comparisons. This final run does not certify general property Undo/Redo. |

123's final property counters: A five color-only changes and one scale-only change; B five color-only changes and three scale changes, two without movement. Both reset checks passed; A also exercised color cancellation. `RESET_CHANNEL` / `RESET_RESULT` distinguish preview and committed readbacks. Earlier crash/reset revisions remain failures, superseded only for the corrected tested path.

## 124–128: grids, groups, manual merges and history

| Diagnostic / retained result | Verified in running games | Boundary |
| --- | --- | --- |
| **124 Test 2**, `Python124test2.log` / `State124test2.json` and native pair | Walls and logical group membership, individual Move/Delete; seven settled commands, all complete. | Opening a building for editing is distinct from selecting the whole group. No general group transform, custom grid settings or history proof yet. |
| **125 Test 2**, `Python125test2.log` / state and native pair | Whole groups moved/rotated; ten settled commands, stale/duplicate guards and matching readbacks; all complete. | Actual confirmation/tool exit matters; selecting/highlighting a group alone is not a committed Move. |
| **126 Test 5**, `Python126test5.log` / state and native pair | Manual Split plus Python-triggered Merge replicated; authoritative group grid and actual initialized editor grid verified; ten settled commands, all complete. | `manualMergeUiTested=false`, `mergeTrigger=PythonJoinCommand`; this run is not evidence of UI-driven Merge. |
| **127 Test 2**, `Python127test2.log` / state and native pair | Actual manual UI Merge captured on both A and B; ten commands settled, editor grids verified, all complete. | Separate from the earlier scripted join path. |
| **128 Test 5**, `Python128test5.log` / `State128test5.json` and matching native pair | 18 settled commands; eight source Undo/Redo proofs for Split/Merge across A and B; actual editor grid includes origin, orientation and cell settings. All complete. | Receiver applies verified effects, not a claim of identical native undo stacks. Other retained 128 files include later failed 129-development revisions; do not select evidence by modification time alone. |

Two important corrected boundaries:

- Remote commit must finish before its undo checkpoint is issued. The checkpoint separates tested remote changes from subsequent local native Undo grouping; **it is not a park save**.
- Group restoration must wait for a fully initialized editor and restore/check the complete editor grid. Membership or a raw default origin alone did not establish the correct rotated building grid.

Those findings come from the corrected 128 runtime readbacks, `historyProofs`, `editorGridChecks` and commit/checkpoint markers; static API names alone would not establish them.

## 129: an evolving group-editor test series

129 is not one monolithic completion result. Retained snapshots establish these specific completed variants, with matching native A/B sessions stored under the reused 128 transport/log names:

| Variant | Committed commands A / B | Recorded result |
| --- | ---: | --- |
| `State129-Parallel.json` | 2 / 2 | Matching client reports; group changes while the other client edits a different group, protected preview checks; complete. |
| `SplitMerge/State129-Parallel.json` | 2 / 2 | Separate retained Split/Merge stage; keep its exact scope separate from group transforms. |
| `State129-Concurrent.json` | 3 / 3 | Completed concurrent group test and matched reports. |
| `State129-History.json` | 6 / 6 | Completed cross-client group history stage and matched reports. |

Derived implementation rules carried into the current prototype: acquire relevant group leases before Move/Split/Merge, include both sides of a Merge, reject locked work before native mutation, capture transforms before tool teardown and do not diagnose a preview disappearance during the commit teardown itself as an independent cancellation. Immutable commands and own histories are separate from temporary previews.

**Retained `State129-Free.json` is an aborted early revision**, despite the owner's subsequent successful free-building work. Do not publish it as a complete pass. New-wall/free-group capability is additionally evidenced in the later completed 130 run below; that does not retroactively change the failed 129 artifact. The owner's one-wall Undo/Redo edge-case report remains narrower evidence than a separately matched archived completion for that exact case.

## 130: mixed scenery/groups and shared DLC catalogue

Final `Python130.log`, `State130.json` and the matching A/B native pair establish:

- **43 settled commands**, A 38 / B 5; all commands settled with 86 recorded duplicate acknowledgements/skips, no open locks and no errors.
- Mixed loose scenery and grid walls, new walls/group extensions, group transforms, Split/Merge, removal and own Undo/Redo effects are represented in the final command graph. Both clients report and complete.
- Two `LOCKED_BY_A` denials were recorded for B; rejected access does not authorize a game mutation.
- Both catalogue inventories contain **7,263 entries**; **5,282 shared allowed entries** remain after the DLC comparison (1,981 excluded). Both filters become ready before free building.
- The group graph retains membership, resource, pose, scale, semantic colors and complete grid data. Local native IDs are resolved per client rather than used as global identities.
- `Completed=true`, `PythonCompleted=true`, both Lua/native completions true, `saveCalls=0`.

The owner observed some DLC models rendering on a client without that DLC, followed by a native entitlement refusal when editing. **Visible assets are not ownership proof.** The implemented shared filter and acceptance gates restrict supported requests to the compared entitlements. They are not a bypass or cryptographic verification of a remote Steam licence.

The individual-wall trash action required its actual selection/popup path; a whole-building-only guard did not capture that UI action. The corrected mixed run succeeds, but catalogue counts and this finite test do not certify every resource, editor, DLC combination, blueprint or asset dependency.

## Remaining limits

All results are local two-client diagnostic sessions. There is no two-PC internet runtime result, full-park file transfer, complete simulation sync, final host-save workflow, general collaborative-history rebasing or arbitrary-crash exactly-once guarantee. Later [lobby tests](../networking/BUILD_TOGETHER_LOBBY.md) add admission and coordinated template loading; [internet transport](../networking/INTERNET_PLAN.md) remains proposed.
