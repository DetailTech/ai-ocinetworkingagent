# OCI Agent Workspace (Codex, Claude, Gemini)

A governed agent environment for OCI networking and security operations.

Use the same control files across all clients:

- `AGENTS.md`: policy, safety model, approval gates, output contract
- `MEMORY.md`: verified environment facts and reusable learnings
- `workflows/*.md`: execution checklists by task type

Directories like `audit/`, `artifacts/`, `docs/agents-history/`, `memory-archive/`, and `sessions/archive/` are created automatically by the agent on first use.

## Getting Started

```bash
git clone https://github.com/DetailTech/ai-ocinetworkingagent.git
cd ai-ocinetworkingagent
```

## Tooling Prerequisites

Before any OCI task, make sure you have a working OCI CLI with a named (non-`DEFAULT`) profile:

```bash
oci iam compartment list --profile <your-profile> --limit 1
```

You also need at least one agentic CLI tool installed: [Codex CLI](https://github.com/openai/codex), [Claude Code](https://docs.anthropic.com/en/docs/claude-code), or [Gemini CLI](https://github.com/google-gemini/gemini-cli).

## Using This Repo

### Codex

Codex reads `AGENTS.md` from the project root automatically.

```bash
cd ai-ocinetworkingagent
codex
```

### Claude Code

Claude Code reads `CLAUDE.md`. Create a copy or symlink:

```bash
ln -s AGENTS.md CLAUDE.md
claude
```

### Gemini CLI

Gemini CLI reads `GEMINI.md`. Create a copy or symlink:

```bash
ln -s AGENTS.md GEMINI.md
gemini
```

### Session Kickoff Prompt

If your client doesn't auto-load the governance file, paste this at the start of each session:

```
Use AGENTS.md as governing policy.
Read MEMORY.md now.
Use workflows/<workflow>.md for this task.
Default to read-only. Do not perform OCI writes until I explicitly approve.
Use --profile <oci_profile> on every OCI CLI command.
```

## Recommended Daily Loop

1. Resolve context: objective, profile, region, compartment.
2. Read `MEMORY.md`, then pick a workflow from `workflows/`.
3. Run read-only discovery and evidence collection.
4. Review findings and risk.
5. Approve writes explicitly before any create/update/delete.
6. Record outputs in `artifacts/` and `audit/`.
7. Append verified learnings to `MEMORY.md`.