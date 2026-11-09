# Lab 03 — Stateful firewall fundamentals

**Status: reported; evidence pending.** Earlier learning sessions report LAN-to-WAN routing, ICMP state inspection, inbound rule-direction experiments, WAN blocking, explicit pass rules and firewall logs. No raw evidence is available in this repository.

## Objective and topology

Explain the difference between a new flow and its return traffic using `LAN_TEST_HOST → OPNsense → WAN_TEST_HOST`. The WAN host is a simulator, not the Internet.

## Technical basis

OPNsense normally applies interface filtering on ingress. A new LAN-originated flow is therefore normally evaluated at LAN ingress; a new WAN-originated flow at WAN ingress. Stateful pass rules can permit matching return traffic. Existing states can affect a rule-change test, so inspect them and remove only relevant lab states when needed. See the [OPNsense firewall reference](https://docs.opnsense.org/manual/firewall.html).

Do not reduce the full ruleset to a blanket “first match wins” statement: floating/group rules, automatic rules and quick/non-quick behavior matter. Record the active rules and installed version.

## Preconditions

- Confirm bridge assignments, routes, endpoint firewalls and actual NAT mode using [Lab 02](02-virtual-network.md).
- Record all relevant LAN/WAN, group, floating and automatically generated policies.
- A private simulated WAN may interact with WAN private-network blocking. Record that setting; any exception must remain scoped to the isolated simulation.
- Preserve management access, save a private backup and record rules to restore. Avoid global state resets.

## Test matrix

All observations below await a fresh recorded run. Use a small bounded ping test, inspect states and capture on both firewall interfaces where needed.

| ID | New traffic | Required starting condition | Expected outcome | Observed |
| --- | --- | --- | --- | --- |
| F01 | LAN host → WAN host, ICMP echo | Explicit matching LAN pass; viable return path | Request and reply succeed; state visible | Not recorded |
| F02 | Reply to F01 | Matching state still exists | Return traffic accepted through state | Not recorded |
| F03 | WAN host → LAN host, fresh ICMP echo | No matching pass or prior state; routed destination | New traffic blocked; logging enabled for relevant block | Not recorded |
| F04 | WAN host → LAN host, fresh ICMP echo | Temporary narrowly scoped WAN pass and valid routing | Request and reply succeed | Not recorded |
| F05 | LAN host → WAN host after policy removal | Relevant old state removed; no other pass matches | New traffic blocked | Not recorded |

For each test record timestamp, source/destination roles, rule identity, state handling, NAT translation if present, packet observations and log action. Traffic targeting a firewall interface tests access to the firewall, not forwarding through it. NAT can change how destinations must be reached; resolve that before interpreting F03/F04.

## Interpretation and rollback

A failed ping is inconclusive without evidence: routing, endpoint policy and address resolution can also cause failure. Logs show the firewall's recorded action, while captures and endpoint observations help establish the path. A successful reply does not prove that unrelated WAN-originated traffic is allowed.

Remove the temporary test pass, restore the prior rules and confirm management plus the intended baseline. Preserve sanitized positive and negative results before changing this report to verified. NAT, Internet access and production hardening are not established by the earlier summary.
