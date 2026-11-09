# Milestones

Milestones describe historical progress and remaining evidence separately. They are not published releases, and no completion percentage or guaranteed date is asserted.

## v0.1.0 — Network Foundation & Firewall Fundamentals

**Status: historical practical work documented; evidence packaging incomplete.**

Completed checkboxes below mean the stated documentation task is complete, not that every historical claim has been independently retested.

- [x] Record supplied Cisco, bridge, VM, addressing and routing inventory.
- [x] Record Cisco management and historical administrative/access-port protections.
- [x] Document VM 101 VLAN-tag startup incident and reported fix.
- [x] Document reported 10/10 LAN-to-WAN ping with source NAT disabled.
- [x] Explain stateful ICMP, ingress direction and scoped logged block.
- [x] Record reported WAN IN pass experiment with its evidence limitation.
- [x] Document local SSH forwarding and temporary vmbr1 host addressing.
- [ ] Archive available original, sanitized screenshots/logs and link each to its claim.
- [ ] Resolve VM 102 final deployment and temporary address cleanup from existing records.
- [ ] Record missing Proxmox/Ubuntu versions, exact switch SKU and full relevant policy.
- [ ] Complete owner publication review and release acceptance.

Historical source recovery comes first; these gaps do not require repeating physical switch configuration just to document past work. See the [evidence register](evidence.md).

## v0.2.0 — Lesson 18: Professional Firewall Policies

**Status: PLANNED; next practical activity.**

- [ ] Define authorized source/destination/service aliases.
- [ ] Design a least-privilege policy matrix.
- [ ] Test authorized management access and denied unauthorized access.
- [ ] Evaluate rule order and existing-state behavior.
- [ ] Document actual logs, management-lockout prevention and rollback.

The existing [Lab 04 plan](labs/04-firewall-policy.md) is retained as planned. Previous ICMP exercises do not mean Lesson 18 is complete.

## v0.3.0 — Physical Switching and Segmentation

**Status: PLANNED.** VLANs 20 USERS, 30 SERVERS and 40 DMZ were created historically. The Proxmox physical uplink remains documented as access VLAN 10.

- [ ] Design the physical access/trunk and virtual bridge tagging model.
- [ ] Plan console access and rollback before changing the uplink.
- [ ] Implement and evidence Cisco–OPNsense physical VLAN integration.
- [ ] Test permitted inter-segment traffic and denied lateral traffic.
- [ ] Establish the actual traffic path using reviewed artifacts.

## v1.0 — Documented Enterprise Lab Baseline

**Status: proposed scope.**

- [ ] Complete preceding milestones and evidence review.
- [ ] Document required infrastructure services and management controls.
- [ ] Demonstrate configuration backup and controlled recovery.
- [ ] Align architecture, policy matrix and troubleshooting reports with the tested baseline.
- [ ] Review limitations and approve an accurate release summary.

Fortinet study can complement later work, but deployed FortiGate, VPN, enterprise HA, production FH connectivity and completed future certifications are not part of the current claims. Check certification requirements with the vendor when planning exams.
