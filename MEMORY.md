# MEMORY.md

Agent persistent memory. Auto-updated during sessions. Read at session start.

---

## Environment

<!-- OCI profiles, regions, compartments, tenancy details, key OCIDs -->


## Known Gotchas


- (2026-03) Service Gateway must be configured with "All Services in Oracle Services Network" (not just Object Storage) for OCI Functions to pull images from OCIR. Object Storage alone is insufficient.
- (2026-03) OCI Bastion service requires outbound SSH (TCP/22) to `host.bastion.<region>.oci.oraclecloud.com` from the client network. Common cause of access failure when corporate firewalls block it.
- (2026-03) OCI Functions in private subnets need: SGW with All Services, route table entry for SGW, and security list/NSG allowing egress TCP 443 to Oracle Services Network CIDR. Test reachability with `curl -v https://ocir.<region-key>.ocir.io/v2/` — a 401 means networking works.
- (2026-03) OCI network bandwidth is allocated per compute instance based on OCPU count, not per VNIC. Single-VNIC and multi-VNIC configs on the same shape get identical bandwidth.

## Working Solutions

<!-- Non-obvious solution patterns that have been confirmed to work -->


## User Preferences

<!-- Workflow conventions, naming preferences, tool preferences, approval patterns -->
- (2026-03-09) Do not ask for approval before read-only OCI CLI `list/get` commands.
- (2026-03-09) Use subagents explicitly on substantive tasks; if tooling blocks true subagents, report `subagent_fallback` and still run parallel tracks.
- (2026-03-09) Naming convention preference: `<type-abbrev>-<pub|priv>-<project>-<env>-<version?>` (example: `sn-pub-rdptest-dev`).
- (2026-03-09) Avoid default subnet route tables/security lists and default DRG attachment routing associations when dedicated named objects are applicable.
- (2026-03-09) Always include clear descriptions on route rules, NSG/security-list rules, gateways, and attachment objects for readability and troubleshooting.
- (2026-03-10) User prefers dynamic routes

## Useful References

<!-- Confirmed-useful endpoints, doc links, CLI snippets, API quirks -->

## Recent Learnings

<!-- Append new discoveries here with date stamps. Promote to sections above when stable. -->

