# .github

Org-level defaults for the [NovraScale](https://github.com/NovraScale) GitHub organization.

GitHub treats this repo specially: files here become the fallback for every repo in the org that doesn't define its own.

This repo is **public**, so it holds only the community-health files GitHub requires to be public. Internal engineering docs live in the private monorepo, not here. Keep nothing sensitive in this repo.

## What's here

| Path | What GitHub does with it |
|---|---|
| [`profile/README.md`](./profile/README.md) | Rendered at [github.com/NovraScale](https://github.com/NovraScale) as the org profile page. |
| [`SECURITY.md`](./SECURITY.md) | Default security policy, linked from every repo's Security tab. |
| [`PULL_REQUEST_TEMPLATE.md`](./PULL_REQUEST_TEMPLATE.md) | Default PR template for repos that don't have their own. |
| [`ISSUE_TEMPLATE/`](./ISSUE_TEMPLATE/) | Default issue templates + contact-links config. |

**These defaults reach every repo, public and private.** Because this `.github` repo is public, GitHub applies its community health files to any repo in the org that lacks its own, regardless of that repo's visibility. That cascade is the point: since most NovraScale repos are private, the security policy and templates here are live across the org. (`profile/README.md` is the exception, rendering only on the public org page.)

## How individual repos override

Any repo that ships its own `.github/PULL_REQUEST_TEMPLATE.md`, `.github/ISSUE_TEMPLATE/`, or root `SECURITY.md` uses its own version. This repo is only the fallback.

## Contributing

Everything here is org-wide, public surface area. Clear changes with matt@novrascale.com before merging.
