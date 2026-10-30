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

Current review: 2026-10-30. Read STATUS, DIAGNOSTICS_119_130 and BUILD_TOGETHER_LOBBY before historical pending statements. 119–121 controlled lease-holder/Python/combined restart cases passed matching runs; 122/123 resources/properties; 124–128 groups/grids/manual Merge and history; specific 129 parallel/conflict/history stages passed, while retained early 129-Free failed; final 130 mixed run passed 43 commands. Private Build Together local lobby now supports either host, one guest, invitation/rejection/approval, guest DLC after consent, readiness and common-template park start. Current game-facing UI is English/stacked and owner-accepted; three false layout transition measurements remain qualified. Corrected input initialization waits for game Engine.whenReady. ACSE remains loader, ACSEDebug absent. No two-PC/WAN runtime evidence: next work is portable, authenticated direct TCP/TLS with both IPv4 and IPv6; optional future relay, no VPN app for the first test. Do not equate local PID checks with remote identity, global engine readiness with game UI readiness, template loading with park transfer, local polls with WAN messages, undo checkpoints with saves or controlled recovery with arbitrary-crash exactly-once. Prioritize private local state, traceable evidence and an honest unimplemented internet boundary.

## Notes and contribution workflow

Write dated findings in `docs/research/LOG.md`. Update the evidence table and unknown list immediately. Do not treat the public Co-op Anything hub as a place to upload the game's source; share concise independently verified findings and original mod code in the game's own repository.
