# Diagnostics 107–119: independent previews, shared editing and lock recovery

> Historical cutoff: 2026-10-26. The 119-prepared statements below describe that date; corrected 119–130 results and the private lobby are now recorded in [119–130](DIAGNOSTICS_119_130.md) and [Build Together](../networking/BUILD_TOGETHER_LOBBY.md).

**Reviewed 2026-10-26.** Runtime evidence reaches 118. **119 is prepared only; no code or runtime result is certified here.**

[Current status](STATUS.md) · [Earlier ledger](DIAGNOSTICS_085_107.md) · [Native bridge](../networking/NATIVE_BRIDGE.md) · [Recovery](../networking/RECOVERY_AND_HISTORY.md)

## Evidence boundary and setup

**Verified in running games:** owner-run diagnostics with two actual local PC2 clients in separate Sandboxie boxes, own build-profiled x64 DLL/logger, separate Named Pipes and Python outside the sandboxes. ACSE remains the loader; ACSEDebug is not the diagnostic foundation. Established setup: PC2 1.11.4.1011357 / ACSE 0.729. This does not certify other executable builds.

Private evidence consists of the named Python run and matching role-labelled native files below. Session equality, counters, world/readback checks and terminal markers were reviewed; raw logs, sessions, private paths, binaries and extracted game code are not published. Passing runs below have both Lua/native pairs complete, Python complete and no reported worker errors. 116 is explicitly an incomplete run.

The scenery resource is AQ_Rock_04, scale one. These are finite local diagnostic proofs, not a release, WAN test or full simulation synchronization. No park save was requested in 107–118. A diagnostic checkpoint call is not a disk park save.

## 107 — simultaneous bidirectional visual previews: passed, corrected repeat

**Private anchors:** Python107Test2.log; Native107-43736Test2.log; Native107-21488Guest2.log. Build 107LIVE1.

Two generations per origin were displayed independently. Overlap windows A1/B1, A2/B1 and A2/B2 all contain changing poses from both sources and owner visual confirmations in both directions. Ending one stream did not stop the continuing peer stream.

- A→B: 1,014 applied updates; B→A: 1,372.
- Each client created and removed two remote roots, rejected six duplicate/old updates or ends, and skipped two own echoes.
- Own-preview checks: 11,761 on A / 14,879 on B; own movements: 1,861 / 3,528.
- No committed game action was requested. A rock/ring proxy is an ephemeral visualization, not a durable placement or transparency proof.

This supersedes the earlier prepared/unverified status for 107. Initial failed runs are not the completion evidence.

## 108 — remote Create during own preview: passed

**Private anchors:** Python108.log; Native108-44224.log; Native108-25508Guest.log. Build 108TOK1.

Each direction captured one manual placement and committed one remote object while the receiver retained its distinct, uncommitted own placement preview. Remote work used a separate native preview token. Each client skipped two duplicate Creates and one own echo.

After the receiver cancelled its own preview, that preview part was absent and the remote committed object remained. Source and receiver logical/local mappings were checked. This tests independent commit ownership; live ghost streaming was explicitly not tested here.

**Observed boundary:** separate preview tokens work for these supported operations. This does not certify arbitrary overlapping editor tools or identical native undo stacks.

## 109 — overlapping remote Create application: passed with qualified overlap

**Private anchors:** Python109.log; Native109-30156.log; Native109-7124Guest.log. Build 109SIM1.

Both directions were released together after preparing the manual placements. Each client retained one local and one remote committed object, two duplicate skips and one own echo; both objects survived own-preview cancellation.

Same-Windows-host DLL QueryPerformanceCounter intervals establish about **51.12 ms remote application overlap** and **10.33 ms remote commit overlap**. The captured local manual commit intervals did **not** overlap (about 2.46 seconds apart). ApplicationOverlapProven=true must not be described as simultaneous manual input.

## 110 — combine live previews and manual placements: passed in Test 4

**Private anchors:** Python110Test4.log; Native110-24880Test4.log; Native110-15552Guest4.log. Build 110LIVE1.

Each client performed two local placements and two remote commits, ending with four registered test objects. Each skipped four duplicate Creates and five own echoes. Three remote roots per client were created and destroyed; zero ghosts remained.

The matching remote ghost was removed when a committed object replaced its visual role. Later old updates/ends did not recreate or remove the wrong generation. Own previews remained uncommitted and movable during remote application; cancellation retained committed objects.

Python reported about 170.80–240.03 ms from confirmed Create receipt to verified receiver ACK. Manual/remote/commit intervals did not overlap between directions in this run. Earlier failed Python/test revisions are superseded by Test 4, not erased from history.

## 111 — real overlap using automatically triggered prepared placements: passed

**Private anchors:** Python111.log; Native111-44612.log; Native111-43704Guest.log. Builds 111OVER1 / behavior 111AUTO1.

