# Deploying titanflowconsulting.com (GitHub Pages)

This folder is a complete, deploy-ready static site. One page, everything inlined (images are embedded in the HTML — no asset folders to manage).

**Files:**

| File | Purpose |
|---|---|
| `index.html` | The site (single file, self-contained) |
| `404.html` | Branded not-found page |
| `og.png` | Social-share card (used when the link is posted in Slack/LinkedIn/texts) |
| `CNAME` | Tells GitHub Pages the custom domain (`titanflowconsulting.com`) |
| `robots.txt` / `sitemap.xml` | Search-engine plumbing |
| `.nojekyll` | Tells GitHub not to run Jekyll processing |

---

## Step 0 — Contact form: DONE ✓

The form is already wired to your Formspree endpoint (`https://formspree.io/f/moeabazr`), delivering to matthew@titanflowconsulting.com (free tier: 50 submissions/month, spam-filtered). No edits needed.

One thing after deploying: submit a test through the live site — the very first submission triggers a one-time confirmation email from Formspree; click it, then confirm the test lands in your inbox.

## Step 1 — Put the site on GitHub Pages

**Web-UI path (no terminal needed):**

1. github.com → New repository → name it anything (e.g. `titanflow-site`) → **Public** (Pages on private repos requires a paid plan; the site is public anyway) → Create
2. "Uploading an existing file" → drag all files from this folder (including the hidden `.nojekyll` — if your OS hides it, use the git path below) → Commit
3. Repo → Settings → Pages → Source: "Deploy from a branch" → Branch: `main`, folder `/ (root)` → Save
4. Wait ~1 minute; the site appears at `https://<your-username>.github.io/titanflow-site/`
5. Still in Settings → Pages → Custom domain: enter `titanflowconsulting.com` → Save (the included `CNAME` file keeps this setting sticky)

**Git path (what you know):**

```
cd titanflow-site
git init && git add -A && git commit -m "TitanFlow Consulting site v1"
git branch -M main
git remote add origin git@github.com:<your-username>/titanflow-site.git
git push -u origin main
```

Then do steps 3–5 above in Settings → Pages.

## Step 2 — Point the domain (ZenBusiness dashboard)

ZenBusiness Dashboard → Domain settings → DNS Manager.

> ⚠️ **Touch only A and CNAME records for `@` and `www`.** Do NOT remove or edit MX or TXT records — those run your matthew@titanflowconsulting.com email. Deleting them breaks your inbox.

Remove any existing A/CNAME records for `@` and `www` that point elsewhere, then add:

**Four A records** for host `@` (apex):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**One CNAME record:** host `www` → `<your-username>.github.io`

Propagation is usually minutes, occasionally up to 24–48h.

## Step 3 — HTTPS

Back in GitHub → Settings → Pages: once the DNS check passes, tick **Enforce HTTPS** (the certificate can take a few minutes to issue — if the checkbox is greyed out, wait and refresh).

## Step 4 — Verify before announcing

- [ ] `https://titanflowconsulting.com` loads with the padlock (and `www.` redirects)
- [ ] "Book a free intro call" opens your Google booking page
- [ ] Contact form test submission arrives at matthew@titanflowconsulting.com
- [ ] Page looks right on your phone
- [ ] Then: send the Gmail draft to Allison — **add Danielle's address first**

## Later (nice-to-haves, not blockers)

- **Headshot:** when you have one, the About card is ready for it — ask Claude to drop it in (one small HTML edit + redeploy).
- **Updates:** any content change = edit `index.html`, commit, push. Live in ~1 minute. Claude can generate the edited file any time.
- **Google Search Console:** verify the domain so Google indexes you for "ServiceTitan accounting consultant" searches.
- **Analytics:** Plausible/GoatCounter are one script tag if you ever want visit counts.

## Alternative: Netlify (if GitHub feels heavy)

Drag this folder onto https://app.netlify.com/drop → done. Netlify also has built-in form handling (would replace Formspree — ask Claude to switch the form markup) and the DNS steps are the same idea with Netlify's records instead.
