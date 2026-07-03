# Submodules

The `NovraScale/NovraScale` monorepo is an umbrella. Every product under `products/` and every client relationship under `clients/` is its own repo, vendored in as a git submodule. Non-code business content (`notes/`, `branding/`, `docs/`, `strategy/`) is tracked directly in the parent.

This layout keeps client history and access isolated (a client repo can be shared without exposing the rest of the org) while giving one working directory to operate from.

## Working inside a submodule

`cd` into the submodule first. Commits and pushes are made from inside the submodule, against its own remote.

```
cd clients/<slug>
# edit, commit, push as normal
```

Then bump the parent-repo pointer:

```
cd ../..
git add clients/<slug>
git commit -m "Bump <slug> to <short-message>"
git push
```

**Don't** stage changes to files inside a submodule from the parent — you'll create a commit that references untracked work.

## Cloning fresh

```
git clone --recurse-submodules git@github.com:NovraScale/NovraScale.git
```

If you already cloned without `--recurse-submodules`:

```
git submodule update --init --recursive
```

## Bumping submodules

When you want the parent to point at each submodule's latest `main`:

```
git submodule update --remote --merge
git add <path>
git commit -m "Bump <path> to latest main"
```

Prefer bumping one submodule per commit, not a sweep of all of them — makes the parent-repo log readable.

## Adding a new submodule

For a new client:

```
gh repo create NovraScale/<slug> --private --clone=false
git submodule add git@github.com:NovraScale/<slug>.git clients/<slug>
git commit -m "Add <slug> submodule"
```

The `new-client` skill scaffolds the whole flow (repo + README + `docs/` tree + Drive folder) — prefer it over doing this by hand.

## Common footguns

- **Detached HEAD inside a submodule.** After a submodule update, the submodule is on a specific commit SHA, not a branch. Before editing, `git checkout main` inside the submodule so your commits land on a branch.
- **"Modified content, untracked content" in the parent status.** That's the submodule saying it has uncommitted work. `cd` into it and handle it — don't try to fix from the parent.
- **Pushing the parent before the submodule.** The parent's pointer will reference a commit that doesn't exist on the submodule's remote yet, and other clones will fail to fetch. Push the submodule first, always.
