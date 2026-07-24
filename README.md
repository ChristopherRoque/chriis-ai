# chriis.ai

Link-in-bio page for the Instagram account [@chriis.ai](https://instagram.com/chriis.ai).

Built on [LittleLink](https://github.com/sethcottle/littlelink) (MIT) — static
HTML and CSS, no framework, no build step, no backend. Upstream license is kept
in `LICENSE.md`.

## Change a link

Open `index.html`, find the block of `<a class="button">` lines, edit the `href`
and the label. Commit and push — Vercel redeploys on its own.

Six more buttons (X, YouTube, TikTok, LinkedIn, Substack, Cal.com) are already
written and sitting inside a comment block just below the live ones. To turn one
on, delete the comment markers around it and swap `HANDLE` for the real handle.

## Add the profile picture

Save a square photo as `images/avatar.png` and a 2x version as
`images/avatar@2x.png`, then uncomment the avatar `<img>` tag and the favicon
`<link>` in `index.html`. Both are commented out right now because those files
still hold the upstream LittleLink logo.

## Preview it locally

```bash
python3 -m http.server 8899
# then open http://127.0.0.1:8899
```

## Design rules

Neutral dark, no brand-color button fills, no gradients, no glow. The upstream
LittleLink styles ship colored brand buttons (including an Instagram gradient);
`css/chriis.css` loads last and overrides them all to one flat treatment. Keep
it that way — see `codebase-map.md`.

## Analytics

Vercel Web Analytics is already wired into the page. Enable it in the Vercel
project dashboard under Analytics to start collecting; until then the script
request 404s and nothing breaks.
