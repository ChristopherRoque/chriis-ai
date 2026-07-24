# codebase-map — chriis.ai

Link-in-bio page for the Instagram account **@chriis.ai**. Built on
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

GitHub repo: `ChristopherRoque/chriis-ai` (private).
Vercel project: `christopher-roques-projects/chriis-ai`, connected to that repo.

**Push to `main` publishes. Never run `vercel deploy` or `vercel --prod` by
hand** — this repo has a remote, so it belongs to the merge-triggers-deploy
class alongside mso-website-v2 and torrent-plumbing, and the bash firewall
blocks the manual CLI deploy on purpose.
The intended custom domain is **chriis.ai** — unregistered as of 2026-07-24,
so the page currently answers on its Vercel URL.

Vercel Web Analytics is wired in `index.html` via the standard insights
script. It only starts recording once Analytics is enabled in the Vercel
project dashboard; until then the request 404s harmlessly.

## Datastore

None. See `schema.md`.

## Design constraint

This page is judged against the global taste bar (`~/SecondBrain/TASTE.md`):
Stripe/Apple/Tesla register, dark mode, confident whitespace, no decoration.
The banned AI-tells are pill shapes, gradients, glow and colored shadows, and
glassmorphism. The upstream LittleLink default look uses brand-colored button
fills, including an Instagram gradient — that is why `chriis.css` overrides
every button to a single neutral treatment. Do not reintroduce brand fills.
