# Section 145A / Form 3CD Clause 14 — Tax Audit Assistant

Single self-contained page. No server, no database, no build step, no external requests.
Everything runs in the visitor's browser — **no client data ever leaves the machine it is
entered on.**

---

## Repository layout — this matters

```
wrangler.toml      configuration; points Cloudflare at public/
.assetsignore      safety net so private files are never published
.gitignore
README.md
public/            EVERYTHING IN HERE IS PUBLISHED. Nothing else is.
  index.html         the application
  guide.pdf          the 31-page explanatory guide
  404.html           sends wrong paths back to the tool
  _headers           caching and security headers
```

**Only `public/` is served.** That separation is deliberate. In the earlier layout every
file sat at the repository root, so Cloudflare published the `.git` folder along with the
site — which puts your entire commit history at `https://your-site/.git/config` for anyone
who looks. Keeping the site in `public/` makes that impossible.

If you have already deployed the flat layout, treat the repository as exposed: assume the
history was readable, and redeploy with this structure.

---

## Deploying

### If you are using Wrangler / Workers (what your build log shows)

The `wrangler.toml` in this repo does the work. In the Cloudflare dashboard, the project's
**build output / assets directory should be left to the config file** — do not override it
to `/`.

Deploy command: `npx wrangler deploy`
Build command: leave **empty** — there is nothing to compile.

Your URL is the `*.workers.dev` address shown at the end of the deploy log.

### If you would rather use Cloudflare Pages

1. Dashboard → **Workers & Pages → Create → Pages → Connect to Git**
2. Pick the repository
3. **Framework preset:** `None`
4. **Build command:** leave completely empty
5. **Build output directory:** `public`   ← this is the line that matters
6. Save and Deploy

Pages ignores `wrangler.toml` for static projects, so setting the output directory to
`public` is what keeps `.git` out of the published site.

---

## Checking it actually worked

After deploying, open these in a browser:

| URL | What you should see |
|---|---|
| `https://your-site/` | The tool, starting on the six-step home screen |
| `https://your-site/guide.pdf` | The guide opens |
| `https://your-site/.git/config` | **404 — if this shows a file, stop and fix the output directory** |

That third one is the check worth doing every time.

---

## Updating it later

Replace `public/index.html` and commit. The link stays the same and everyone is on the
current version — which is the main reason to host it rather than email the file around.

---

## Adding your own domain later

Nothing in the repo changes. In the project settings add a custom domain such as
`clause14.yourfirm.in` and create the CNAME record Cloudflare gives you. The
`workers.dev` or `pages.dev` address keeps working alongside it.

A firm domain is what makes the link read as a professional application rather than a side
project. It is the single most worthwhile change you can make.

---

## If you later want it restricted to your team

Cloudflare Access can put a login in front of the whole site — dashboard, under
**Zero Trust → Access → Applications**. Check the current free seat allowance first.
Nothing about the tool itself needs to change.

---

## Things to know before circulating

**A public link is public.** With no login, anyone who has the address can open it.

**The source is readable.** Anything that runs in a browser can be read with View Source or
saved with Ctrl+S. Hosting does not change that.

**Check the ICAI position on advertising and solicitation** if this is going beyond your own
firm or team.

**It is a working aid.** The law applicable is the law for the relevant previous year, and
GST return table numbering should be confirmed against the format notified for that year.

---

## What it does not do

No data is saved between sessions. There is no login, no database and no record of past
engagements. Complete an engagement in one sitting and print the working paper to PDF before
closing the tab. That is deliberate: it is what allows the tool to be used on client data
without any confidentiality question arising.
