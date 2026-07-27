# codebase-map — christopherroque.com

Personal link-in-bio page for **Chris Roque**, at **christopherroque.com**
(registered 2026-07-24 at GoDaddy). Linked from the @chriis.ai Instagram bio,
but the page is name-branded, not handle-branded, so it survives any account
rename. Built on
[LittleLink](https://github.com/sethcottle/littlelink) (MIT), a static
HTML + CSS link page. No build step, no framework, no JavaScript required
to render, no backend.

## What it is

A small credibility site, not a link card. Two pages today: a bio card
(`index.html`) and a receipts page (`proof.html`), with weekly build-log
write-ups landing inside the receipts page as they're written.

## Who this page is for — and why that changed (2026-07-26)

It was first built to serve the @chriis.ai Instagram bio, which sells to
service businesses. **That was wrong, and the strategy plan says why**
(`~/.claude/plans/lively-jingling-willow.md`, approved 2026-07-26):

- Chris's own MSO marketing plan already concluded *"Ads/content/socials are NOT
  the motion"* — his ICP lives on Google Maps and the phone. July 2026 market
  data agrees: contractors pick software off review sites and buyer guides.
  **Service-business owners are not on Instagram.** The account cannot sell to
  them.
- So the account speaks to **builders** — people who want to learn to build what
  he built. The service business is the *evidence*, not the audience.
- **The highest-value job of this site needs no audience at all.** When a
  cold-emailed shop owner googles "Chris Roque," this is what they find. That
  pays off at zero followers, which is why `proof.html` outranks follower count
  as a priority.

**Deliberately absent**, with reasons recorded inline in `index.html`: Instagram
(every visitor came from there — linking back is a loop), X / YouTube / TikTok /
Substack (not accounts he runs), LinkedIn (worth one small contact icon once a
handle is confirmed), and a booking link (highest-value future addition).

Editing a link means editing one block of HTML and committing it — GitHub Pages
republishes automatically.

## ⚠ Claim discipline (hard gate on `proof.html`)

Every number on the receipts page must trace to the live dispatch ledger. The
canonical owner of what may and may not be said is
`~/SecondBrain/mso-marketing-plan.md` § "The proof", and the approved/banned
list is duplicated as a comment block at the top of `proof.html` so nobody edits
it blind. **"Zero missed" is banned** (two documented drops exist) and the
"3 of 4 inside 6 minutes" figure is measured against *confirmed dispatches*, not
all calls — the page states that denominator in plain sight on purpose.

Note: `~/SecondBrain/business-state.md` still carries a stale "300+ dispatches,
0 missed" line from March 2026. It is superseded by the marketing plan's list.
Do not source claims from it.

## Files that matter

| Path | What it is | Touch it when |
|------|-----------|---------------|
| `index.html` | The bio card. Head/meta at top, four two-line buttons (the receipts page leads, then the three products), contact line under them. A comment block at the bottom records which links were deliberately left off and why — read it before adding anything. | Adding, removing, or reordering a link; changing the bio, credential, or share preview text |
| `proof.html` | **The receipts page — the reason this site exists.** What the dispatch system does, the ledger numbers, the ML-0056 escalation walked through minute by minute, an honest note on how it's built, and the build log. Carries a claim-discipline comment block at the top. | Adding a build-log entry; changing any stat (read the claim rules first) |
| `css/chriis.css` | Our visual override, loaded last so it beats the upstream styles. Neutral dark register — no brand-color button fills, no gradients, no glow, per the global taste bar. Owns the primary/secondary button split, the two-line button layout, and the `.container--doc` reading layout used by `proof.html` (left-aligned and wider — centred body copy is unreadable past two lines). | Changing colors, type, spacing, button treatment |
| `css/style.css` | Upstream LittleLink layout and theme system. | Rarely — prefer overriding in `chriis.css` |
| `css/brands.css` | Upstream per-brand button colors. Deliberately unused — we do not apply `button-<brand>` classes. | Never, unless we intentionally adopt brand fills |
| `css/reset.css` | Upstream CSS reset. | Never |
| `images/icons/*.svg` | White monochrome brand and generic icons shipped by LittleLink. | Adding a button whose icon isn't present yet |
| `images/avatar.png`, `avatar@2x.png` | Still the upstream LittleLink logo. **Placeholder — not shown.** The avatar `<img>`, the favicon link, and the `og:image` all point here, and the first two stay commented out until a real square headshot replaces these files. A `CR` monogram div stands in meanwhile. A real face outperforms initials on this page — swapping it in is the single highest-value edit outstanding. | Adding the real profile photo |
| `privacy.html` | Upstream privacy page, linked from the footer. | If the page ever collects anything |
| `vercel.json` | Static-hosting config: clean URLs, no trailing slashes, long-lived caching for assets. | Changing hosting behavior |
| `docker/`, `wrangler.toml` | Upstream deploy paths for Docker and Cloudflare. Unused — we deploy on Vercel. | Never, unless the host changes |

## Links currently live on the page

Ordered by what the arriving visitor (a builder) wants, not by company size:

1. **What I've built** (`proof.html`) — the primary action and the only button
   with a light fill. Everything else is outlined. One page, one lead action.
2. **MyServiceOps** (myserviceops.ai)
3. **JobSend** (jobsend.co)
4. **Reconciled** (reconciledai.com)
5. **Email** (admin@myserviceops.ai) — a quiet contact line under the stack, not
   a button. Contact is not a destination. Its wording ("tell me what's breaking
   in your shop") deliberately targets the *buyer*, since that's the money lane,
   even though the page above it speaks to builders.

**Gotcha — clean URLs.** GitHub Pages serves `foo.html` at `/foo`; a local
`python3 -m http.server` does **not**. Links are written with the explicit
`.html` so they resolve identically in local preview and in production. Don't
"tidy" them into extensionless paths — you'll lose local verifiability for a
cosmetic win.

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
