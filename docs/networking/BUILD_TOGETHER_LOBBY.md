# Build Together: private local lobby and coordinated park start

**Reviewed 2026-10-30. Verified with two actual clients on one Windows PC. Current tested UI/protocol: `LOBBY_ALPHA04_2`, layout `EN_STACKED2`. Internet joining is not implemented.**

[Status](../research/STATUS.md) · [119–130 evidence](../research/DIAGNOSTICS_119_130.md) · [Internet plan](INTERNET_PLAN.md)

## What ran successfully

The archived 085 menu proof has become an operational local lobby. Lua, the own DLL/logger and external Python survive the main-menu-to-park transition without a second native Begin or ACSEDebug dependency.

- Main-menu entry: **Build Together**, reused persistent menu/dialog work from 085.
- Two participants; **either A or B can create the lobby and become host**. A/B remain installation/transport roles, not permanent Host/Guest roles.
- Random 128-bit invitation, ten-minute validity, consumed by one valid join request; explicit host approval for one guest. Pending request expires after two minutes; five attempts per minute are allowed before rate limiting.
- Guest invitation entry, pending request, approve/reject, renewed invitation and ready/not-ready states.
- Guest DLC/ready/park/build messages are gated by admission. Host's own DLC manifest may be read before guest approval; guest's manifest is processed only after approval.
- After both are ready, the selected host starts the same tropical sandbox template on both clients. Both loaded-world acknowledgements and both catalogue-filter confirmations precede build release.
- Existing scenery/group synchronizer attaches to the same native worker/session. This loads a common template, **not a transferred arbitrary Host save**.

## Runtime evidence anchors

Raw logs and session identifiers stay private. Match each Python run with the native client SUMMARY session before comparing results; Python/state output is in the folder from which the companion was launched, which can be either installation.

| Tested run | Observed result |
| --- | --- |
| Private admission, `LOBBY_ALPHA03_1`, `Python-Lobby01.log` and A/B native pair | Two `INVALID_INVITE` denials (wrong and consumed code), one host rejection, fresh invitation and subsequent single-guest approval. Guest DLC follows APPROVED; both ready. Both BYE replies drained; all completion markers and state Completed true. |
| Reversed host, `LOBBY_ALPHA04_1`, Python/state in installation B | `HOST_GEWAEHLT B`; both clients report `HOST_ROLE B`. A requests and B approves; exactly one guest bound to A's verified local game process. Both ready, both BYE drained, all complete; no game changes/saves. |
| Earlier integrated park/build run, `LOBBY_ALPHA02_1` | Both template parks loaded; each inventory 7,263 entries, 5,282 shared permitted entries. Both filters/build barriers released. Two Creates and two Moves confirmed; matching final reports/no locks, all complete. |
| First private park/build run, `LOBBY_ALPHA03_1` | Admission and both load/filter/build barriers passed; two Creates and one Move settled. Owner stopped the games before finish: Completed false. This is useful operation evidence, not a successful final audit. |
| Latest corrected UI run, `LOBBY_ALPHA04_2` | A host/B guest; invitation, approval, guest DLC and both-ready confirmed; menu-only finish succeeds. A/B LuaCompleted and NativeCompleted true, PythonCompleted true, state Completed true, gameChanges/saveCalls zero. |

## UI layout, language and startup correction

The original standard dialog placed all host actions in a horizontal row and overflowed. A first scoped styling attempt through the game's separate Dialog view did not solve the owner's visible problem. The current lobby renders in its own main-menu view with game Dialog/Button/InputField components, injected scoped styling, left-aligned status rows and vertically stacked actions.

The corrected run measures the five-button pending Host view twice as `UI_LAYOUT|EN_STACKED2|ButtonsInside=true|buttons=5`. It also records three false samples during view/model transitions (two on A, one on B); later samples pass. **The owner visually accepted the buttons and reported no remaining visible problem.** Preserve the false samples as measurement caveats rather than claiming every frame passed. The check combines rendered button count with horizontal bounds; it is not whole-frame/vertical-clipping telemetry.

Game-facing lobby, invitation and park-preparation text is English. Host invitation field uses **Click here to show code**; guest uses **Paste invitation code here**. The checked package assets contain both conditional hints; literal rendered field text is not recorded in native logs, so visual language confirmation is distinct from completion evidence. Some historical diagnostic markers/Python backend progress remain German; they are not evidence of untranslated current game-facing controls.

The first new input-context startup failed with “Not ready to call this function yet.” Root cause: global `engine.whenReady` only established browser-binding readiness; `Input.createGlobalPlayerControlContext` calls the game's `Engine.isCoherentPlayer` before that UI module was ready. The fix imports `/js/common/core/Engine.js` as `GameEngine` and waits for **GameEngine.whenReady**, with controlled rejection handling. No DLL or game-executable change was required.

Offline regression coverage now deliberately separates early native readiness from later game-UI readiness: zero input contexts before the latter, exactly one after it. Actual corrected menu startup and the completed owner run provide the separate runtime confirmation. Other tests cover stale model/action IDs, invitation submit/cancel ordering, input-context activation/release, ESC/Close action routing, menu retention and stopping the UI without restarting the DLL. Mock tests do not replace rendered-game evidence.

Own source anchors: `pc2cooplobbyruntime.lua` (`R.Buttons`, `R.Rows`, `R.UIKey`, admission handlers), `pc2cooplobbymenu02.lua` (`updateDialog`, Select/Layout listeners), `Menu.js` (`onControl`, GameEngine readiness), `LobbyPanel.js` (`parsePanel`, `installPanelStyle`, bounds report), `PrivateInvite.js` (`render` copy/join branch), `private_lobby.py` (`issue_invite`, `receive`, `member`), `peer_identity.py` (`verify_peer`) and `park_protocol.py` (`receive`, `activate`). Source files remain in the private development workspace; no game UI modules are redistributed here.

## Security and lifecycle boundary

The local pipe checks the actual Windows client PID and expected game executable path. Invitation summaries/logs omit the secret; pending consent is bound to a concrete request and local peer. Old approvals do not authorize replacement requests. These checks establish tested local admission, **not verified Steam friend identity or internet authentication**.

Menu finish requires both approved participants ready. Both native workers must read BYE before Python tears down their pipes; completion is not inferred from an overlapped write alone. `FlushFileBuffers` is performed on the I/O worker outside the shared lobby lock. Closing the games before finish is an interrupted test, not a failure of the earlier admission steps.

Recent lobby/UI tests do not save a park. Host-controlled durable saving, late join, arbitrary park transfer, public release packaging and a friend on a second PC remain separate work.
