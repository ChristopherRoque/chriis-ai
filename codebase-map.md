# codebase-map — christopherroque.com

Personal link-in-bio page for **Chris Roque**, at **christopherroque.com**
(registered 2026-07-24 at GoDaddy). Linked from the @chriis.ai Instagram bio,
but the page is name-branded, not handle-branded, so it survives any account
rename. Built on
[LittleLink](https://github.com/sethcottle/littlelink) (MIT), a static
HTML + CSS link page. No build step, no framework, no JavaScript required
to render, no backend.

## What it is

One page. A heading, a one-line bio, and a stack of link buttons. Editing a
link means editing one line of HTML and committing it — Vercel redeploys on
push automatically.

## Files that matter

| Path | What it is | Touch it when |
|------|-----------|---------------|
| `index.html` | The whole page. Head/meta at top, link buttons in the middle. Extra buttons (X, YouTube, TikTok, LinkedIn, Substack, Cal.com) sit pre-written inside an HTML comment block, ready to switch on. | Adding, removing, or reordering a link; changing the bio line or share preview text |
| `css/chriis.css` | Our visual override, loaded last so it beats the upstream styles. Neutral dark register — no brand-color button fills, no gradients, no glow, per the global taste bar. | Changing colors, type, spacing, button treatment |
| `css/style.css` | Upstream LittleLink layout and theme system. | Rarely — prefer overriding in `chriis.css` |
| `css/brands.css` | Upstream per-brand button colors. Deliberately unused — we do not apply `button-<brand>` classes. | Never, unless we intentionally adopt brand fills |
| `css/reset.css` | Upstream CSS reset. | Never |
| `images/icons/*.svg` | White monochrome brand and generic icons shipped by LittleLink. | Adding a button whose icon isn't present yet |
| `images/avatar.png`, `avatar@2x.png` | Still the upstream LittleLink logo. **Placeholder — not shown.** The avatar `<img>` and the favicon link are both commented out in `index.html` until a real @chriis.ai profile picture replaces these files. | Adding the real profile photo |
| `privacy.html` | Upstream privacy page, linked from the footer. | If the page ever collects anything |
| `vercel.json` | Static-hosting config: clean URLs, no trailing slashes, long-lived caching for assets. | Changing hosting behavior |
| `docker/`, `wrangler.toml` | Upstream deploy paths for Docker and Cloudflare. Unused — we deploy on Vercel. | Never, unless the host changes |

## Links currently live on the page

MyServiceOps (myserviceops.ai) · Reconciled (reconciledai.com) · JobSend
(jobsend.co) · Instagram (@chriis.ai) · Email (admin@myserviceops.ai).
All four URLs were confirmed returning 200 on 2026-07-24.

## Hosting and deploy

**GitHub Pages**, served from `main` at the repo root. Custom domain
`christopherroque.com`. Push to `main` publishes — there is no build step and no
deploy command to run.

GitHub repo: `ChristopherRoque/chriis-ai` — **public**, which GitHub Pages
requires on a free plan. Safe: the repo holds only the public page. Never commit
anything private here.

DNS lives at GoDaddy: four apex `A` records pointing at GitHub Pages
(185.199.108–111.153) plus a `www` CNAME to `christopherroque.github.io`.
The `CNAME` file at the repo root is what binds the domain — deleting it
unbinds the site.

### Why not Vercel

A Vercel project (`christopher-roques-projects/chriis-ai`) was created first and
**abandoned**. Every deployment returned `BLOCKED` with no logs and zero build
duration. Vercel's Hobby plan explicitly forbids commercial use, defined in their
fair-use docs as any deployment "advertising the sale of a product or service" —
this page links to MyServiceOps, Reconciled, and JobSend, so it qualifies. The
block fires before the build runs, which matches the symptoms exactly. Not
proven (Vercel doesn't disclose trigger criteria) but it fits and the
alternatives were ruled out. **Do not retry Vercel for this page.** `vercel.json`
is retained but inert.

Vercel Web Analytics was wired into `index.html` and is now dead weight on
GitHub Pages — the insights script simply 404s. Harmless; strip it or swap in
another analytics provider when someone cares about numbers.

## Datastore

None. See `schema.md`.

## Design constraint

This page is judged against the global taste bar (`~/SecondBrain/TASTE.md`):
Stripe/Apple/Tesla register, dark mode, confident whitespace, no decoration.
The banned AI-tells are pill shapes, gradients, glow and colored shadows, and
glassmorphism. The upstream LittleLink default look uses brand-colored button
fills, including an Instagram gradient — that is why `chriis.css` overrides
every button to a single neutral treatment. Do not reintroduce brand fills.