One operator cannot click both windows simultaneously. Both clients therefore prepared ordinary placements, then automatically confirmed through SubModePlacement._DoConfirm on a coordinated future same-host clock target.

- Four local placements and four remote commits per client; eight registered committed objects each.
- Eight duplicate Creates and nine own echoes skipped per client.
- Five remote roots created/destroyed per client; zero remaining ghosts.
- Actual local commit intervals overlapped in **three of four rounds**; remote application and remote commit intervals overlapped in **all four**.
- Source/remote live previews, post-result own-preview movement and cancellation checks passed.

The legacy counter name manualCommits includes these automatically triggered confirmations. This is real measured overlap of the tested paths, not proof that two humans clicked at the same instant. The overlap clock assumes both clients share one Windows host.

## 112 — confirmed manual Moves during receiver placement preview: passed

**Private anchors:** Python112.log; Native112-23356.log; Native112-30728Guest.log. Build 112MOVE1.

Each origin performed two manual Moves and each receiver applied two Moves to its existing mapped part. No Move path created a new part. Per client: five duplicate skips including an old first Move replayed after the second, two own echoes and one own-preview cancellation proof. Final object versions were two.

Own placement previews remained active and movable. Cancelling them did not revert committed remote positions. This is confirmed Move replication, not continuous drag streaming.

## 113 — live drag, commit and cancel in both directions: passed, Test 3

**Private anchors:** Python113Test3.log; Native113-13040Test3.log; Native113-46452Guest3.log. Build 113LIVE1.

Four cycles completed: A commit, A cancel, B commit, B cancel. Applied live updates by cycle were **198 / 368 / 221 / 165**. The receiver edited the existing mapped part with an independent preview token; MoveCreateCalls=0.

Each client recorded one local and one remote commit, one local and one remote cancellation, two remote edit sessions, twelve rejected duplicate/old packets and six skipped own echoes. Final object versions were one. Cancels restored the baseline instead of committing a displaced pose. Protected own previews survived and could still move; their later cancellation left committed test objects intact.

Python pose-receipt→receiver-readback-ACK means were approximately 33.1–34.4 ms across cycles, with maximum about 115.2 ms. Source sampling was 100 ms and lies outside that interval. A field labelled presented-readback is an API/readback proof, not a captured displayed frame.

Earlier runs ended prematurely or violated the test's confirmation gate. Test 3 waited for the Python prompts and completed all four cycles; do not infer a native Commit/Cancel failure from the superseded runs.

## 114 — shortened Delete with receiver own preview: passed

**Private anchors:** Python114.log; Native114-47988.log; Native114-43280Guest.log. Build 114DELETE1.

Source absence on A was confirmed before forwarding Delete. B used exactly one edit, one destroy and one commit. Two duplicates were skipped, and A skipped its own echo. The control part remained unchanged.

B retained its own placement preview across 3,485 checks and 1,032 movements. After ESC the preview was absent, the deleted target remained absent and the control remained. The shortened runtime test covers **A→B**, not a second reverse-direction Delete cycle.

Initial defects were diagnostic framing/transform construction errors. Idle transport replies must be the single byte W expected by the native filter; game transforms must use the verified PC2 constructors. The corrected run, not the initial park-load failure, is the completion evidence.

## 115 — manual Undo/Redo with receiver own preview: passed

**Private anchors:** Python115.log; Native115-44796.log; Native115-12888Guest.log. Build 115HISTORY1.

Nine A-origin steps: Create, Undo Create, Redo Create, Move, Undo Move, Redo Move, Delete, Undo Delete, Redo Delete.

B applied nine explicit counteractions: three creates, six edits, three destroys, six transforms and nine commits. Recreated local parts were remapped; logical identity stayed stable. Ten duplicate skips include an old Create replay after final Delete; it did not resurrect the object. A skipped nine own echoes.

B's own placement preview survived 17,324 checks and 2,515 movements, with a movement proof after every result and final cancellation proof. Both logical versions reached nine. **Receiver native undo history was not used or certified**; source manual native Undo/Redo and receiver counteractions are different mechanisms.

## 116 — free editing: useful partial evidence, not a completion pass

**Private anchors:** Python116.log; Native116-10656.log; Native116-47044Guest.log. Build 116FREE1.

Both clients connected after correcting the per-endpoint Sandboxie rules. Before termination, 101 commands applied, 101 duplicates and 101 own echoes were skipped. The covered actions were Create, Move, Undo Create and Redo Create; not all proposed history/Delete cases ran.

Trying to edit a peer-created object triggered the diagnostic's own-object restriction. Both clients/Python ended incomplete. This identified the next ownership requirement; it is not an unexplained transport failure or Completed=true result. No final register audit passed in this run.

## 117 — shared-object Move/Delete and conflicts: passed, Test 5

**Private anchors:** Python117Test5.log; Native117-48140Test5.log; Native117-31548Test5.log. Lua build 117LOCK1; reused transport/footer labels remain 116.

