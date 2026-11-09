# Evidence and publication standard

## Result labels

| Label | Meaning |
| --- | --- |
| Planned | Exercise or design has not been executed in this documented workflow |
| Reported; evidence pending | Earlier session describes the result, but supporting artifacts are unavailable here |
| Verified | A dated report includes actual observations and reviewed supporting artifacts |
| Failed / inconclusive | Observed behavior differs from expectations or evidence cannot isolate the cause |

Do not change a report to verified based only on an earlier assistant summary. Preserve unsuccessful tests and explain what they establish.

## Required lab record

Each report should identify the objective, topology, software versions, prerequisites, starting policy, exact test direction, expected outcome, observed outcome, evidence, interpretation, limitations and rollback. Distinguish endpoint traffic from traffic addressed to the firewall itself.

Suggested artifact name: `lab-03-test-01-YYYY-MM-DD-sanitized.txt`. Add only reviewed artifacts under `docs/evidence/` when they exist; no placeholder logs or synthetic success screenshots are included.

## Sanitization

- Replace real addresses, hostnames, domains, VM identifiers, MAC addresses and interface identifiers consistently when sensitive.
- Remove passwords, hashes, tokens, private keys, VPN secrets, SNMP communities, serial numbers, usernames and organization/customer details.
- Review screenshot browser bars, side panels, terminal prompts and image metadata. Use opaque redaction, flatten the image, and check the exported copy.
- Review packet captures for payloads and unrelated traffic. Prefer minimal sanitized text excerpts where sufficient.
- Do not publish full Proxmox configuration trees, OPNsense backups, switch configurations or raw captures without reviewing their contents.
- Keep private originals outside this repository. An ignore rule is not a secrecy guarantee and does not remove files already tracked by Git.

## Before publication

1. Review the complete diff, links and diagrams.
2. Confirm each result label against its artifacts.
3. Scan tracked files and proposed additions for sensitive content; inspect manually too.
4. Check that actual topology and sanitized examples remain distinguishable.
5. Obtain owner confirmation before pushing this initial documentation or publishing a release.

No license is added by this documentation change. Choose one deliberately before inviting reuse.
