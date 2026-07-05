# .github

Org's central `.github` repo. Holds reusable CI workflow(s) other repos call by reference.

## Quality Gate

`.github/workflows/quality-gate.yml` is a reusable `workflow_call` workflow. Project repos invoke it like:

```yaml
jobs:
  quality-gate:
    uses: Quanby-IT-Solutions/.github/.github/workflows/quality-gate.yml@main
    with:
      node-version: "22.20.0"
      pnpm-version: "10.27.0"
      run-e2e: false
    secrets:
      NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

It runs typecheck, lint, format check, unit tests + coverage, and conditionally E2E (Playwright) when `apps/web`, `packages/contracts`, `packages/auth`, `packages/db`, or `packages/e2e-web` change.

**Changing this one file changes the CI standard for every repo that calls it.** Edit with care — a broken workflow here breaks CI org-wide.
