# OCI Agent Workspace (Codex, Claude, Gemini)

This repository is a governed agent environment for OCI networking and security operations.

Use the same control files across all clients:

- `AGENTS.md`: policy, safety model, approval gates, output contract
- `MEMORY.md`: verified environment facts and reusable learnings
- `workflows/*.md`: execution checklists by task type
- `audit/`, `artifacts/`, `docs/agents-history/`: evidence and markdown history

## 1) One-Time Bootstrap

If you are recreating this environment elsewhere:

```bash
mkdir -p oci-agent-project/{workflows,artifacts,audit,docs/agents-history,memory-archive,sessions/archive}
cd oci-agent-project

touch AGENTS.md MEMORY.md \
  audit/retro-log.md \
  docs/agents-history/CHANGELOG.md \
  workflows/{design.md,implementation.md,troubleshooting.md,compliance.md,incident-response.md,oke-networking.md,fastconnect-ipsec.md}
```

## 2) Tooling Prerequisites

```bash
for c in oci codex claude gemini; do
  command -v "$c" >/dev/null && echo "ok: $c" || echo "missing: $c"
done
```

Before any OCI task, choose an explicit non-`DEFAULT` profile:

```bash
export OCI_PROFILE=<your-profile>
oci setup config list-profiles
oci iam compartment list --all --profile "$OCI_PROFILE" --limit 1
```

## 3) Using This Repo in Codex

Run from repo root:

```bash
cd /path/to/oci-agent-project
codex
```

Codex can use root-level `AGENTS.md` directly. Session kickoff prompt:

```text
Use AGENTS.md as governing policy.
Read MEMORY.md now.
Use workflows/<workflow>.md for this task.
Default to read-only. Do not perform OCI writes until I explicitly approve.
Use --profile <oci_profile> on every OCI CLI command.
```

## 4) Using This Repo in Claude

Run from repo root:

```bash
cd /path/to/oci-agent-project
claude
```

Compatibility option (if your Claude client supports `CLAUDE.md` auto-instructions):

```bash
cp -f AGENTS.md CLAUDE.md
```

If auto-loading is unclear, paste the same kickoff prompt and attach `AGENTS.md`, `MEMORY.md`, and the selected workflow file.

## 5) Using This Repo in Gemini

Run from repo root:

```bash
cd /path/to/oci-agent-project
gemini
```

Compatibility option (if your Gemini client supports `GEMINI.md` auto-instructions):

```bash
cp -f AGENTS.md GEMINI.md
```

If auto-loading is unclear, use the same kickoff prompt and include `AGENTS.md`, `MEMORY.md`, and one workflow file at session start.

## 6) Recommended Daily Loop (All Clients)

1. Resolve context: objective, `oci_profile`, region, compartment.
2. Read `MEMORY.md`, then pick one workflow from `workflows/`.
3. Run read-only discovery and evidence collection.
4. Review findings and risk.
5. Approve writes explicitly before any create/update/delete action.
6. Record outputs in `artifacts/` and `audit/`.
7. Append verified learnings to `MEMORY.md`.

## 7) Fallback Rule That Always Works

If any client fails to auto-load local policy files, manually provide:

- `AGENTS.md`
- `MEMORY.md`
- `workflows/<selected-workflow>.md`

Then require explicit acknowledgment of:

- read-only by default
- no OCI writes without approval
- no `DEFAULT` profile unless explicitly requested
- `--profile <oci_profile>` on every OCI CLI command
