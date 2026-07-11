# Quality of Life Sharing Session

A [Slidev](https://sli.dev) presentation deck about how AI is changing college students' quality of life — covering critical thinking, mental health, and day-to-day learning behaviors.

## What's inside

- **~20 slides** exploring the shift from pre-AI to post-AI student habits
- Research-backed claims with citations from 2024–2026 studies
- A casual, story-driven tone aimed at a student community audience

Core themes:

- 🧠 **Critical Thinking** — cognitive offloading, inference decline, passive vs. reflective AI use
- 💭 **Mental Health** — loneliness, AI dependency, procrastination, memory retention
- 🎒 **Real-Life Behaviors** — how assignments, study groups, and help-seeking have changed

## Run locally

```bash
pnpm install
pnpm dev
```

Open <http://localhost:3030>.

Edit [`slides.md`](./slides.md) to update content.

## Build

```bash
pnpm build                  # Standard build
pnpm cloudflare:build:ci    # Build for Cloudflare Workers
```

## Deploy

### Via GitHub Actions (recommended)

1. Add `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` secrets in GitHub
2. Go to **Actions → Deploy to Cloudflare Workers**
3. Click **Run workflow**

### Locally

```bash
pnpm deploy:cf
```

This builds the deck, removes the conflicting `_redirects` file, and deploys to Cloudflare Workers as a static-asset Worker.

## Tech stack

- [Slidev](https://sli.dev) — Markdown-based slides
- [Vue 3](https://vuejs.org) — underlying framework
- [Cloudflare Workers](https://workers.cloudflare.com) — hosting via static assets
- [Wrangler](https://developers.cloudflare.com/workers/wrangler/) — deployment CLI

## License

Personal sharing-session material.