Creator, current actor and local part identity are distinct. Each client successfully moved and deleted an object created by the other. Python granted versioned per-object leases before mutation; conflicting Move and Delete requests were rejected with LOCKED before any game operation.

- Eleven applied commands, thirteen duplicate skips and eleven own-echo skips.
- Two conflicts confirmed without game operations; one verified ESC Move cancellation and subsequent release.
- Both final registries matched canonical state: five logical records, two live and three tombstones; no open locks.
- Old Creates from both origins were skipped after deletion.
- Seven old-release-against-new-lease and eleven stale-version checks are **server protocol probes**, not extra in-game conflict demonstrations.
- Remote application during own placement previews was recorded for Create/Move/Delete on A and Move/Delete on B.

**Important correction:** the standalone object popup's selected part must be resolved through InfoPopUpComponent:GetOpenPopUp() and its partID/entityID mapping. The generic current mode lacked GetEditorContext in this path; using it had prevented all Move requests before lock acquisition. The corrected resolver restored actual Moves.

The final successful run explicitly started finalization with Enter. Earlier status-only or early-exit runs are not final completion evidence. Lock-aware per-actor history remains a limited diagnostic policy, not a finished collaborative Undo UX.

## 118 — pipe loss while locked and after application: passed

**Private anchors:** Python118.log; Native118-39040.log; Native118-6804Guest.log. Build 118RESUME1.

### Case 1: disconnect while A holds an unconfirmed Move

Python processed OPEN, retained L1 and dropped A's transport response. B attempted the same Move and received UNCERTAIN without a game operation. A reconnected with the same session/lease; its pending OPEN request was replayed without repeating application processing. After ESC, the baseline was verified and L1 released.

### Case 2: disconnect after B applies but before its ACK is accepted

A committed one new Move. B applied it once. Python discarded B's first application ACK, closed B's pipe and withheld reconnect completion for two seconds. The DLL retained the pending request and retried it after connection recovery. An additional identical Move command was delivered.

B did not repeat the edit/transform/commit; it acknowledged again and skipped the duplicate. L2 was released after the required effect proofs. B's independent own preview survived and remained movable.

| Final observation | A | B |
| --- | ---: | ---: |
| Successful connections / disconnects | 2 / 1 | 2 / 1 |
| State reconciliations, including initial | 2 | 2 |
| Local / remote Move commits | 1 / 0 | 0 / 1 |
| Cancelled Moves | 1 | 0 |
| Application duplicate skips / own echoes | 0 / 1 | 1 / 0 |
| Advances counted while locally offline | 1,059 | 89 |
| Protected own-preview checks / movements | 0 / 0 | 1,712 / 89 |

Both ended at the same transform/version one, activeLease=null and no quarantined clients. Two ACK attempts were recorded. Both native workers reported workerError=0 and all completion markers were true.

The Advances-during-outage counter follows each client's Lua online/reconciliation state; it is not a precise stopwatch for the server's complete outage interval. Both game processes and Python stayed alive: this is **pipe recovery with in-memory state**, not client or server restart.

## 119 — prepared: restart the client holding a lease

**No runtime result, implementation certification or park-save authorization yet.**

Proposed shortened scenario: keep A/Python running, let B hold an unconfirmed Move, stop B, deny A's conflicting edit while the outcome is unresolved, reload B from an explicit matching baseline, rebuild local mappings/status, verify the unconfirmed Move was not committed, invalidate the old lease and permit a new operation under a fresh lease identifier. Replay old command/lease messages and verify no second action or stale unlock.

A reproducible implementation is expected to need one newly saved local B baseline **before** opening the Move, subject to explicit owner authorization. Do not reuse an old native preview token across processes. Old local Part-/Entity-IDs require validation/remapping against the loaded world. Restoration of the interactive drag itself is not required for the first proof.

## Derived architecture and limits

- Retain immutable committed command identity, payload, revision, processing outcome and tombstones separately from coalescible preview streams.
- Separate native preview tokens isolate the tested supported remote changes from the local placement preview. Ghost rendering alone is not commit authority.
- Grant an object lease before native mutation; bind it to logical object/version/actor. An old release must not release a newer lease.
- Treat disconnect during a held edit as uncertain until reconciliation; timeout alone is not proof of rollback.
- Retrying transport or application ACKs must not trigger another game action when a verified outcome already exists.
- Game-thread Lua owns game operations. Workers transfer copied data and write logs.
- Still unknown: atomic native commit/status/save persistence, arbitrary crash outcomes, reconnecting a dead lease holder, general collaborative Undo rebasing, authenticated two-computer transport, safe resource/property/group coverage and production lifecycle/backpressure behavior.

No distributed exactly-once guarantee, persistent ghost placement, finished lobby, released internet alpha or synchronized full park simulation follows from these local tests.
