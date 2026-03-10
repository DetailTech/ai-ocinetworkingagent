# Incident Response Workflow

## Purpose

Handle OCI network/security incidents with containment, evidence preservation, and validated recovery.

## Steps

1. Scope incident:
   - affected assets, regions, compartments, related IPs
2. Contain safely with least disruption.
3. Preserve evidence snapshots before broad changes.
4. Build and test hypothesis matrix.
5. Apply approved remediation in controlled sequence.
6. Validate containment and service recovery.
7. Produce timeline, findings, and follow-up hardening plan.

## Evidence Requirements

- preserve raw CLI/log artifacts under `audit/<task-id>/`
- redact sensitive values before user-facing output
