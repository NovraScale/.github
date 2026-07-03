# NovraScale engineering docs

Org-wide conventions and playbooks that apply across every NS repo. Per-repo `CLAUDE.md` / `AGENTS.md` files remain the source of truth for their own build/architecture — this directory is only for things that are true everywhere.

## Contents

| Doc | What it covers |
|---|---|
| [engineering-conventions.md](./engineering-conventions.md) | Git hooks, commit scope, submodule discipline, `--no-verify` policy. The minimum bar for any NS repo. |
| [submodules.md](./submodules.md) | How the NovraScale monorepo tracks products and client repos as submodules — bumping, cloning fresh, common footguns. |
| [ai-assistants.md](./ai-assistants.md) | How NS uses Claude Code and other AI coding assistants — where CLAUDE.md lives, agents/skills conventions, secret handling. |

## When to add a doc here

Add a doc to `docs/` only if it would be true for **every** NS repo (or a large class of them). Deal-specific or product-specific docs belong in their own repo.

Failure mode this prevents: docs drift out of relevance because they were org-wide when written but became product-specific over time. If a doc starts naming one product or client, move it into that repo.
