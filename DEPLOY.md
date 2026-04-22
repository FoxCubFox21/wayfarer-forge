# Deploying Wayfarer Forge to wayfarerforge.game

The `public/` folder is now self-contained — everything the site needs is
inside it (HTML + `models/` subfolder). You can upload this directory to any
static host. Three zero-to-hero options in order of easiest:

## Option 1 — Netlify Drop (5 minutes, no account needed at first)

1. Go to https://app.netlify.com/drop
2. Drag the **entire `public/` folder** onto the page.
3. Netlify gives you a URL like `https://random-name-12345.netlify.app` — open
   it and click through to make sure the game loads.
4. Sign up for a free Netlify account so the site sticks around.
5. In the site's settings, go to **Domain management → Add custom domain** and
   enter `wayfarerforge.game`. Netlify will give you a target like
   `apex-loadbalancer.netlify.com` or a set of IP addresses.
6. At your domain registrar (where you bought wayfarerforge.game), set the
   DNS records Netlify tells you to (usually an `A` record for the apex and a
   `CNAME` for `www`). Propagation takes 10 min – a few hours.
7. Netlify auto-issues a free Let's Encrypt SSL cert once DNS points at them,
   so the site will be on `https://wayfarerforge.game`.

## Option 2 — Cloudflare Pages (best performance, free)

Requires a GitHub account:

1. Create a new GitHub repo (e.g., `wayfarer-forge`) and push the `public/`
   folder as the repo root (or as a subdirectory — either works).
2. Go to https://pages.cloudflare.com → Create a project → Connect to GitHub.
3. Pick the repo. For **Build command** leave blank. For **Output directory**
   enter `public` (or whatever you pushed). Save & deploy.
4. Cloudflare gives you a `*.pages.dev` URL. Test it.
5. In the project's **Custom domains** tab add `wayfarerforge.game`. If you use
   Cloudflare as your DNS registrar, this is one click. If not, follow their
   CNAME / A-record instructions at your registrar.

## Option 3 — GitHub Pages (free, fine for a hobby site)

1. Create a public GitHub repo. Push `public/` contents as the repo root.
2. In the repo's **Settings → Pages**, pick **Deploy from a branch → main /
   (root)**. Save.
3. GitHub gives you `https://<username>.github.io/<repo>`.
4. To use `wayfarerforge.game`, add a file `CNAME` at the repo root
   containing exactly `wayfarerforge.game`. Then in your DNS registrar add an
   `A` record pointing to GitHub's IPs (listed in their docs) and a `CNAME`
   for `www` pointing to `<username>.github.io`.

---

## What's in this folder

```
public/
├── index.html         # the Wayfarer Forge landing page
├── chapter1.html      # Wayfarer: The Wounded, Never Wolves — Kingdom 1
├── chapter2.html      # Kingdom 2 (the artefact)
├── chapter3.html      # Kingdom 3 (the war + moral choice)
├── preview.html       # dev-only model/asset viewer (don't link from prod)
├── battle.html        # dev-only — not linked from the site
└── models/            # all the .glb assets the game loads
```

## After deploying

- Open `https://wayfarerforge.game` and confirm the landing page loads.
- Click **PLAY** on *The Wounded, Never Wolves* and walk through Kingdom 1 to
  make sure the models load (the astronaut and crashed ship should appear).
- Share the link.
