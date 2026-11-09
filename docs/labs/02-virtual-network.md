# Lab 02 — Proxmox and Ubuntu network foundation

**Status: reported; evidence pending.** The learning summary identifies Ubuntu LAN and simulated-WAN endpoints with OPNsense between them. Exact bridge and interface mappings are unavailable.

## Objective

Map the Layer 2 segments and Layer 3 paths before interpreting firewall tests.

## Prerequisites and procedure

Retain hypervisor console access and a private backup before changing networking. Record Proxmox, Ubuntu and OPNsense versions. This report requires inventory first, not a bridge reconfiguration.

1. Inspect the Proxmox network view and each VM's vNIC configuration. Record bridge assignments, VLAN tags, bridge VLAN awareness and physical uplinks.
2. On each Ubuntu endpoint, inspect `ip -br address`, `ip route` and `ip route get <destination-address>`, replacing the placeholder privately.
3. Check that each endpoint connects only to its intended segment and that no alternate NIC or bridge provides a firewall bypass.
4. Confirm the LAN host's route toward the WAN endpoint. On the WAN side, record a return route or the actual source-NAT behavior; do not invent either.
5. Record local endpoint firewall settings so a host-level block is not mistaken for an OPNsense decision.

## Result record

| Check | Expected | Observed | Evidence |
| --- | --- | --- | --- |
| Bridge/vNIC map | Each role attached to its intended segment | Not recorded | Pending |
| Forward and return path | Traffic traverses OPNsense in both directions | Not recorded | Pending |
| Isolation | No unintended external uplink or bypass | Not recorded | Pending |

## Recovery and limits

If later changing a bridge, document the exact reversal and use console access if management is lost. Successful endpoint connectivity does not by itself prove isolation, filtering or Internet access.
