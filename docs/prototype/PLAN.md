# Scenery co-op prototype: completed gates and next work

**Updated 2026-10-25.** [Status](../research/STATUS.md) · [085–107 ledger](../research/DIAGNOSTICS_085_107.md)

## Achieved within local diagnostic scope

Own DLL/Named Pipes/external Python carry manual Create/Move/Delete and live-session Undo/Redo without ACSEDebug. Lost confirmations, pipe breaks, companion restarts and controlled saved-Guest catch-up pass. Separate objects can originate from either client with tested duplicate/echo suppression. 102 demonstrates actual overlapping catch-up; 105 achieves final convergence but only partial phase overlap.

106 adds an independent A-to-B visual rock/ring while B moves its own preview. This is ephemeral rendering, not a durable park commit. 085 supplies a deferred local menu/dialog proof.

These are owner-run diagnostic gates, not a shipped multiplayer mod. The native interface is build-profile specific; remote security, conflict ownership, automatic persistence and full simulation remain open.

## Next acceptance gates

1. **107, prepared/unverified:** simultaneous A↔B previews with two generations each, one ghost per receiver, continuous independent own previews, stale/duplicate/echo rejection and verified cleanup.
2. Remote committed edits while the recipient's ordinary preview remains active: prove safe completion or a clear bounded defer policy. Do not confuse ghost rendering with a solved shared undo-preview path.
3. Same-object conflicts, origin authority/revisions and multiplayer Undo ownership.
4. Authenticated remote companion connection across two computers, failure/backpressure checks and reproducible install/start/stop.
5. Matching save + durable registry/status/tombstone recovery, including uncertain commit outcomes and repair.
6. Host/join admission, baseline transfer and Host-controlled save UX; revisit the archived 085 UI after these decisions.
7. Broader resources/properties, soak/GC tests, actual rendered-frame measurements and isolated exit-crash diagnosis.

## Evidence rules

Require matching sessions and all participant completions; inspect counters and world checks rather than completion labels alone. 087's retained mismatched result pair is not certified. 101's completion is not overlap; 105's completion is not all-phase overlap.

Keep committed commands lossless and ordered; previews may coalesce to the latest valid pose. A worker never invokes Lua/game APIs. No persistent-placement claim follows from InstantiatePrefab, and no arbitrary-crash exactly-once claim follows from controlled checkpoint tests.

No released playable internet co-op or full-park simulation is claimed.
