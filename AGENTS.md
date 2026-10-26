# Agent instructions — Planet Coaster 2 co-op

Before working, read `README.md`, `docs/README.md`, `docs/research/STATUS.md`, `docs/testing/RUNTIME_TESTS.md`, `docs/research/EVIDENCE.md`, and `docs/research/OPEN_QUESTIONS.md`, then the relevant subsystem document. The chronological `LOG.md` retains superseded failures; do not promote them back into the current status. Also read the upstream [Co-op Anything AGENTS.md](https://github.com/cranebeaker/coop-anything/blob/main/AGENTS.md), and follow its applicable safety, ownership and QA rules.

## Non-negotiable evidence rules

1. Separate **Observed in extracted material**, **Derived**, **Hypothesis**, **Unknown**, and **Verified in a running game**. Static API names and readable decompiled Lua do **not** count as runtime confirmation.
2. Identify the exact source file, build/version (if known), symbol, and relevant line/function for each technical claim. Do not transfer engine details between Frontier games without PC2 confirmation.
3. Decompiled Lua can contain reconstruction bugs even if it parses. Check assembly/bytecode for important decisions and report discrepancies.
4. Never claim that `InstantiatePrefab` creates a persistent park placement without a save/reload test.
5. Distinguish `EntityID`, `PlacementID`, `PlacementPartID`, `SaveEntityID` and any mod-defined network ID. Do not treat them as interchangeable.
6. Respect prefab-local versus world-space transforms.
7. Do not redistribute raw game binaries, extracted resources, OVL/OVS archives, assets, or whole decompiled scripts here; `local/` is ignored. Keep credentials and personally identifying paths out of commits and logs.
8. Obtain owner approval before touching installations or saves, accessing accounts, installing tools, publishing material or initiating external contact. Use copies and backups; test on isolated profiles.
9. For any claim of working co-op, require two actual game clients and recorded reproducible test steps; label untested otherwise.
10. Preserve this project's research notes incrementally and reconcile contradictions before implementing.

## First engineering objective

Reviewed runtime evidence reaches 118 (2026-10-26); 119 is prepared only, with no code/run certification or save authorization. Read docs/research/DIAGNOSTICS_107_119.md and current STATUS before historical next-step statements. Own profiled DLL/Named Pipes/external Python/logger work without ACSEDebug; ACSE remains the loader. 107 passes bidirectional visual previews; 108–111 separate-token commits during own previews; 111 proves coordinated automatic local overlap in three of four rounds, remote overlap in all four. 112–115 cover confirmed/live Move, cancel, shortened A-to-B Delete and manual source history with explicit receiver counteractions. 116 is incomplete due to its own-object restriction; 117 Test 5 proves cross-creator editing, Move/Delete conflict rejection, ESC release, matching registries and no open locks. 118 proves two controlled live-process pipe recoveries with leases, pending requests and application status retained; it is not a game-process restart. Creator/actor/local native identity are distinct. Retained 087 files are not a matched completion pass. Keep committed commands immutable and previews coalescible; never reuse native preview tokens across processes or infer arbitrary-crash exactly-once from controlled tests. Priorities: 119 lease-holder restart, durable metadata/reconciliation, secured two-computer transport, product workflow and exit-crash isolation.

## Notes and contribution workflow

Write dated findings in `docs/research/LOG.md`. Update the evidence table and unknown list immediately. Do not treat the public Co-op Anything hub as a place to upload the game's source; share concise independently verified findings and original mod code in the game's own repository.
