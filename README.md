# Section 145A / Form 3CD Clause 14 — Tax Audit Assistant

Single self-contained page. No server, no database, no build step, no external requests.
Everything runs in the visitor's browser — **no client data leaves the machine it is entered on.**

---

## READ THIS FIRST — replace the whole repository

Do not add these files alongside what is already there. The old `index.html` at the top of
your repository is a broken build, and while it exists it is the one Cloudflare serves.

**Delete every file in the repository, then upload these seven.** On GitHub the quickest way
is to delete the repository and create a fresh one of the same name.

```
index.html         the application          ← published
guide.pdf          the 31-page guide        ← published
404.html           wrong paths go home      ← published
_headers           caching and security     ← published
.assetsignore      what must NOT be published
wrangler.toml      deployment configuration
README.md          this file
.gitignore
```

Everything sits at the top level. That is deliberate: Wrangler auto-detects the repository
root as the assets directory, so this is the layout it actually expects. `.assetsignore`
is what keeps `.git`, `wrangler.toml` and this README out of the published site.

---

## Deploying

Connect the repository in the Cloudflare dashboard. Leave the build command **empty** —
there is nothing to compile. Do not set a build output directory; `wrangler.toml` handles it.

Your URL is the `*.workers.dev` address printed at the end of the deploy log.

---

## Three checks after every deploy

| URL | What you must see |
|---|---|
| `https://your-site/` | The tool, on the six-step home screen with a **Start** button |
| `https://your-site/guide.pdf` | The guide opens |
| `https://your-site/.git/config` | **404.** If a file downloads, your repository is public — stop and fix `.assetsignore` |

Also check the deploy log. It should say roughly **"Read 5 files from the assets
directory"**. If it says sixty, it is publishing `.git` and the exclusions are not working.

---

## If the page is blank below the blue bar

That means the HTML loaded but the scripts did not run. Press **F12 → Console** and read the
first red line. Nine times out of ten it is a stale cached copy: hard-refresh with
**Ctrl+Shift+R** (Windows) or **Cmd+Shift+R** (Mac), because `index.html` is served with
`must-revalidate` but browsers still hold onto it.

---

## Updating it later

Replace `index.html` and commit. The link stays the same and everyone is on the current
version — the main reason to host it rather than email the file around.

---

## Adding your own domain later

Nothing in the repo changes. Add a custom domain such as `clause14.yourfirm.in` in the
project settings and create the CNAME record Cloudflare gives you. The `workers.dev`
address keeps working alongside it.

---

## Restricting it to your team later

Cloudflare Access can put a login in front of the site — dashboard, **Zero Trust → Access →
Applications**. Check the current free seat allowance first. The tool itself needs no change.

---

## Before circulating

**A public link is public.** With no login, anyone with the address can open it.

**The source is readable.** Anything running in a browser can be read with View Source.
Hosting does not change that.

**Check the ICAI position on advertising and solicitation** if this goes beyond your own firm.

**It is a working aid.** The law applicable is the law for the relevant previous year, and GST
return table numbering should be confirmed against the format notified for that year.

---

## What it does not do

No data is saved between sessions. No login, no database, no record of past engagements.
Complete an engagement in one sitting and print the working paper to PDF before closing the
tab. That is deliberate — it is what allows the tool to be used on client data without a
confidentiality question arising.
