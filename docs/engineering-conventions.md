# Engineering conventions

The floor. Every NS code repo — products, client sites, internal tools — must clear this bar.

## Git hooks (required)

Every code repo runs a two-tier hook setup via Husky:

- **pre-commit** — Prettier on staged files + a `\uXXXX` literal-escape guard. Sub-second; runs on every commit.
- **pre-push** — `npm run lint && npm run typecheck` per sub-project. 5–15s; runs once before push.

The split exists because ESLint cold-start + `tsc` on Next.js + React 19 sub-projects is too slow to run on every commit. Don't move the slow checks back into pre-commit — that's why pre-push exists.

The full drop-in (single-package repos and multi-sub-project monorepos) lives at [`templates/client-site-snippets/precommit-hooks.md`](https://github.com/NovraScale/NovraScale/blob/main/templates/client-site-snippets/precommit-hooks.md) in the monorepo. If you open a repo and find no `.husky/` and no `husky` devDep, install it before doing other work.

The hooks are the local half. The same `lint` + `typecheck` (plus `format:check`, `build`, tests, and a gated deploy) run again in CI on every push and PR, via the shared standard. See [ci-cd.md](./ci-cd.md). Local and CI enforce the same bar, so a green pre-push should mean a green pipeline.

## `--no-verify` policy

Don't. Not on `git commit`, not on `git push`. If a hook fails, fix the underlying issue — the hook is telling you something. The only justification is a hook that is itself broken (typo in the script, dependency conflict), and even then the fix is to unbreak the hook in the same session.

If a slow check is the friction, that's what pre-push is for — do not move checks into pre-commit to skip pre-push.

## Commit scope

**One submodule per commit.** The NovraScale monorepo vendors every product and client repo as a git submodule. When you change files inside a submodule, commit and push those changes in that submodule first; then bump the parent's pointer in a separate commit.

Never mix changes to two submodules in one commit — it makes rollback ambiguous and the parent-repo diff useless for reviewers.

## Commit messages

- Imperative mood, present tense: "Add contact form" not "Added" or "Adds".
- First line under ~70 chars.
- Body wraps at ~72 chars, explains **why** — the diff already shows what.
- No `Co-Authored-By: Claude` (or any bot) trailer. NS commits are attributed to their human author.

## Branches and PRs

NS works **on `main`, directly**, in every repo. No feature branches, no human-opened PRs, no squash-merges. Keep history linear. This supersedes any per-repo `CONTRIBUTING`/`CLAUDE` policy that says otherwise.

PRs exist for exactly one thing: **Dependabot dependency updates**. Those are reviewed and merged by a human (rebase-merge, to keep history linear), never auto-merged. When a PR is in play, the org-default template (`.github/PULL_REQUEST_TEMPLATE.md`) applies; its verification section is not decorative, so actually exercise the change before checking the box.

## Secrets

- Never commit `.env*` files (they're gitignored; keep them that way).
- NS-level secrets live in `.env.local` at the monorepo root. The absolute path is machine-dependent (`/Users/neo/NovraScale/.env.local` on macOS, `/home/neo/NovraScale/.env.local` on Ubuntu), so reference it relative to the repo root and probe rather than hardcoding. The file is gitignored and is not shell-sourced by default; load it inline in a subshell when a script needs the keys.
- Rotate a Worker secret with `npx wrangler secret put <NAME>` **and** update the `.env.local` mirror in the same session. Worker secrets are write-only, so the mirror is the only readable copy.
- When you add a new NS-level key, update the credentials table in the root `CLAUDE.md` in the same commit that introduces the consumer of that key.
