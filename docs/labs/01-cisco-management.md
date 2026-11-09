# Lab 01 — Cisco management foundation

**Status:** historical configuration and outcomes reported by the owner. IOS XE version additionally supported by a directly pasted command excerpt. No full running configuration is archived.

**Anonymized examples:** all infrastructure IP addresses and hostnames in this report replace actual deployed values using the [public addressing convention](../architecture.md). Historical roles, VLAN IDs and evidence status are preserved.

## Objective and historical topology

Establish switch/hypervisor/Windows management connectivity and apply scoped administrative and access-port controls. See the [addressing inventory](../architecture.md).

| Item | Historical configuration |
| --- | --- |
| Switch | Cisco Catalyst C9200CX; IOS XE 17.12.03 / 17.12.3 (Dublin) |
| Management SVI | VLAN 10, 192.0.2.2/24 |
| Proxmox uplink | Gi1/0/1, access VLAN 10; host 192.0.2.50/24 |
| Windows administrative PC | Gi1/0/2, access VLAN 10; 192.0.2.10/24 |
| Additional VLANs | 20 USERS, 30 SERVERS, 40 DMZ created; not integrated through a physical trunk |
| Remote administration | SSH v2, local administrative authentication, VTY source restrictions |
| Web administration | HTTP and HTTPS management services disabled |
| Unused ports | Administratively shut down |
| Windows access-port protection | BPDU Guard; sticky MAC port-security, maximum one MAC, violation mode restrict |

Exact ACL entries, local credentials, sticky MAC values, unused-port ranges and full switch SKU are not supplied. Do not infer them.

## Direct command evidence

The owner supplied the following excerpt from `show version`; unrelated support, copyright and build lines are omitted:

```text
Cisco IOS XE Software, Version 17.12.03
Cisco IOS Software [Dublin], Catalyst L3 Switch Software (CAT9K_LITE_IOSXE), Version 17.12.3, RELEASE SOFTWARE (fc7)
```

This supports the software identity/version, not the port configuration or hardening settings. The two version spellings refer to the same release. The C9200CX identification comes from the owner report.

## Historical verification and troubleshooting

| Activity | Historical observation | Evidence status |
| --- | --- | --- |
| Physical connectivity and management access | Performed; management reachability reported | Owner report; original outputs pending |
| Windows ICMP troubleshooting | Windows Defender Firewall investigated during connectivity work | Owner report; exact profile/rule changes and before/after output not supplied |
| Administrative hardening | Settings in the table above configured historically | Owner report; sanitized configuration excerpt pending |
| Software identification | IOS XE 17.12.03 / 17.12.3, Dublin | Direct supplied command excerpt above |
| Physical trunk integration | Not completed | Planned |

Windows firewall policy can affect ping without proving a switch-path failure. The audit does not establish the exact failing direction, remediation rule or final Windows policy; those details must not be invented.

BPDU Guard protects the edge-port assumption against received BPDUs. Sticky port-security restricts learned source MAC membership; it is not user authentication. Neither feature demonstrates that violations were deliberately tested.

## Recovery and limits

No configuration commands need to be rerun to document this historical work. Before any future exercise, preserve console access and a private backup and scope rollback to the actual changes. Do not blindly reload the switch.

This report does not claim a trunk, physical inter-VLAN routing, penetration-test coverage or independently verified present-day hardening.
