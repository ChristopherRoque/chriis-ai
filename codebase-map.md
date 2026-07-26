# codebase-map — christopherroque.com

Personal link-in-bio page for **Chris Roque**, at **christopherroque.com**
(registered 2026-07-24 at GoDaddy). Linked from the @chriis.ai Instagram bio,
but the page is name-branded, not handle-branded, so it survives any account
rename. Built on
[LittleLink](https://github.com/sethcottle/littlelink) (MIT), a static
HTML + CSS link page. No build step, no framework, no JavaScript required
to render, no backend.

## What it is

One page, sized to fit a single phone screen with no scrolling. Monogram (a
real headshot when one exists), name, credential line, two-sentence bio, three
product buttons, one contact line.

**The page exists to keep a promise made somewhere else.** The @chriis.ai
Instagram bio reads: *"Tech Founder / Former Plumbing Service Ops Manager (5+
Years) / Helping service businesses automate, scale & reach 7+ figures with AI
↓"*. Every visitor is a service-business owner who just read that and tapped.
Two things follow, and both are load-bearing:

1. **The operator credential stays visible.** "Former plumbing service ops
   manager" is the trust asset that separates Chris from every other person
   selling AI to contractors. It is the first thing under his name.
2. **Only links this audience needs.** Deliberately absent, with reasons
   recorded inline in `index.html`: Instagram (every visitor came from there —
   linking back is a loop), X / YouTube / TikTok / Substack (not accounts he
   runs), LinkedIn (worth one small contact icon if the profile is active —
   needs a confirmed handle), and a booking link (the highest-value future
   addition, since the bio promises help and there is currently no way to ask
   for it beyond email).

Editing a link means editing one block of HTML and committing it — GitHub Pages
republishes automatically.

## Files that matter

| Path | What it is | Touch it when |
|------|-----------|---------------|
| `index.html` | The whole page. Head/meta at top, three two-line product buttons in the middle, contact line under them. A comment block at the bottom records which links were deliberately left off and why — read it before adding anything. | Adding, removing, or reordering a link; changing the bio, credential, or share preview text |
| `css/chriis.css` | Our visual override, loaded last so it beats the upstream styles. Neutral dark register — no brand-color button fills, no gradients, no glow, per the global taste bar. Owns the primary/secondary button split and the two-line button layout. | Changing colors, type, spacing, button treatment |
| `css/style.css` | Upstream LittleLink layout and theme system. | Rarely — prefer overriding in `chriis.css` |
| `css/brands.css` | Upstream per-brand button colors. Deliberately unused — we do not apply `button-<brand>` classes. | Never, unless we intentionally adopt brand fills |
| `css/reset.css` | Upstream CSS reset. | Never |
| `images/icons/*.svg` | White monochrome brand and generic icons shipped by LittleLink. | Adding a button whose icon isn't present yet |
| `images/avatar.png`, `avatar@2x.png` | Still the upstream LittleLink logo. **Placeholder — not shown.** The avatar `<img>`, the favicon link, and the `og:image` all point here, and the first two stay commented out until a real square headshot replaces these files. A `CR` monogram div stands in meanwhile. A real face outperforms initials on this page — swapping it in is the single highest-value edit outstanding. | Adding the real profile photo |
| `privacy.html` | Upstream privacy page, linked from the footer. | If the page ever collects anything |
| `vercel.json` | Static-hosting config: clean URLs, no trailing slashes, long-lived caching for assets. | Changing hosting behavior |
| `docker/`, `wrangler.toml` | Upstream deploy paths for Docker and Cloudflare. Unused — we deploy on Vercel. | Never, unless the host changes |

## Links currently live on the page

Ordered by relevance to an inbound service-business owner, not by company size:

1. **MyServiceOps** (myserviceops.ai) — the primary action, and the only button
   with a light fill. Everything else is outlined. One page, one lead action.
2. **JobSend** (jobsend.co)
3. **Reconciled** (reconciledai.com)
4. **Email** (admin@myserviceops.ai) — a quiet contact line under the stack, not
   a button. Contact is not a destination.

Each product carries a one-line plain-English descriptor. A bare product name
means nothing to a stranger; the descriptor is what makes the page read as a
real page rather than a filled-in template. Do not add a button without one.

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

Vercel Web Analytics was wired into `index.html` and **removed on 2026-07-26** —
the insights script only 404s on GitHub Pages. The page now loads zero
JavaScript. Add an analytics provider when someone actually cares about numbers.

## Datastore

None. See `schema.md`.

## Design constraint

This page is judged against the global taste bar (`~/SecondBrain/TASTE.md`):
Stripe/Apple/Tesla register, dark mode, confident whitespace, no decoration.
The banned AI-tells are pill shapes, gradients, glow and colored shadows, and
glassmorphism. The upstream LittleLink default look uses brand-colored button
fills, including an Instagram gradient — that is why `chriis.css` overrides
every button to a single neutral treatment. Do not reintroduce brand fills.
