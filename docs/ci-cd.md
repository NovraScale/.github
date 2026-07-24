# CI/CD

Every NS repo shares one CI/CD standard, versioned in [`NovraScale/ci`](https://github.com/NovraScale/ci). That repo holds the reusable GitHub Actions workflows; each project repo carries a thin **caller** that picks its tier. Fix a pipeline bug once, bump the tag, the whole fleet inherits it. No per-repo copy-paste, no drift.

`NovraScale/ci`'s own README is the authoritative reference for inputs and behavior. This doc is the org-level orientation: what the tiers are, how a repo opts in, and the two things that bite.

## The tiers

| Tier | For | Reusable workflow | Runs |
|---|---|---|---|
| **1** | Static / simple sites (parking pages, redirects) | `site.yml` (`e2e: none`) | lint · typecheck · format:check · build · gated deploy · post-deploy smoke · Discord |
| **2** | Standard client sites (Next.js on Workers) | `site.yml` (`e2e: smoke`) | Tier 1 **+ a Playwright smoke** on the path that loses money if it breaks (lead form, or the a11y suite where that's the repo's e2e gate) |
| **3** | Platform apps (Next.js + Supabase, e.g. the dashboard) | `app.yml` | Tier 2 shape **+ coverage floors + full e2e on a local Supabase stack** |

Deploy runs **only on push to the default branch**, gated behind a green check (plus e2e where enabled), and ships the exact commit that passed. Migrations are never auto-applied.

## Opting a repo in

The repo's entire `.github/workflows/ci.yml` is a thin caller:

```yaml
name: ci
on:
  push: { branches: [main], paths-ignore: ["**/*.md", "docs/**"] }
  pull_request: { branches: [main], paths-ignore: ["**/*.md", "docs/**"] }
jobs:
  ci:
    uses: NovraScale/ci/.github/workflows/site.yml@v1
    with:
      e2e: smoke                       # none | smoke
      deploy: true                     # gated to push-on-main
      health-url: https://theclient.com
    secrets: inherit
```

**Multi-Worker repos carry one caller per deployable sub-project**, each filtered on its own `paths:`, with `working-directory` set. That preserves deploy isolation: a change to one Worker must not gate another's deploy. `maxx-city-realty` is the reference (`ci-brokerage.yml` + one caller per listing).

### The script contract

Callers expose these npm scripts; each CI step **auto-skips a script the repo doesn't define**, so partial adoption is safe:

| Script | Used by |
|---|---|
| `check` *or* (`typecheck` + `lint`) | all (`check` = combined `tsc && eslint`, preferred) |
| `format:check` | all |
| `build` | all |
| `test` | Tier 2/3 |
| `test:coverage` | Tier 3 (or Tier 2 with `coverage: true`) |
| `test:e2e` | `e2e: smoke` / Tier 3 |
| `cf:deploy` / `cf:build` | deploy |

Keep the a11y/Playwright gate exposed as `test:e2e` so it runs in the e2e job (which installs the browser) and blocks deploy, rather than being chained inside `cf:deploy` where no browser is installed.

### Secrets each repo sets

Passed with `secrets: inherit`; set per repo, not shared:

- `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID` — deploy
- `DISCORD_WEBHOOK_URL` — notifications (optional; absent = the notify step no-ops)
- `SENTRY_AUTH_TOKEN` — source-map upload (optional)

## Two things that bite

- **The deploy token and new routes.** The account-scoped NS Cloudflare token reconciles an **already-attached** custom domain fine (that's most deploys). It **cannot create a brand-new route**: standing up a Worker on a fresh vanity domain needs one local `wrangler login` deploy first, after which CI takes over. Symptom if you skip it: CI deploy fails where a local deploy succeeds.
- **Node version.** `site.yml` resolves the Node version from a `node-version-file` (default `.nvmrc`) relative to `working-directory`. A sub-project without an `.nvmrc` fails setup. NS pins `24`.

## Dependabot in caller repos

Caller repos run **npm only** in `.github/dependabot.yml`, never the `github-actions` ecosystem. The callers pin no actions of their own; the reusable workflows in `NovraScale/ci` are pinned at `@v1` (a moving major tag) and updated by *that* repo's Dependabot. One npm entry per deployable sub-project. See [engineering-conventions.md](./engineering-conventions.md) for the branch/PR policy that governs how dependency PRs are merged.

## Versioning

Callers pin `@v1`, a moving major tag. Backward-compatible fixes re-point `v1`, so every repo gets them for free. Breaking changes ship as `@v2`.
