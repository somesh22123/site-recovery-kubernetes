# tsr-k8s-skill

Agent plugins for Trilio Site Recovery (TSR), owned by the TSR team.
Part of **Option A (three-repo model)** in the *Agent Plugins: Repository Structure Proposal*. Built with
[trilio-agent-plugin-kit](https://github.com/somesh22123/trilio-agent-plugin-kit) v1.0.0.

## Layout

| Path | What it is |
| --- | --- |
| `plugins/trilio-tsr-guide/plugin.yaml` | Portable source: manifest and MCP config. **Edit this.** |
| `plugins/trilio-tsr-guide/skills/` | Skills, shared by every agent tool |
| `plugins/trilio-tsr-guide/.claude-plugin/`, `.codex-plugin/`, `.cursor-plugin/`, `.mcp.json`, `mcp.json` | Generated. CI fails if edited by hand |
| `plugins/trilio-tsr-guide/agents/` | `tsr-recovery-planner` helper agent |
| `plugins/trilio-tsr-guide/hooks/` | Safety hook: asks before mutating Trilio resources (Claude Code) |
| `mcp-server/` | The TSR MCP server |
| `evals/` | Eval cases |
| `tests/` | Unit tests, run by CI |

## Workflow

```sh
git clone https://github.com/somesh22123/trilio-agent-plugin-kit .pluginkit -b v1.0.0
python .pluginkit/pluginkit.py validate .
python .pluginkit/pluginkit.py generate .        # after editing plugin.yaml or skills
```

Release by bumping `version` in `plugin.yaml` and tagging `trilio-tsr-guide/v<version>`.
The release workflow builds the zip and GitHub release; then the platform group
pins the tag in [trilio-agent-marketplace](https://github.com/somesh22123/trilio-agent-marketplace).

## Install (customers)

Customers don't add this repo directly; they add the catalog once:

```sh
claude plugin marketplace add somesh22123/trilio-agent-marketplace
claude plugin install trilio-tsr-guide@trilio
```
