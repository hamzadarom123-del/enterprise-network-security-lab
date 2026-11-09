# Milestones

These are proposed repository milestones, not GitHub releases or completed work. Dates and completion percentages are intentionally omitted until evidence supports them.

## v0.1.0 — Network Foundation & Firewall Fundamentals

Status: documentation in progress; experiments reported, evidence pending.

- [ ] Record platform versions and sanitized component inventory.
- [ ] Confirm switch management VLAN and management reachability.
- [ ] Map Proxmox bridges, physical uplinks and VM vNICs.
- [ ] Record Ubuntu addressing, default routes and WAN-side return path.
- [ ] Validate a new LAN-initiated flow and its stateful return traffic.
- [ ] Validate a blocked new WAN-initiated flow and an explicit permitted comparison.
- [ ] Attach sanitized logs or captures with expected and observed outcomes.
- [ ] Document rollback and limitations; review all artifacts for publication.

Completion requires the linked [lab reports](labs/README.md) to contain reproducible steps and actual results. A ping or screenshot alone does not prove the full architecture.

## v0.2.0 — Professional Firewall Policies

Status: planned; corresponds to the next policy-design lesson.

- [ ] Define authorized sources, destinations and services using aliases.
- [ ] Build and justify a least-privilege policy matrix.
- [ ] Test allowed management access and denied unauthorized access.
- [ ] Evaluate rule order and existing-state behavior.
- [ ] Document logs, rollback and management lockout prevention.

## v0.3.0 — Physical Switching and Segmentation

Status: planned.

- [ ] Review access/trunk design and bridge tagging behavior.
- [ ] Integrate Cisco switching with the virtual firewall using a verified port map.
- [ ] Test permitted inter-segment traffic and denied lateral traffic.
- [ ] Prove the intended path with captures and counters.

## v1.0 — Documented Enterprise Lab Baseline

Status: proposed scope, subject to owner review.

- [ ] Complete the preceding milestones with evidence.
- [ ] Document required infrastructure services and management controls.
- [ ] Demonstrate configuration backup and a controlled recovery exercise.
- [ ] Provide an architecture, policy matrix and troubleshooting case study consistent with the tested environment.
- [ ] Review residual risks and publish an accurate release summary.

Fortinet practice, VPN, high availability, IDS/IPS, cloud and automation remain optional later work. They are not represented as deployed capabilities. Certification requirements should be checked with the vendor when scheduling study or exams.
