# Design Workflow

## Purpose

Turn requirements into an approved OCI network/security architecture with explicit risk and cost implications.

## Inputs

- user objective and success criteria
- `oci_profile`, target region(s), compartment scope
- constraints: compliance, latency, HA, throughput, budget
- existing topology and dependencies

## Steps

1. Resolve scope and assumptions; batch clarifying questions early.
2. Build current-state summary (as-is).
3. Propose target-state options (to-be), including tradeoffs.
4. Define ingress-boundary policy for public LB/NLB paths: approved backend VCN targets only and dynamic-routing preference/requirements.
5. Evaluate each option for security, blast radius, operations, and cost.
6. Select recommended option and explain why alternatives were rejected.
7. Define implementation sequence and validation plan.
8. Request approval before any mutation.

## Outputs

- recommended architecture
- rejected alternatives and rationale
- risk level + key risks
- implementation plan + validation plan
- estimated cost impact
