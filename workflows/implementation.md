# Implementation Workflow

## Purpose

Execute approved OCI changes safely, with repeatable validation and clear audit trail.

## Steps

1. Preflight:
   - confirm objective, `oci_profile`, region, compartments
   - verify profile exists
   - run `oci iam compartment list --all --profile <oci_profile>`
   - assess security/cost/blast radius
   - for public LB/NLB cross-VCN paths, confirm route scope is limited to approved backend VCN prefix(es) only
   - prefer dynamic DRG route distribution/propagation when supported; document any static-route exception before change approval
2. Capture baseline state before any write and store under `audit/<task-id>/raw-cli/` using `pre-*` filenames.
3. If target is production and sandbox profile exists, ask whether to run sandbox test in `<profile>`.
4. Run dry-run style checks where available.
5. Compare approved target state vs baseline; if already compliant, record no-op evidence and stop (no mutation).
6. Present exact change plan for explicit approval.
7. Execute minimal approved changes only.
8. Validate success with independent checks, including explicit verification that no unintended LB/NLB path exists to non-approved VCNs.
9. Run no-regression checks for adjacent critical flows.
10. Record timestamped change ledger (local timezone and UTC) with explicit links to pre/post evidence.

## Required Deliverables

- commands executed summary
- validation results
- rollback-ready notes
- cost estimate for medium/high risk changes
