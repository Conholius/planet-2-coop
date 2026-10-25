# Diagnostics 085–107: native scenery, recovery and live previews

**Updated 2026-10-25.** Completed retained runs through 106 are distinguished below from failed/limited runs. **107 code was supplied in chat; no runtime result has been reviewed.**

[Current status](STATUS.md) · [Native bridge](../networking/NATIVE_BRIDGE.md) · [Earlier 083–084 ledger](DIAGNOSTICS_083_084.md)

## Evidence and environment

These are owner-run tests of two actual local Windows PC2 clients in separate Sandboxie boxes, with external Python and the own DLL/logger, without ACSEDebug where specified by the test setup. ACSE remains the loader. The established game build is 1.11.4.1011357; the native interface is tied to the tested executable profile, not a portable Lua ABI.

This update reread retained private Python and native summaries, plus the successful 106 records. It did not rerun games or modify installations/saves. Individual failed attempts are not promoted to successful outcomes. Raw logs, session/save identifiers, personal paths, game resources and decompiled scripts are not published.

## 085: local menu proof, parked for later integration

**Verified in a running game:** the retained persistent-menu run in Native084-Lobby01.log records 20 menu clicks, 20 dialog opens and 20 closes; seven Create and seven Join selections; zero ignored opens/selections. Both completion markers are true. Closing/reopening retains the menu entry. Earlier revisions lost the entry, disabled it or disrupted the main menu; they are superseded by this retained run, not erased from the history.

**Limit:** RealSessionCreated=false, GameChanges=0, SaveCalls=0. This is an actual menu/dialog integration proof, not a working multiplayer lobby, baseline transfer or shared loading flow. It is archived as diagnostic 085 and deliberately deferred until the architecture is settled. UI-stop acknowledgement was not awaited in the final cleanup record.

## 086–090: transport hardening with one client

| Diagnostic / private anchor | Observed result | Qualification |
| --- | --- | --- |
| 086: Native086.log / Python086.log | 60 unique messages, three connections, two intentional Python exits, two duplicates; native/Lua/Python completion true | Reconnect and deduplication in the tested message protocol; no game/save effects |
| 087: retained Native087.log / Python087.log | Python reports 60 messages and completion; the retained native file instead times out waiting for its first Python connection, with both native/Lua completion false | These retained files do **not** constitute a matched all-participant pass. Earlier conversation describes corrected reruns, but this update cannot certify them from this retained pair or assign a unique cause to the earlier 657-ms Advance gap |
| 088: Native088.log / Python088.log | 60 unique messages, three injected header/body/stored-response faults, four connections, three duplicates; all completion markers true | Fragmentation/retry checks include intentional pauses; no editor effects |
| 089: Native089.log / Python089.log | 15 cases: nine valid payloads, four length rejects, one truncated body and one timeout; 16 connections; all complete | Fixed receive buffer 4,096 bytes; tested boundary cases are not a general security audit |
| 090: Native090.log / Python090.log | 64 cases, 38 accepted values and 26 rejected values, exact text validation; all complete | Large IDs/length representations are preserved as text. Arbitrary large lengths are not permission to allocate or send oversized frames |

**Derived:** keep identifiers in exact text form across Lua/native/Python boundaries, enforce bounded frame lengths before body processing, and distinguish transport retry from application replay. One-client framing tests do not prove safe handling of every malicious peer.

## 091–094: manual edits over the own bridge

**Verified in running games:** matching A/B native logs and Python logs complete for these retained runs, with workerError=0.

- **091:** one manually confirmed Host Create is captured; Guest makes one create, one transform update, one preview and one commit, then rejects one identical duplicate. Host's distinct next preview remains active in the sampled checks. This supplies the native-pipe game-effect proof that was still pending as 084 Step 12 at the previous documentation cutoff.
- **092:** manual Move follows the initial Create. Guest records one create, one existing-part edit and two commits in total; two duplicate confirmations. Resource/transform/mapping checks pass.
- **Corrected 093:** manual Delete is confirmed on A before publication; B ends at object version 3, DELETED, with one destroy and three commits total across Create/Move/Delete; three duplicate skips. The final logs complete on both clients and Python.
- **094:** manual Undo/Redo for Create, Move and Delete passes all nine command steps, with nine duplicate confirmations and final object state DELETED. This is controlled live-session history behavior, not persisted multiplayer Undo ownership.

### Delete capture: actual popup path matters

