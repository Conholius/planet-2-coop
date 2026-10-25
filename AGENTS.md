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

Reviewed retained evidence now extends through 106 (2026-10-25); 107 code is supplied but untested. Read docs/research/DIAGNOSTICS_085_107.md and current STATUS before historical next-step statements. Own profiled DLL/Named Pipes/external Python and own logger operate without ACSEDebug; ACSE remains the loader. 091–094 pass manual scenery/history effects; 095–102 controlled recovery/catch-up; 103/104 reverse and separate-object bidirectional edits; 105 converges with only partial overlap and an unresolved local-preview/remote-commit interaction. 106LIVE2 passes independent A-to-B visual previews while B keeps its own preview active; 107 bidirectional visual behavior is unverified. 085 proves local menu/dialog integration, not a real lobby. Retained 087 native/Python files are not a matched completion pass. Keep immutable committed commands separate from coalescible ephemeral preview poses. Do not infer durable placement from prefab rendering, whole-frame latency from readbacks, WAN capability from local pipes, or arbitrary-crash safety from completed checkpoints. Priorities: 107, editor coexistence/conflict authority, authenticated remote transport, durable recovery and product workflow. The reported exit crash remains unisolated.

## Notes and contribution workflow

Write dated findings in `docs/research/LOG.md`. Update the evidence table and unknown list immediately. Do not treat the public Co-op Anything hub as a place to upload the game's source; share concise independently verified findings and original mod code in the game's own repository.
