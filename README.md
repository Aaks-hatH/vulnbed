# WebScan Testbed — Intentionally Vulnerable Demo Site

A deliberately vulnerable banking demo for testing WebScan. **Do not use real credentials or sensitive data.**

## Deploy to GitHub Pages in 3 steps

### 1. Create repo and push

```bash
git init
git add .
git commit -m "Add WebScan testbed"
gh repo create webscan-testbed --public --push
# OR: create repo manually at github.com, then:
# git remote add origin https://github.com/YOUR-USERNAME/webscan-testbed.git
# git push -u origin main
```

### 2. Enable GitHub Pages

- Go to your repo → **Settings** → **Pages**
- Source: **Deploy from a branch**
- Branch: `main` / `(root)`
- Click **Save**

Your site will be live at: `https://YOUR-USERNAME.github.io/webscan-testbed/`

### 3. Update the sitemap and robots.txt

Replace `[YOUR-USERNAME]` in `sitemap.xml` and `robots.txt` with your GitHub username.

---

## What WebScan should find

| Vulnerability | Page | Expected Severity |
|---|---|---|
| Missing CSP header | All pages | HIGH |
| Missing X-Frame-Options | All pages | MEDIUM |
| Reflected XSS (`?q=` param) | `/`, `/search.html` | HIGH |
| Reflected XSS (login error) | `/login.html` | HIGH |
| Stored XSS (bio field) | `/profile.html` | HIGH |
| CSRF — no token on forms | `/transfer.html`, `/profile.html` | MEDIUM |
| IDOR — sequential user IDs | `/profile.html?user_id=N` | HIGH |
| Open redirect (`?callback=`) | `/support.html` | MEDIUM |
| SQLi pattern in search | `/admin.html?search=` | HIGH |
| Exposed admin panel (no auth) | `/admin.html` | CRITICAL |
| Password hashes in HTML | `/admin.html` | HIGH |
| Internal paths in comments | `/index.html` | MEDIUM |
| API key in HTML comment | `/index.html` | CRITICAL |

## Scan this with WebScan

Use profile: **Full** for maximum coverage.

- Target: `https://YOUR-USERNAME.github.io/webscan-testbed/`
- Max Depth: `3`
- Max Pages: `200`
- Profile: `full`

Expected: 15–20 findings across CRITICAL/HIGH/MEDIUM.
