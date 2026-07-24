# AI coding assistants

NS uses Claude Code as the primary AI coding assistant. This doc covers conventions that apply across every repo — per-repo specifics live in each repo's `CLAUDE.md`.

## Where instructions live

- **Root `CLAUDE.md`** — monorepo-wide orientation: what lives where, how submodules work, credentials table, routing rules.
- **Sub-project `CLAUDE.md`** (per product / per client) — authoritative for that project's build commands, architecture, and conventions. Read before touching code inside that directory.
- **`AGENTS.md`** — used by some products (e.g. `novrascale-site`) to point AI assistants at framework-specific docs bundled in `node_modules`. Heed those pointers; don't answer from training-data memory about newer framework versions.

Rule: the most-specific `CLAUDE.md` wins. Don't duplicate content between root and sub-project files. Link instead.

## Where Claude assets live

- **`.claude/` in a repo** — NS-owned agents (`ns-*`), skills, and settings. Committed. Ships with the repo.
- **`.claude/agents/library`** — the broader agent collection, vendored **in-repo as a git submodule** pointing at [`NovraScale/agents`](https://github.com/NovraScale/agents), NS's own fork of the `awesome-claude-code-subagents` collection. Its ~140 agents load straight from the clone. **Do not re-clone upstream into `~/.claude/agents/`** — some agents in the fork are tuned for NS (e.g. `hormozi` is rebuilt around NS's offer stack), and an upstream copy at user level would shadow the tuned versions with generic ones. A `git clone --recurse-submodules` is required to get the library; a plain clone leaves it empty and every library agent missing.
- **User level (`~/.claude/`)** — first-party skills and MCP servers (e.g. Cloudflare's). Not committed. Each repo's `.claude/REQUIRED.md` lists the full manifest and a fresh-clone setup checklist.

## Attribution

NS commits do not carry `Co-Authored-By: Claude` (or any bot) trailers. Human authors own their commits. The assistant is a tool, not a co-author.

## Secrets and AI

- Do not paste secrets into AI chat sessions. Reference them by name (e.g. "the `META_ACCESS_TOKEN` in `.env.local`") and let the assistant load them at execution time.
- The credentials table in the root `CLAUDE.md` is the canonical inventory of NS-level keys. When adding a new key, update that table in the same commit.

## Skills you'll want to know about

- `new-client` — scaffolds a new client repo end-to-end (repo + README + docs tree + Drive folder). Use instead of the 10-step manual procedure.
- `code-review` — reviews the working diff for correctness and cleanup opportunities.
- `verify` — exercises a change end-to-end before you claim it's done.
- `deep-research` — multi-source, fact-checked research for prospect intel or strategic questions.

The full list is discoverable via the Skill tool in any Claude Code session.