Private Native093.log records both _Delete and DeleteModularScenery monitors installed. GetOpenPopUp identifies the active popup entity, mapped registered part and Select editor. The observed invocation is ENTER path=MODULAR method=DeleteModularScenery on the world's SelectAndEdit component, followed by one delete hook. The inspected popup's _Delete method still equals the original rather than that module wrapper.

**Derived:** a wrapper installed on an assumed editor/module is insufficient evidence of interception. Resolve the actual active instance/component and verify source absence after native completion before publishing DELETE. Do not assert that both wrappers ran merely because both installation messages exist.

## 095–097: lost confirmations, pipe cuts and Python restart

| Diagnostic | Retained completed result | Scope limit |
| --- | --- | --- |
| 095 | Nine manual action/history steps; B skips nine replayed actions after lost confirmations; both clients and Python complete | Controlled loss points and a live client ledger |
| 096 | Nine real pipe breaks/resumes on **each** client, ten connections each; B skips nine application replays; all complete | Native worker reconnect and application deduplication are separate layers |
| Corrected 097 | 18 Python restarts; both clients record 18 breaks/resumes and 19 connections, final generation 19; B skips nine action replays; native/Lua/Python and supervisor complete | Journal/restart workflow tested, not arbitrary client-crash atomicity |

Keep immutable command identity, payload validation, origin, sequence/revision and verified application status. A received frame or stored relay record is not itself a completed editor commit.

## 098–102: saved Guest restart and ordered catch-up

- **098:** B saves one new local checkpoint after Create+Move, then restarts while A continues. Phase 2 restores two included records, skips old effects and performs only one new Move/commit. Python reports restored=true, oldDuplicates=[1,2], saveIntents=1 and completion; all three native process logs complete.
- **099:** while B is offline, A publishes sequences 3–5. Restored B performs two Moves and one Delete, three commits, and ends DELETED at version 5; six duplicate skips include the late old Create. Python reports replayed=[3,4,5], pending=[], lateCreateSkipped=true, saveIntents=1 and completion.
- **100:** eventual convergence and completion passed, ending at version 7/DELETED, but the diagnostic's staged release/confirmation flow made B visibly trail A. It is not evidence of unrestricted overlapping catch-up.
- **101:** artificial catch-up gates are removed. B reaches version 10/DELETED, skips 11 duplicates and completes; Python explicitly reports overlapObserved=false. Human publication happened after B caught up, so this does not prove changes arriving during an existing backlog.
- **102:** automatic A changes create real overlap without artificial catch-up gates. Python reports SynchronizationCompleted=true, RealOverlapObserved=true, artificialCatchupGates=false and TestVerdict=PASSED. B restores through sequence 2, applies sequences 3–51 in order (48 Moves and one Delete), skips 52 duplicates and ends version 51/DELETED. Both Guest phases, Host and Python complete with no worker errors.

**Limit:** these are explicit completed-save/checkpoint workflows. A's later runtime changes are not automatically included in B's saved checkpoint. They do not prove atomic park-save/metadata persistence or safe blind replay after an arbitrary crash.

## 103–105: reverse and bidirectional committed edits

| Diagnostic | Verified result | Important limit |
| --- | --- | --- |
| 103 | Guest B manually publishes Create/Move/Delete; A applies/commits three, skips four duplicates; B skips four own echoes. No unexpected publications or remote capture hits; all complete | Guest-originating edit path for one supported resource |
| 104 | Each client publishes three own edits and applies/commits three peer edits; four duplicates and four echoes skipped per client; no bad publications/unexpected actions; all complete | Deliberately ordered six-step test, not simultaneous conflict resolution |
| 105 | Both objects reach version 3/DELETED on both clients; three remote applies/commits each, four duplicates/four echoes each, all completions true | TestVerdict=PASSED_PARTIAL_PHASE_OVERLAP; OverlapObserved=true but AllPhasesOverlapObserved=false |

104's local part mapping differs across clients: the B-origin object maps to local part 1184 on A and 1183 on B. This is direct evidence that logical network identity must remain separate from local part IDs.

In 105, the B-origin Create's publish-to-applied acknowledgement took about **17,792.64 ms**, while the user observed application after the local preview closed. The remaining command confirmations were about 94–217 ms. This is an application/preview interaction in this test; it is **not** proof of a 17-second pipe-transfer time or a solved commit-while-own-preview problem. Zero sampled preview interruptions do not prove that a remote durable commit can safely execute during every local preview.

## 106: independent remote preview, successful 106LIVE2 run

### Observed in extracted material

