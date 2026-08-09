# Section 145A / Form 3CD Clause 14 — Tax Audit Assistant

A guided working tool for determining applicability under section 145A and reporting
under Clause 14(a) and 14(b) of Form 3CD.

Single self-contained page. No server, no database, no build step, no external requests.
Everything runs in the visitor's browser — **no client data ever leaves the machine it is
entered on.**

---

## Files

| File | What it is |
|---|---|
| `index.html` | The application. This is the whole thing. |
| `guide.pdf` | The 31-page explanatory guide with worked industry examples. |
| `_headers` | Cloudflare Pages configuration — caching and security headers. |
| `404.html` | Sends any wrong path back to the tool. |

---

## Deploying to Cloudflare Pages

You need a GitHub account and a Cloudflare account. Both free. Allow about ten minutes.

### 1. Put these files in a GitHub repository

Create a new repository — it can be **private**, Cloudflare Pages works either way.
Upload the four files above to the root of the repository, not inside a folder.

If you use the GitHub web interface: *Add file → Upload files*, drag them in, commit to `main`.

### 2. Connect Cloudflare Pages

1. Sign in at **dash.cloudflare.com**
2. In the sidebar choose **Workers & Pages**, then **Create → Pages → Connect to Git**
3. Authorise GitHub and pick the repository
4. On the build settings screen:
   - **Framework preset:** `None`
   - **Build command:** *leave completely empty*
   - **Build output directory:** `/`
5. **Save and Deploy**

There is nothing to compile, so the first deploy takes under a minute.

### 3. Your link

You get an address like:

```
https://your-project-name.pages.dev
```

That is the link to circulate. Note there is no `.html` in it — because the file is named
`index.html`, it is served at the root automatically.

### 4. Updating it later

Replace `index.html` in the repository and commit. Cloudflare rebuilds within a minute and
the same link serves the new version. Everyone is always on the current one — which is the
main reason to host it rather than email the file around.

---

## Adding your own domain later

Nothing above has to change. In the Pages project go to **Custom domains → Set up a domain**,
enter something like `clause14.yourfirm.in`, and add the CNAME record Cloudflare shows you at
whoever manages your DNS. The `.pages.dev` address keeps working alongside it.

A firm domain is what makes the link read as a professional application rather than a
side project. It is the single most worthwhile change you can make.

---

## If you later want it restricted to your team

Cloudflare Access can put a login in front of the whole site — in the dashboard, under
**Zero Trust → Access → Applications**. Check the current free seat allowance before relying
on it. Nothing about the tool itself needs to change.

---

## Things to know before circulating

**A public link is public.** With no login, anyone who has the address can open it. Decide
deliberately whether that is what you want.

**The source is readable.** Anything that runs in a browser can be read with View Source or
saved with Ctrl+S. Hosting does not change that. If protecting the logic matters, the
computation would have to move to a server — a different and much larger piece of work.

**Check the ICAI position on advertising and solicitation** if this is going beyond your own
firm or team. A publicly circulated, branded professional tool may engage those norms.

**It is a working aid.** The law applicable is the law for the relevant previous year, and
GST return table numbering should be confirmed against the format notified for that year.
The tool says so on screen and the guide says so in writing — keep that wording in place.

---

## What it does not do

No data is saved between sessions. There is no login, no database and no record of past
engagements. Complete an engagement in one sitting and print the working paper to PDF before
closing the tab. That is a deliberate design choice: it is what allows the tool to be used on
client data without any confidentiality question arising.

If you ever want engagements saved, reviewed by a partner, or shared across the firm, that
needs a backend and a considered position on where client data is stored.
