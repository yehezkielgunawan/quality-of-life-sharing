# Agent Notes

This repo is a **Slidev presentation deck**, not a web application.

## Project Basics

- **Package manager:** `pnpm` (locked to `11.11.0` via `packageManager` field)
- **Main content:** `slides.md`
- **Framework:** [Slidev](https://sli.dev) (Vue-based slides)
- **Output:** Static SPA in `dist/` (gitignored)

## Development

```bash
pnpm install
pnpm dev        # http://localhost:3030
```

Edit `slides.md` to change slide content.

## Build & Deploy

### Build commands

| Command | Purpose |
|---------|---------|
| `pnpm build` | Standard Slidev build |
| `pnpm cloudflare:build:ci` | Build with `--base /` for Cloudflare Workers |
| `pnpm deploy:cf` | Local one-shot: build → remove `_redirects` → `wrangler deploy` |

### Deployment target: Cloudflare Workers (static assets)

This deck deploys as a **Cloudflare Worker with static assets**, not Cloudflare Pages.

Key config in `wrangler.toml`:

```toml
[assets]
directory = "./dist"
not_found_handling = "single-page-application"
html_handling = "auto-trailing-slash"
```

### Critical gotcha: remove `_redirects` / `_headers`

Slidev generates a `dist/_redirects` file (and sometimes `_headers`) during build. These are meant for Netlify/Pages. If you deploy to Workers without removing them, Cloudflare throws:

```
Invalid _redirects configuration: Infinite loop detected...
```

The GitHub Action and the `deploy:cf` script already delete these files. If you deploy manually, run:

```bash
rm -f dist/_redirects dist/_headers
```

before `wrangler deploy`.

## CI/CD

- Workflow: `.github/workflows/deploy.yml`
- Trigger: `workflow_dispatch` only (manual run from GitHub Actions tab)
- Required secrets:
  - `CLOUDFLARE_API_TOKEN`
  - `CLOUDFLARE_ACCOUNT_ID`
- Worker name: `quality-of-life-sharing`

## File Guide

| File | Purpose |
|------|---------|
| `slides.md` | All slide content and speaker notes |
| `wrangler.toml` | Cloudflare Worker + static assets config |
| `.github/workflows/deploy.yml` | Manual GitHub Actions deploy |
| `package.json` | Scripts and dependencies |
