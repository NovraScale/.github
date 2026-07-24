<!--
Default PR template for the NovraScale org.
Individual repos can override by adding their own PULL_REQUEST_TEMPLATE.md.
Delete sections that don't apply — brevity > completeness.
-->

## What changed

<!-- One or two sentences. What did you actually change, and why? Link the issue/deal/context if there is one. -->

## Type

- [ ] Feature
- [ ] Fix
- [ ] Refactor / cleanup
- [ ] Docs / content
- [ ] Chore / tooling
- [ ] Client site: copy / assets update
- [ ] Client site: new page / section

## Scope

<!-- Which product or client repo is affected? If touching multiple submodules, list each. -->

## Verification

<!-- How did you confirm this works? Not "the tests pass" — what did you actually exercise? Screenshots for UI changes are strongly encouraged. -->

- [ ] `npm run lint && npm run typecheck` pass (pre-push hook is not enough — run it and confirm)
- [ ] Feature exercised end-to-end (not just unit-tested)
- [ ] Screenshots / recording attached (for any visible change)

## Deployment notes

<!-- Any env vars, secrets, DNS, cache, or third-party dashboard changes required alongside this merge? -->

## Follow-ups

<!-- Anything intentionally left out of this PR that needs its own ticket or a next-step commit? -->
