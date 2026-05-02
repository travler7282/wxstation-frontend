# AGENTS-IMPROVEMENT-SPEC.md

Audit notes for the standalone `wxstation-frontend` repository.
Date: 2026-05-01

## Current State

| Artifact | Status |
|---|---|
| `AGENTS.md` | ✅ Updated for standalone repo |
| `README.md` | ✅ Updated for standalone repo |
| `.github/workflows/` | ✅ Updated to deploy only WXStation |
| `.github/pull_request_template.md` | ✅ Uses standalone build command |

## Changes Captured Here

1. Removed stale monorepo guidance that referenced deleted apps and backends.
2. Replaced CI/CD workflows with a standalone Vue/Vite build, test, and S3 deploy pipeline.
3. Aligned deployment docs and Vite base path with the `apps/wxstation/` deploy target.
4. Simplified repository instructions to match the files that actually exist.

## Remaining Maintenance Guidance

1. Keep `AGENTS.md` as the canonical instruction file.
2. Update thin adapter files whenever `AGENTS.md` changes.
3. Keep deployment path, `baseHref`, and CloudFront routing aligned whenever the public route changes.
