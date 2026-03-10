# Troubleshooting Workflow

## Purpose

Diagnose OCI network and security issues methodically and converge on the most likely fix with minimum blast radius.

## Steps

1. Define symptom, expected behavior, and affected scope.
2. Build evidence set:
   - control-plane state (routes, NSGs/security lists, gateways, DRG/RPC)
   - data-plane observations (path tests, connectivity outcomes)
   - logs (flow logs, audit logs, host/app logs when relevant)
3. If path issue, build hop-by-hop path model.
4. Classify failure category and confidence.
5. Generate ranked remediation options by likelihood vs implementation risk.
6. Apply approved fix only.
7. Re-test and confirm closure.
8. Document root cause + prevention recommendation.

## Root Cause Standard

Declare root cause only after at least two corroborating signals, with at least one from live runtime state.
