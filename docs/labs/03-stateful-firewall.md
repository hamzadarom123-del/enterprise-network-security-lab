# Lab 03 — Stateful firewall fundamentals

**Status:** historical configuration and successful experiments reported by the owner. OPNsense 26.7 has a historical console-screenshot reference; original screenshot, logs and packet output are not available here. No fresh tests were run.

**Anonymized examples:** every infrastructure address and hostname below is a fictional RFC 5737 replacement, not an actual deployed value. Reported packet counts and outcomes are unchanged; address labels have been substituted consistently.

## Objective and configuration

Demonstrate pure routing, stateful ICMP handling and policy placement across an isolated LAN and simulated WAN.

| Setting | Historical value |
| --- | --- |
| Firewall | VM 200 firewall-example; OPNsense 26.7 per screenshot reference |
| WAN | vtnet0 on vmbr2, 203.0.113.2/30 |
| LAN | vtnet1 on vmbr1, 198.51.100.1/24 |
| WAN private-network blocking | Disabled in the original RFC1918 simulation; public example addresses are TEST-NET replacements |
| Source NAT | Disabled for the pure-routing experiment |
| LAN endpoint | VM 101, 198.51.100.10/24; gateway 198.51.100.1 for remote networks |
| Simulated WAN endpoint | VM 103, 203.0.113.1/30 |
| Return route on VM 103 | 198.51.100.0/24 via 203.0.113.2 |

The /30 WAN network is 203.0.113.0/30, with .1 and .2 as host addresses. This segment does not establish Internet or production connectivity.

## Historical experiments and verification table

| ID | Activity | Reported observation | Evidence classification |
| --- | --- | --- | --- |
| F01 | Ping 198.51.100.10 → 203.0.113.1 | 10 sent, 10 received, 0% loss | Owner-supplied historical result; original output not attached |
| F02 | Inspect OPNsense states and Live View | State table and logs inspected during training | Owner report; original state/log artifacts pending |
| F03 | Apply scoped LAN IN ICMP block before default LAN allow | Matching block observed in firewall log | Owner report; original log/screenshot pending |
| F04 | Study default denial for new WAN-to-LAN traffic | Default-deny behavior studied | Historical training report; detailed observation not supplied |
| F05 | Specific WAN IN ICMP pass from simulated upstream toward LAN | Experiment reported completed successfully | Owner-reported success; exact rule export and counters pending |

No test timestamps, RTT values, state identifiers, packet captures or full ruleset are fabricated. F04 is not an independently evidenced blocked-packet test. F05 does not establish a general WAN permit.

## Scoped blocking rule

| Field | Historical setting |
| --- | --- |
| Description | LAB-BLOCK-ICMP-TO-WAN |
| Interface / direction | LAN IN |
| Action | Block |
| Source | 198.51.100.10 |
| Destination | 203.0.113.1 |
| Protocol / type | ICMP / Echo Request |
| Position | Before the default LAN allow rule |
| Observation | Matching block appeared in firewall log |

The supplied addresses identify IPv4 endpoints. The complete rule export, other advanced options and its present enabled state are not supplied. This historical record is not a claim that the rule was later removed.

## Interpretation

**Routing versus filtering.** The LAN gateway and WAN-side return route define the forward and return paths. Disabling source NAT keeps the original LAN source address visible to the WAN host. Routing provides a path; it does not authorize traffic through the firewall.

**Ingress direction.** A LAN-originated request enters OPNsense on LAN, so the scoped block belongs at LAN IN. A new WAN-originated request enters on WAN and requires an applicable WAN-side permission. “WAN-bound” traffic is not necessarily evaluated as a new flow on WAN IN.

**Rule order.** In the reported interface-rule experiment, placing the narrow block before the broad default LAN pass prevented that pass from handling matching new requests. The full ruleset also includes automatic, floating and group policies; quick/non-quick behavior prevents treating every rule as a universal first-match list.

**Stateful return traffic.** Matching replies to an allowed flow can use its state without an independent broad reverse-direction permit. ICMP request/reply tracking is distinct from a TCP connection handshake. An unrelated new WAN echo request is a separate flow, not automatically authorized by the LAN-initiated ping.

**Existing states.** A rule edit can appear ineffective while an existing state remains. For a future test, inspect and expire only the relevant lab state if necessary. The historical audit does not say whether any states were cleared, so no reset is claimed.

## Troubleshooting and limits

A failed ping alone cannot identify the cause: routes, endpoint firewall rules and address resolution also matter. Use the recorded firewall action with path evidence to distinguish filtering from forwarding failures. The separate Windows Defender Firewall incident is documented in [Lab 01](01-cisco-management.md).

Disabling private-network blocking was specific to the private simulated WAN; it should not be generalized to an Internet-facing firewall. Complete policy state, endpoint policies and cleanup require artifacts before this report can be marked repository-verified. Future exercises should preserve management access and record the exact rollback.

Reference: [OPNsense firewall rules, states and processing order](https://docs.opnsense.org/manual/firewall.html). Current documentation may show UI differences from the historical 26.7 installation.
