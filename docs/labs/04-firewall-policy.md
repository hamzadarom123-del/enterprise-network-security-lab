# Lab 04 — Professional firewall policy design

**Status: planned.** This is the next exercise, not an implemented configuration.

## Objective

Replace broad test permissions with a policy that permits a specific administrative source to reach a specific service, while showing that unauthorized sources cannot.

## Proposed policy matrix

| Source | Destination | Service | Intended decision |
| --- | --- | --- | --- |
| Authorized management host | Ubuntu test server | SSH, TCP 22 | Pass |
| Other test host | Same server | SSH, TCP 22 | Block |
| Authorized management host | Same server | Unapproved test service | Block |

These are proposed roles. First confirm where the hosts attach and which ingress interface sees each flow. Same-subnet traffic may bypass the firewall entirely; use a topology that actually crosses it. Test forwarding to the server separately from firewall administration.

## Procedure and acceptance criteria

1. Preserve console access and the current policy. Confirm the SSH service is listening and endpoint policy is known.
2. Define aliases for the reviewed source and destination roles. Record their sanitized membership.
3. Review existing automatic, floating, group and interface rules. Position a narrowly scoped pass according to the effective ruleset, accounting for broad permits.
4. Enable appropriate logging. Run positive and negative tests with fresh flows and inspect only relevant states.
5. Record actual results, rule identities and packet observations. A blocked connection needs evidence that it reached the firewall and was denied there.
6. Remove temporary rules and aliases, restore the prior baseline and confirm management access.

Completion requires all matrix cases to have observed outcomes with sanitized evidence, plus a rationale for rule direction and ordering. Do not claim least privilege across the whole lab from these three tests alone.
