# Scenery co-op prototype: completed gates and next work

**Updated 2026-10-26.** [Status](../research/STATUS.md) · [107–119 ledger](../research/DIAGNOSTICS_107_119.md)

## Achieved within local diagnostic scope

Own DLL/Named Pipes/external Python carry supported manual Create/Move/Delete and history effects without ACSEDebug. 095–102 establish specific recovery/catch-up paths; 107 bidirectional live visual previews; 108–111 separate-token remote placement while own previews stay active, including measured overlap; 112–115 Move/live-drag/cancel/Delete/history under preview protection; 117 shared-object leases/conflicts and matching final registries; 118 held-edit/lost-ACK pipe recovery without duplicate effects.

111 uses automatically confirmed prepared placements; three of four local commit rounds overlap. 116 is an incomplete own-object-restriction run, superseded in shared-object scope by 117. 085 remains an archived local UI proof.

These are owner-run local diagnostic gates. ACSE remains the loader, the native ABI is executable-profile-specific, and no released internet alpha is claimed.

## Next acceptance gates

1. **119, prepared only:** restart the client holding a lease, reconcile a matching saved baseline and command/object state, retire stale authority and prove a fresh operation plus late-message rejection. Save authorization is a separate prerequisite; no 119 park save has occurred.
2. Authenticated/encrypted companion communication on two computers, reconnect/backpressure/admission tests.
3. Durable save/registry/status/tombstone integration and reconciliation of uncertain native commit outcomes; mismatched-save repair and late join.
4. Collaborative Undo policy, revision changes by other actors, broader resources/scale/properties/groups and supported tool coverage.
5. Host/join/baseline transfer/load/save workflow; finalize 085 menu integration after architecture decisions.
6. Reproducible packaging, automated regressions, long soaks, presented-frame profiling and exit-crash isolation.

## Evidence rules

Require matching participant runs, world checks and measured overlap intervals; completion labels alone are insufficient. Preserve historical failures as dated evidence.

Committed actions remain lossless, immutable and ordered; disposable preview poses may coalesce. A worker never invokes Lua/game APIs. Native tokens/local IDs are not cross-process network identities. No persistent-placement claim follows from InstantiatePrefab and no arbitrary-crash guarantee follows from completed checkpoints or live-process pipe recovery.
