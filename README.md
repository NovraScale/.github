# .github

Org-level defaults for the [NovraScale](https://github.com/NovraScale) GitHub organization.

GitHub treats this repo specially — files here become the fallback for every repo in the org that doesn't define its own.

## What's here

| Path | What GitHub does with it |
|---|---|
| [`profile/README.md`](./profile/README.md) | Rendered at [github.com/NovraScale](https://github.com/NovraScale) as the org profile page. |
| [`SECURITY.md`](./SECURITY.md) | Default security policy — linked from every repo's Security tab. |
| [`PULL_REQUEST_TEMPLATE.md`](./PULL_REQUEST_TEMPLATE.md) | Default PR template for repos that don't have their own. |
| [`ISSUE_TEMPLATE/`](./ISSUE_TEMPLATE/) | Default issue templates + contact-links config. |
| [`docs/`](./docs/) | Org-wide engineering docs — conventions, playbooks, methodology. Referenced by per-repo `CLAUDE.md` / `AGENTS.md` when useful. |

> **Note:** GitHub applies these defaults only to **public** repos in the org. Most NovraScale repos are private and will not inherit these — but the profile README, SECURITY.md, and docs are still useful as a canonical source of truth.

## How individual repos override

Any repo that ships its own `.github/PULL_REQUEST_TEMPLATE.md`, `.github/ISSUE_TEMPLATE/`, or `SECURITY.md` at the repo root uses its own version. This repo is only the fallback.

## Contributing

- Changes to the profile README, security policy, or issue/PR templates should be discussed with matt@novrascale.com before merging — they're org-wide surface area.
- Changes to `docs/` follow the normal PR flow.

## Related

- Monorepo: [`NovraScale/NovraScale`](https://github.com/NovraScale/NovraScale) (private) — the umbrella repo that vendors every product and client repo as a submodule. This repo is submoduled into it at `./.github/`.
