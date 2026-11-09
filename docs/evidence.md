# Evidence and publication standard

## Provenance

This update uses the owner's historical lab audit of commit `89068b1`, the accessible training-session summaries and a directly pasted Cisco `show version` excerpt. No switch, hypervisor, endpoint or firewall was accessed to recreate historical results.

A screenshot described by the owner is not the same as an image present and inspected in the repository. Historical success may be documented without relabeling it independently verified.

## Evidence labels

| Label | Meaning |
| --- | --- |
| Historical configuration — owner reported | Settings explicitly supplied in the training audit; no live-state assurance |
| Historical outcome — owner reported | Completed action/result reported by the owner; original artifact unavailable |
| Screenshot-supported — historical reference | Owner identifies an original training screenshot; image not yet archived/inspected here |
| Direct command evidence — supplied excerpt | Actual pasted output available in the report; supports only the fields shown |
| Repository-verified | Dated, sanitized supporting artifacts are present and reviewed against a specific claim |
| Planned / deployment unconfirmed | Future activity or ambiguous deployment status; no completed-result claim |

## Evidence register

| Claim | Source available now | Classification / remaining gap |
| --- | --- | --- |
| Cisco IOS XE 17.12.03 / 17.12.3 (Dublin) | Owner-pasted show version excerpt in [Lab 01](labs/01-cisco-management.md) | Direct command evidence; no claim about other switch settings |
| Cisco ports, VLANs and hardening | Detailed owner audit | Historical configuration; original sanitized config pending |
| Proxmox bridges, VM resources and routing | Detailed owner audit | Historical configuration; versions/exports pending |
| VM 101 startup after removing VLAN tag | Detailed owner audit | Historical outcome; original task log pending |
| OPNsense 26.7 | Console screenshot described by owner | Screenshot-supported historical reference; image unavailable here |
| LAN-to-WAN ping, 10/10 received | Numeric result supplied by owner audit | Historical outcome; raw output/screenshot pending |
| State table / Live View and ICMP block log | Owner audit | Historical outcome; original log/state images pending |
| Specific WAN IN ICMP pass | Owner reports successful completion | Historical outcome; rule details and artifacts pending |
| GUI reached through SSH forwarding | Owner audit | Historical outcome; screenshot pending |
| VM 102 final deployment | Planned/configured during training | Final deployment unconfirmed |
| Temporary vmbr1 address removal | No completion evidence supplied | Cleanup unconfirmed |
| Lesson 18 | Next planned practical activity | Planned |

## Artifact structure

Use [docs/assets](assets/README.md) for reviewed screenshots, organized by lab. Folder README files describe intended contents; they are not evidence. Do not generate sample logs or screenshots that could be mistaken for actual results.

Suggested image name: `lab-03-icmp-block-YYYY-MM-DD-sanitized.png`, using the original capture date when known. Mark an unknown capture date explicitly in the report rather than inventing it.

Each added artifact should identify its source, capture date if known, related claim, redactions and what it cannot establish. Link it from the relevant lab report. Preserve failed and inconclusive results too.

## Privacy and sanitization

All public infrastructure addresses and hostnames are anonymized examples, not actual deployed values. Use RFC 5737 TEST-NET-1 for management, TEST-NET-2 for LAN, and a /30 within TEST-NET-3 for simulated WAN. Keep host offsets and routing relationships consistent. Standard loopback values are retained. Device roles, VLAN IDs, technologies and evidence status remain unchanged. These ranges are documentation-only, not deployment assignments.

Original historical documentation, the owner audit and a verified Git bundle are preserved in private local records outside the public Git repository. Do not publish that backup, its filesystem path or the example-to-real mapping.

Remove passwords, password hashes, tokens, private keys, VPN secrets, SNMP communities, serial numbers, MAC addresses, public infrastructure details and personal/customer identifiers. The historical SSH account name `root` is retained to explain the supplied command; no authentication secret is included.

Review screenshot browser bars, side panels, terminal prompts and metadata. Apply opaque redaction, flatten and inspect the export. Review captures for payloads and unrelated traffic. Keep private originals outside Git; ignore rules do not erase tracked history.

## Contradictions and limits resolved

- Earlier “unknown bridge/port/address” statements reflected missing source material; the owner audit now supplies historical values.
- The initial “no command output supplied” statement is superseded by the actual Cisco version excerpt.
- IOS XE 17.12.03 and 17.12.3 are two displayed spellings of the same release.
- vmbr1 initially had no host IP; 198.51.100.254/24 was a temporary administration exception. Cleanup is not established.
- An IP subnet and switch VLAN 20 do not establish tagging; the working VM 101 configuration removed tag 20. Public subnet numbering is anonymized independently of unchanged VLAN IDs.
- OPNsense version has a referenced historical screenshot, not a screenshot independently reviewed here.
- VM 102 was planned/configured during training; verified final deployment remains uncertain.

## Publication review

Review the diff, links, diagrams, evidence labels and sensitive-content scan before committing. The owner authorized push, pull request creation and merge after sanitization checks pass. A pull-request description is prepared under [review notes](review/historical-lab-audit.md).

### Git history findings

The original unpublished audit commit contained real lab addresses and hostnames in six Markdown files. It was flagged and privately archived, then replaced before publication; adding a cleanup commit alone would have exposed its parent. Existing published branch history had no matches for those known values in the local history scan. Reachable publication history is rescanned after replacement. The original object may remain in local reflogs/object storage; it is not an ancestor of the sanitized branch and is not to be pushed. A scan reduces disclosure risk but is not proof that every possible secret has been detected.

**Existing public-history finding:** initial commit `eccf460` contains a personal email address in its author/committer metadata. Its value is not repeated here. It was already in public history before this update; shared history has not been rewritten. Updating Git email settings or sanitizing current files does not remove that earlier metadata. Removing it requires a separately coordinated history rewrite and does not guarantee removal from existing clones or caches.

No production FH connectivity, physical Cisco–OPNsense inter-VLAN integration, deployed FortiGate, VPN, enterprise HA or completed certification is established. No license is added.
