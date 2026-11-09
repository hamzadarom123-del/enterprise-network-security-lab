# Lab 01 — Cisco management foundation

**Status: reported; evidence pending.** The earlier session summary describes a management VLAN on a Cisco Catalyst C9200CX. No configuration or command output was supplied.

## Objective

Establish a controlled switch management path and explain the relationship between VLAN membership, the management SVI and upstream reachability.

## Validation procedure

Before changes, preserve console access and a private configuration backup. Record the exact hardware and IOS XE version. On the authorized switch, collect read-only output such as `show version`, `show vlan brief`, `show ip interface brief` and `show interfaces trunk`. Sanitize outputs before adding them here.

Check the management SVI state, relevant access-port membership and any actual trunk configuration. An SVI being administratively enabled does not guarantee its line protocol is up. Verify reachability from the authorized management endpoint and identify the gateway or routing mechanism used for off-subnet management.

## Result record

| Test | Expected | Observed | Evidence |
| --- | --- | --- | --- |
| VLAN and SVI inventory | Intended management VLAN and SVI present | Not recorded | Pending |
| Authorized management path | Reachable using the intended path | Not recorded | Pending |
| Trunk inventory | Actual port modes documented; no trunk assumed | Not recorded | Pending |

## Recovery and limits

Revert only the changes made in the exercise using console access and the reviewed prior configuration. Do not blindly reload or overwrite the running configuration. No SSH hardening, inter-VLAN routing or Cisco–OPNsense integration is claimed by this report.
