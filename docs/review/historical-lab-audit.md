# Pull request draft — historical lab audit

**Suggested title:** docs: reconstruct historical Cisco, Proxmox and OPNsense lab baseline

**Base:** main at 89068b1

**Branch:** docs/historical-lab-audit

**Publication authorization:** owner approved push, pull request creation and merge after sanitization and checks pass.

## Summary

Replace incomplete unknown-state descriptions with the owner's detailed historical configuration and reported outcomes. Preserve evidence provenance rather than claiming a fresh audit. Keep Lesson 18 planned.

## Scope

- README: topology, technology stack, progress and navigation.
- Architecture: management ports, bridge/VM mapping, addressing and return route.
- Cisco report: hardening, reachability history and direct supplied IOS XE excerpt.
- Virtualization report: VLAN-tag startup fix and SSH-forwarded GUI experiment.
- Firewall report: no-NAT routing, 10/10 ping report, ICMP block and reverse-direction study.
- Evidence/roadmap/lab index: historical evidence labels, gaps and next activities.
- Assets: per-lab screenshot folders containing instructions only; no fabricated evidence.

## Review points

All infrastructure addresses and hostnames are anonymized RFC 5737 examples. Original records and a Git bundle are preserved privately outside this repository. The unpublished original audit commit was replaced so real values are absent from branch ancestry; previously published history was also scanned. Original evidence present here remains distinct from historical screenshots/logs referenced but not attached. VM 102 final deployment, temporary host-address cleanup, exact switch SKU and Proxmox/Ubuntu versions remain unresolved.

An existing personal email in the author/committer metadata of already-public initial commit `eccf460` was flagged. This update does not repeat its value or rewrite shared history. New publication content is checked separately from this pre-existing exposure.

The initial no-host-IP bridge baseline and temporary administration address are different stages, not simultaneous permanent settings. Access VLAN 10 is retained; no working physical trunk is claimed.

## Validation

Passed relative-link checks, fenced-block balance, table-column checks, Git whitespace checks and scans of tracked files plus all reachable commit contents/metadata. New content contains only RFC 5737 example infrastructure addresses and consistent example hostnames; standard loopback is retained. The pre-existing initial-commit email finding remains flagged separately. Both topology diagrams pass the Mermaid parser and example-endpoint consistency checks. All three external Markdown documentation links returned HTTP 200. /24 endpoint/gateway membership and /30 WAN endpoint/return-route relationships were checked. Lesson 18 is unchanged. Diagrams have not been visually rendered in GitHub. No hardware changes, new packet tests or fabricated artifacts are part of this update.
