# Open questions and next experiments

**Updated 2026-10-25.** [Status](STATUS.md) · [085–107 evidence](DIAGNOSTICS_085_107.md)

## Immediate: bidirectional previews and editor coexistence

1. Execute **107**, whose code was supplied but has no reviewed run. Both clients must move their own preview while displaying one independent peer ghost, stop/restart separately, reject old updates/end messages without destroying a newer ghost, and reject own echoes.
2. Test disconnect/world-change cleanup, frozen peers, bounded queues and long preview sessions.
3. Resolve the separate **committed-action** problem: 105's B-origin Create waited about 17.79 seconds for acknowledgement while a local preview was active. 106's independent render proxy does not make shared undo-preview commits concurrently safe.
4. Extend resource/rotation/scale/property coverage, transparency and nonselectable visualization. Measure actual input-to-presented-frame latency separately from readback ACKs.

## Ownership and supported editing

103/104 establish reverse and bidirectional edits to separate logical objects. Still open: simultaneous conflicting edits to the same object, authoritative acceptance/stale revisions, multiplayer Undo ownership, repeated/cancelled placements, groups and dependent objects. Preserve local-part/logical-ID separation and remote-capture suppression.

## Remote transport and product workflow

- Implement authenticated/encrypted companion networking and test two computers. Local Named Pipes are not a WAN link.
- The intended UX remains Host session → Guest join → compatible world loading → Host-controlled saving. Independent park loading is diagnostic scaffolding.
- 085 proves a local main-menu entry/dialog, not a lobby or park transfer. It is intentionally deferred until architecture decisions settle.
- Baseline transfer/verification, admission, packaging, account/service behavior and save isolation remain separate tests.

## Recovery and lifecycle

095–102 establish specific lost-ACK, pipe-break, Python-restart and completed-checkpoint workflows. Still open: native commit/status/ACK/save atomicity, unknown outcomes after arbitrary crashes, mismatched saves, automatic metadata persistence, repair, late join and history retention/compaction.

The recurring game-exit crash reporter remains unisolated. Compare clean/no-mod, ACSE-only and own-DLL lifecycle controls before assigning a cause. The own logger cannot capture every pre-load failure or replace native crash dumps.

## Performance and evidence quality

- 102 proves actual catch-up overlap; 101 did not. 105 proves only partial phase overlap despite successful synchronization.
- Retained 087 native/Python files disagree on connection/completion; obtain a matched corrected run before certifying it or explaining the earlier 657-ms gap.
- 106's approximately 270/260-ms maximum Advance gaps remain unattributed; callback cost is a different measurement.
- Broaden realistic parks, sustained traffic, GC/allocation profiling and presented-frame measurements.
- Synthetic 100,000-entry registry tests do not establish 100,000 real objects.

Kepler's internal pacing remains hypothetical, but the own bridge now has direct game-effect/recovery evidence. General exactly-once crash guarantees, a released internet mod and full simulation synchronization are not established.