Source anchors inspected privately include Editors.Scenery.SubModePlacement, SubModeBase preview-start guards, ObjectPlacementGizmo, PlainRotateGizmo, basemodularscenery, basesimplescenery_flexicolour, AssetPackageStream / scenerypreview specdefs and sharedprefabsneededearly.lua.bin. Names and prefab/component fields are static evidence, not render success by themselves. PC2 bytecode reconstruction requires special header/vector handling; incomplete decompilations were cross-checked where relevant.

The ordinary editor preview uses a shared undo-preview path. Starting another normal preview is not an independent remote visualization mechanism. Bare SimpleModel-style entities also do not establish resource residency or visibility.

### Verified in two running clients

The corrected **106LIVE2** retained run uses a custom resource-bound AQ_Rock_04 model prefab, a rotation-ring child and LocationBucketed streaming. B displays A's sampled live pose while B keeps and moves its own ordinary placement preview.

Private anchors: Python106.log, Host Native106-30900.log and Guest Native106-29132Guest.log. Their private session values match.

| Check | Result |
| --- | ---: |
| First cycle sent / applied / final ACK | 188 / 188 / 188 |
| Second cycle sent / applied / final ACK | 435 / 435 / 435 |
| Total applied poses | 623 |
| Remote roots created / destroyed on B | 2 / 2 |
| Rotation children created | 2 |
| Active/stale update/end rejections | 6 |
| B own-preview checks / own pose changes | 8,336 / 199 |
| Requested committed actions / saves | 0 / 0 |

Both cycles have visualConfirmed=true from the user's explicit visual checks, matching freeze/final/end sequences, destroyed=true and complete=true. Both Lua/native pairs and Python complete; worker errors are zero and both clients close. Earlier invisible/aborted variants are **not** completion evidence. Local Fixed and LocationBucketed variants were both reported visibly independent; this does not isolate one unique cause of the earlier invisibility.

**Visibility boundary:** transform/entity readbacks prove logical state, while visualConfirmed records the user's observation. The extra stone and rotation ring were seen; this is an opaque visual proxy, not verified transparency, selection behavior or saved scenery. Scale is fixed at one. No durable placement is inferred from InstantiatePrefab.

### Measured boundaries

| Measurement | Mean | P95 | Maximum |
| --- | ---: | ---: | ---: |
| Python update receipt → B pose-readback ACK receipt, 623 updates | 20.5641 ms | 34.1381 ms | 61.4005 ms |
| A diagnostic Advance callback | 0.012902 ms | — | 0.414800 ms |
| B diagnostic Advance callback | 0.030214 ms | — | 0.485500 ms |
| B SetTransform + readback section | 0.013823 ms | — | 0.064400 ms |

The first interval excludes A's input/sampling delay and Python receipt before the start, and ends at a readback acknowledgement rather than a presented frame. It is not full input-to-visible latency or directly comparable to old committed-action confirmations. Maximum observed Advance gaps were 269.8039 ms on A and 259.6835 ms on B; their cause is not established by these summaries. Fast callbacks do not prove absence of stutter.

## 107: supplied code, no reviewed runtime result

The next diagnostic sends independent preview streams in **both directions**, with external Python and own logging, without ACSEDebug. It is designed to test:

1. Simultaneous active A1/B1 preview streams with changing poses from each.
2. Ending A1 while B1 continues, restarting A2 while B1 is active, then ending/restarting B.
3. One remote root per client, own previews retained, generation/sequence/session/origin separation.
4. Duplicate pose rejection, old pose/end rejection while a newer ghost exists, own-echo suppression and cleanup.
5. Ongoing progress with timing output only at the end.

**Status: prepared/unverified.** No 107 completion, simultaneous visual independence, feedback safety or performance claim is made. Its planned latest-pose coalescing may skip intermediate preview samples; that policy is appropriate only to ephemeral visual state, not to the committed command history.

## Architecture consequences and remaining limits

**Derived:** maintain two distinct flows: immutable ordered committed actions with application proofs and recovery records, and disposable latest-pose previews with generations/sequences and explicit cleanup. A preview must never silently become a committed park object, create a save entry or publish itself as a local user action.

The local bridge now carries actual supported edits and recovery traffic, not just harmless messages. Still open: simultaneous conflicting edits to the **same** object; multiplayer Undo ownership; automatic durable metadata in a matching save; unknown/crash outcomes; remote authenticated transport; full host/join and park transfer; multiple resources, scale/properties/groups; preview disconnect cleanup and sustained load; crash-free game exit.

No released playable internet co-op, full simulation synchronization or general exactly-once crash guarantee is claimed.
