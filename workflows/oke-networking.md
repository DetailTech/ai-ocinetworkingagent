# OKE Networking Workflow

## Purpose

Validate and troubleshoot OKE networking and security posture.

## Checklist

1. Cluster endpoint exposure (private/public) and admin access path.
2. Worker subnet routes and gateway dependencies.
3. NSG/security-list layering for nodes and load balancers.
4. Pod/service CIDR overlap and routing implications.
5. CNI behavior and network policy enforcement.
6. LB/NLB integration, annotations, and health-check reachability.
7. DNS resolution and private endpoint dependencies.
8. Node OS firewall rules and required ports.
9. Flow/audit logging coverage for troubleshooting.

## Output

- pass/fail checklist with evidence links
- prioritized fixes for failed checks
