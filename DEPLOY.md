# Deploy morahmani.com

Static site — no build step. Pick **one** host below and point DNS at it.

## Before you deploy

1. Edit `index.html` — replace placeholders:
   - `YOUR-LINKEDIN` → your LinkedIn slug
   - `YOUR-GITHUB` → your GitHub username (or remove the button)
   - `you@email.com` → your email
2. Drop your resume PDF at `assets/resume.pdf` (or change the Resume link).

Preview locally: open `index.html` in a browser, or:

```powershell
cd website
py -m http.server 8080
# visit http://localhost:8080
```

---

## Option A — Vercel (recommended)

1. Push this repo to GitHub (or create a **new public repo** with only the `website/` folder).
2. Sign in at [vercel.com](https://vercel.com) → **Add New Project** → import the repo.
3. If the repo is the full Mo_Dash monorepo, set **Root Directory** to `website`.
4. Deploy (no build command needed; output is static files).
5. Project **Settings → Domains** → add `morahmani.com` and `www.morahmani.com`.
6. Vercel shows the DNS records to add at your registrar. Typical setup:

   | Type  | Name | Value              |
   |-------|------|--------------------|
   | A     | `@`  | `76.76.21.21`      |
   | CNAME | `www`| `cname.vercel-dns.com` |

7. Wait for DNS propagation (minutes to a few hours). Vercel will issue HTTPS automatically.

---

## Option B — GitHub Pages (from this repo)

A workflow at `.github/workflows/deploy-website.yml` publishes the `website/` folder on every push to `main`.

1. Push the `website/` folder and workflow to `github.com/mvincer/Mo_Dash`.
2. Repo **Settings → Pages** → **Build and deployment** → Source: **GitHub Actions**.
3. After the first workflow run succeeds, **Settings → Pages → Custom domain** → enter `morahmani.com`.
4. At your registrar (where you bought morahmani.com):

   | Type  | Name | Value                    |
   |-------|------|--------------------------|
   | A     | `@`  | `185.199.108.153`        |
   | A     | `@`  | `185.199.109.153`        |
   | A     | `@`  | `185.199.110.153`        |
   | A     | `@`  | `185.199.111.153`        |
   | CNAME | `www`| `YOUR-USER.github.io`    |

   (GitHub’s UI shows the exact records for your account.)

5. Enable **Enforce HTTPS** once the certificate is ready.

---

## Option C — Netlify

1. [netlify.com](https://netlify.com) → **Add site** → import repo, set publish directory to `website`.
2. **Domain settings** → add `morahmani.com`.
3. Add the A/CNAME records Netlify provides at your registrar.

---

## DNS tips

- **Root domain (`morahmani.com`)**: usually an **A record** pointing to the host’s IP.
- **`www`**: **CNAME** to the host (Vercel/Netlify/GitHub).
- Redirect `www` → apex (or apex → www) in your host’s dashboard so both work.
- Remove conflicting old A/CNAME records for `@` and `www` before adding new ones.

---

## Updating the site

Edit `index.html` / `css/style.css`, commit, push — Vercel/Netlify redeploy automatically.
For GitHub Pages, push to `main`.
