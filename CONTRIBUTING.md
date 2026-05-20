# Contributing

## Scope

`setup-astm` is a single-action repository. The active product surface is the GitHub Action defined by `action.yml` and the TypeScript runtime in `src/`.

## Local Verification

`just` is the canonical local entrypoint for repository tasks.

The repository-owned verification and maintenance recipes are:

- `just fix`: runs `pnpm format` and `pnpm lint:fix`
- `just check`: runs `pnpm format:check`, `pnpm lint`, and `pnpm typecheck`
- `just test`: runs `pnpm test`
- `just coverage`: resets `coverage/` and runs `pnpm test:coverage`
- `just clean`: removes repository-local generated artifacts under `.tmp`, `coverage`, and `node_modules`

`package.json` retains the atomic pnpm scripts behind these recipes:

- `pnpm format`
- `pnpm format:check`
- `pnpm lint`
- `pnpm lint:fix`
- `pnpm test`
- `pnpm test:coverage`
- `pnpm typecheck`
- `pnpm package`

## Distribution Boundary

`dist/` is committed because GitHub Actions executes repository contents directly from the tagged revision. Normal development changes do not update `dist/`.
Release automation on `main` runs `pnpm package`, commits `dist/` when changed, and then creates release tags.

## Release Model

The repository versions one action. Consumer-facing tags follow `vX.Y.Z`, and the moving major tag for workflows is `v2`.
Release automation is manually dispatched with an `X.Y.Z` input, validates it on `main`, creates `vX.Y.Z`, moves `v2`, and publishes the GitHub Release.

## Documentation

`README.md` is the public front door. `docs/` owns task-oriented usage, durable architecture, and configuration reference surfaces.
