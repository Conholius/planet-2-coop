# Current research status

**Reviewed 2026-10-30. Local supported-scenery/group prototype and private Build Together lobby verified on two actual clients. Two-PC internet transport is planned, not implemented.**

[Overview](../../README.md) · [119–130 ledger](DIAGNOSTICS_119_130.md) · [Lobby evidence](../networking/BUILD_TOGETHER_LOBBY.md) · [Internet plan](../networking/INTERNET_PLAN.md)

## Verified in running games

- Own build-profiled DLL, direct strings, own logger and bounded asynchronous local pipes work without ACSEDebug; ACSE remains the loader. Earlier 091–118 results retain their diagnostic-specific scope.
- Corrected 119 restores a restarted lease holder from an existing matching checkpoint, restores two command records, rejects old authority and applies only the new remote Move. 120 recovers two Python restarts; 121 recovers a combined Guest/Python restart and retires the dead incarnation. All matched participants/supervisors complete. No arbitrary crash/commit/save atomicity follows.
- 122 supports multiple tested resources. Final 123 transfers actual scale and semantic RGB changes, preserves scale during remote Move, and corrects reset-to-default with separate empty-channel handling and strict named-channel checks.
- 124/125 establish grid walls/groups and whole-group movement/rotation. 126 verifies Split and a Python-triggered join with actual editor grids; 127 adds actual UI-driven Merge. 128 Test 5 completes source Split/Merge Undo/Redo and full editor-grid restoration after initialized-editor waits.
- 129 completed parallel, Split/Merge, concurrent-conflict and history stages. Retained early State129-Free is failed, not a completed free-building run. Later completed 130 supplies mixed/new-wall building evidence.
- Final 130: 43 settled commands (A38/B5), 86 duplicate records, no open locks/errors, both Lua/native pairs and Python/state complete. Mixed loose scenery/grid groups, supported own history, shared catalogue: 7,263 entries each, 5,282 jointly permitted.
- Build Together provides private one-guest invitations, pending requests, reject/approve and readiness. Both A-host/B-guest and B-host/A-guest have completed matched local lobby runs. Guest DLC follows approval.
- Common tropical-template load, both loaded acknowledgements, both catalogue filters and build release have runtime evidence; earlier integrated run also completes two Creates/two Moves. This is not arbitrary park transfer.
- Current English in-menu UI uses stacked actions and waits for GameEngine.whenReady before creating its input context. The five-button Host view passes measured horizontal bounds; the owner visually accepts it. Latest menu-only run completes everywhere, with no game changes or saves.

## Evidence and measurement limits

See the ledgers for corrected-run anchors. Later failed development files do not negate earlier matched successful scope, and earlier success does not certify every later revision. The retained 087 mismatch and earlier incomplete 116 remain qualified.

Three false layout samples occurred at model/view transitions; later samples pass. The bounds check combines button count and horizontal rectangles, not every-frame/vertical/rendered-latency proof. English assets contain the correct Host/Guest code hints, but logs do not transcribe visible labels. Owner visual observations are separate evidence.

Callback time, Advance scheduling gaps, initialization, native worker exchange, native completion/readback and end-to-end confirmation are distinct. Restart/outage intervals must not be reported as normal packet latency. These measurements are on one host; none establishes WAN performance or whole-simulation synchronization.

## Derived architecture

Keep commands immutable, ordered and outcome-tracked; retain logical IDs, revisions and tombstones. Coalesce only disposable previews. Native tokens/Part-/Entity-IDs stay local. Acquire all affected group leases before changes; stale releases cannot unlock fresh authority. Separate remote commit completion and its undo checkpoint; a checkpoint is not a park save. Restore the complete initialized editor grid after group reconstruction.

Local invitation admission binds a process-checked pipe peer to host consent. It does not verify a remote Steam friend. Visible DLC assets are not proof of entitlement; shared catalogue checks gate supported operations.

## Next work — prepared only

1. Direct companion-to-companion TCP/TLS across two PCs, supporting IPv4 and IPv6 without a VPN app for the first test. Preserve the proven local DLL/pipe boundary and selectable host.
2. Extend invitations with endpoint/server identity; define certificate trust, local-to-room sessions, bounded async queues/fragments, remote peer identity and disconnect behavior.
3. Produce a portable original-code package without developer paths or archived-diagnostic dependency chains. Match supported game/DLL/mod versions on both PCs.
4. Prove actual internet admission, common template load and bidirectional building, then controlled disconnect handling. IPv4 and IPv6 need separate route evidence; no universal reachability is promised.
5. Later optional relay fallback for inaccessible NAT combinations; durable host saves/metadata, arbitrary-crash reconciliation, late join, collaborative history rebasing, expanded editor coverage, soak/frame QA and exit-crash isolation.

No internet implementation, router/firewall change or park save was performed during this documentation update.
