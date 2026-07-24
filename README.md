# .github

Org-level defaults for the [NovraScale](https://github.com/NovraScale) GitHub organization.

GitHub treats this repo specially: files here become the fallback for every repo in the org that doesn't define its own.

## What's here

| Path | What GitHub does with it |
|---|---|
| [`profile/README.md`](./profile/README.md) | Rendered at [github.com/NovraScale](https://github.com/NovraScale) as the org profile page. |
| [`SECURITY.md`](./SECURITY.md) | Default security policy, linked from every repo's Security tab. |
| [`PULL_REQUEST_TEMPLATE.md`](./PULL_REQUEST_TEMPLATE.md) | Default PR template for repos that don't have their own. |
| [`ISSUE_TEMPLATE/`](./ISSUE_TEMPLATE/) | Default issue templates + contact-links config. |
| [`docs/`](./docs/) | Org-wide engineering docs: conventions, CI/CD standard, submodule discipline, AI-assistant conventions. Referenced by per-repo `CLAUDE.md` / `AGENTS.md` when useful. |

> **These defaults reach every repo, public and private.** This `.github` repo is **public**, and GitHub applies a public `.github` repo's community health files (SECURITY.md, PR template, issue templates) to any repo in the org that lacks its own, regardless of that repo's visibility. Since most NovraScale repos are private, that cascade is the whole point: the security policy and templates below are live on all ~28 repos. The one exception is `profile/README.md`, which only renders on the public org page. (A private `.github` repo would *not* cascade, which is why this one stays public even though its docs describe private infrastructure. Keep nothing sensitive here.)

## How individual repos override

Any repo that ships its own `.github/PULL_REQUEST_TEMPLATE.md`, `.github/ISSUE_TEMPLATE/`, or root `SECURITY.md` uses its own version. This repo is only the fallback.

## Org-wide standards that live elsewhere

Two things every repo inherits are not in this repo:

- **CI/CD** — [`NovraScale/ci`](https://github.com/NovraScale/ci) holds the shared, versioned GitHub Actions workflows. Each repo carries a thin caller that picks its tier. See [`docs/ci-cd.md`](./docs/ci-cd.md).
- **Security posture** — Dependabot alerts, the dependency graph, and Dependabot security updates are enabled org-wide via a default [security configuration](https://github.com/organizations/NovraScale/settings/security_products/configurations), applied to all existing repos and set as the default for new ones. Nothing to configure per repo.

## Contributing

- Changes to the profile README, security policy, or issue/PR templates are org-wide surface area. Clear them with matt@novrascale.com before merging.
- Changes to `docs/` follow the normal flow.

## Related

- Monorepo: [`NovraScale/NovraScale`](https://github.com/NovraScale/NovraScale) (private), the umbrella repo that vendors every product and client repo as a submodule. This repo is submoduled into it at `./.github/`.
- CI/CD standard: [`NovraScale/ci`](https://github.com/NovraScale/ci).
- Tuned agent library: [`NovraScale/agents`](https://github.com/NovraScale/agents), NS's fork of the awesome-claude-code-subagents collection, vendored into the monorepo at `.claude/agents/library`.
