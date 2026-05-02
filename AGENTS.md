# AGENTS.md — Agent Instructions for wxstation-frontend

This repository contains only the WXStation frontend that was split out of the old monorepo.

## Repository Overview

| Area | Location | Notes |
|---|---|---|
| Vue app | `src/`, `public/`, `vite.config.ts` | Single Vue 3 + Vite application |
| CI/CD | `.github/workflows/` | Deploys dev and prod bundles to S3 + CloudFront |
| Runtime config | `public/runtime-config.js` | Sets the SDR API base URL |

## Layout

```
src/                  # Vue application source
public/               # Static assets copied into the build
.github/workflows/    # Dev and prod deployment workflows
vite.config.ts        # Vite build and dev-server configuration
package.json          # Root package manifest and scripts
```

## Branch Mapping

| Branch | Environment |
|---|---|
| `dev` | Development deployment |
| `main` | Production deployment |

## Tech Stack

- Node 24
- Vue 3 + Vite
- TypeScript 5.8
- Vitest for unit tests
- AWS S3 + CloudFront for static hosting

## Common Commands

Run from the repository root.

```bash
npm ci
npm run dev
npm run build
npm run test
npm run test:coverage
npm run preview
```

## Deployment

Both workflows build the Vite app, stage the bundle, and sync it to the `apps/wxstation/` prefix in the target S3 bucket.

Required secrets:
`AWS_DEV_ROLE_ARN`, `AWS_PROD_ROLE_ARN`, `AWS_REGION`, `AWS_DEV_BUCKET_NAME`, `AWS_PROD_BUCKET_NAME`, `AWS_DEV_CLOUDFRONT_ID`, `AWS_PROD_CLOUDFRONT_ID`

The production bundle uses a base href of `/apps/wxstation/`, so the deployed site must be served from that route.

## Code Conventions

- Keep TypeScript strict and follow the existing Vue single-file-component style.
- Do not add new top-level dependencies without updating `package.json`.

## Git Workflow

Agents must not commit directly to `main` or `dev`.

Preferred flow:
1. Create an issue.
2. Create a feature branch.
3. Open a PR into `dev`.
4. Promote `dev` to `main` after verification.

## Guardrails

- Do not commit `dist/`, `coverage/`, `deploy/`, or `node_modules/`.
- Do not hardcode or log secrets.
- Keep workflow changes aligned with the actual standalone repo structure.
