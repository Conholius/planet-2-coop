# Proposed internet transport: direct IPv4/IPv6 Build Together

**Decision recorded 2026-10-30. Preparation only: no internet transport has been implemented or tested with a second PC.** The owner chose direct connection without a VPN application and requires both IPv4 and IPv6 support.

[Verified local lobby](BUILD_TOGETHER_LOBBY.md) · [Native bridge](NATIVE_BRIDGE.md) · [Open questions](../research/OPEN_QUESTIONS.md)

## Keep the proven local boundary

~~~mermaid
flowchart LR
    GA["PC 1: Game Lua + own DLL"] <--> PA["PC 1: local Named Pipe + Python"]
    PA <-->|"Proposed persistent TCP + TLS"| PB["PC 2: Python + local Named Pipe"]
    PB <--> GB["PC 2: own DLL + Game Lua"]
~~~

Named Pipes remain local, including `PIPE_REJECT_REMOTE_CLIENTS`; do not expose Windows pipe/SMB access across the internet. Each Python process validates its own local game endpoint. The selected host's companion owns authoritative room admission, command ordering, group/object leases and accepted outcomes. The other companion routes its local client's traffic to that authority.

The native DLL can probably remain unchanged because sockets live in Python; that is an architectural inference, not a cross-PC compatibility result. Lua/runtime and invitation/bootstrap changes are still needed. A/B transport roles must be configured or assigned consistently across PCs and kept separate from the selectable Host/Guest roles.

## Required engineering changes

1. **Dual-stack endpoints.** Accept hostnames, IPv4 and bracketed IPv6 addresses with bounded parsing. Resolve and attempt available compatible endpoints; listeners must support the available families explicitly. A silent fallback to an insecure protocol is not an endpoint fallback.
2. **Encrypted, authenticated connection.** Persistent TCP with TLS and a checked server identity/certificate, then one-time admission and host consent. Choose and test the certificate/trust bootstrap before implementation; never assume encryption without peer verification proves the intended host. Python provides the needed client/server SSL contexts ([official Python 3.11 documentation](https://docs.python.org/3.11/library/ssl.html)).
3. **Reachable invitations.** The old 32-hex-character code proves access to a local lobby but contains no route to another PC. A direct invitation must carry a versioned endpoint/port, room/server identity and one-time secret, with an explicit size/expiry bound. Extend the UI's current 64-character entry limit accordingly. A short lookup-only room code would require a separate rendezvous service, which is not currently present.
4. **Remote identity.** Keep PID/image checks local. Bind the remote guest to the authenticated room/connection identity; a claimed Windows PID or A/B role is not remote authentication. Preserve one guest, pending request identity, stale-consent rejection, rate limits and pre-admission DLC/build gates.
5. **Asynchronous routing.** Do not turn each fast local pipe poll into a WAN round trip. Respond locally from bounded queues, push network messages asynchronously and distinguish local transport acceptance from verified native application. Preserve immutable commands, duplicate/outcome records, ordering and tombstones. Disposable preview poses may coalesce; committed edits may not.
6. **Sessions and framing.** A local game already gets a session when its DLL connects, before an invitation is entered. Define the local-to-room binding explicitly; do not simply replace a live session ID or trust matching independent sessions. Existing 4,096-byte native frames and bounded logical messages up to 65,536 bytes include `F_BIG` fragmentation with an embedded session inside the encoded body. Translation/reassembly must validate both outer and inner envelopes, sequence and size rather than blindly forwarding/replacing text.
7. **Disconnect policy.** Stop accepting unsafe new edits while authority/outcomes are uncertain; reconcile epochs, leases and verified command status before resuming. Existing controlled local recovery results do not certify a new WAN gateway. Initial fail-closed behavior is preferable to promising automatic recovery without evidence.
8. **Portable package.** Remove developer-specific Python launcher/game paths and implicit dependencies on archived diagnostic directories. Include only the required original mod/companion files; each player supplies their own legitimate game installation and matching supported executable profile. DLC sets may differ; shared-catalogue filtering remains mandatory. ACSE remains required; ACSEDebug does not.

## Reachability and compatibility

Direct IPv4 normally needs a reachable public host endpoint plus appropriate router and host firewall rules for the chosen TCP port. IPv6 needs a usable route on both sides and an inbound firewall allowance. Do not assume an IPv6-only host can be reached by an IPv4-only guest merely because the application supports both families.

A router offering port forwarding does not guarantee a public inbound IPv4 path. DS-Lite/provider NAT can block that path; IPv6 or provider-supported arrangements may be required ([FRITZ! DS-Lite explanation](https://fritz.com/service/wissensdatenbank/dok/FRITZ-Box-6591-Cable/1611_Was-ist-DS-Lite-und-wie-funktioniert-es/)). Show actionable connectivity errors rather than hanging the lobby.

For broad future accessibility, reserve an optional **relay** transport behind the same authenticated lobby/command interface. Some NAT configurations cannot establish direct peer communication; a relay is a documented fallback ([IETF RFC 8656](https://www.rfc-editor.org/info/rfc8656/)). No relay, automatic NAT traversal, universal reachability or zero-configuration invitation service is implemented by this plan. A relay also introduces deployment and operating costs.

## First acceptance run on two PCs

1. Match supported game/DLL/mod/protocol versions; confirm local logging and local pipe operation independently on each PC.
2. Prove actual cross-network connectivity, server identity, invalid/expired invitation rejection, host rejection/approval and single-guest admission. Test IPv4 and IPv6 as separate routes where available; one route's pass does not certify the other.
3. Run DLC comparison, both-ready gate, common tropical-template load and both loaded/filter acknowledgements. Do not confuse loading the same template with transferring an existing host park.
4. Exercise supported manual Create/Move/Delete in both directions, peer-created objects, groups/history and receiver-preview coexistence. Check readbacks, duplicates/own echoes and lock release; preserve the local acceptance semantics.
5. Measure network RTT, queue residence, source sampling, game operation/readback and full confirmation separately. Do not subtract unsynchronized clocks on different PCs to invent one-way latency.
6. Test a controlled connection loss and verify the advertised stop/recovery policy, then matching final registries, no open locks and all completion markers. No park save in this initial transport test.

This plan changes neither the current files nor router/firewall settings. All internet and two-PC acceptance rows remain **unverified** until those runs actually occur.
