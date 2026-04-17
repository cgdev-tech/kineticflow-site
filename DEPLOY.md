# Hosting the Fight Cafe Legal Site

Three files → three URLs Apple requires before App Store submission:
- `fightcafe.app/` — landing page (App Store marketing URL)
- `fightcafe.app/privacy` — Privacy Policy URL (required by App Store Connect)
- `fightcafe.app/terms` — Terms of Use

---

## Option A — GitHub Pages (free, 5 min)

1. Create a new GitHub repo named `fightcafe-site` (public)
2. Push the three HTML files into the repo root
3. Go to **Settings → Pages → Source → main branch → / (root) → Save**
4. GitHub gives you: `https://yourusername.github.io/fightcafe-site/`
5. Buy `fightcafe.app` on Namecheap/Cloudflare (~$12/yr)
6. In Namecheap DNS: add a CNAME record pointing `www` → `yourusername.github.io`
7. In GitHub Pages settings, set custom domain → `fightcafe.app`
8. Check "Enforce HTTPS" (Let's Encrypt cert, automatic)

URLs will be:
- `https://fightcafe.app/` → index.html
- `https://fightcafe.app/privacy` → privacy.html  (use `privacy.html` or rename to `privacy/index.html`)
- `https://fightcafe.app/terms`   → terms.html

> Tip: Rename `privacy.html` → `privacy/index.html` and `terms.html` → `terms/index.html` so the URLs look clean without the .html extension.

---

## Option B — Vercel (free, even faster)

1. `npm i -g vercel` (or use the web dashboard)
2. `cd legal-site && vercel`
3. Add custom domain in the Vercel dashboard
4. Done — HTTPS is automatic

---

## Option C — Framer / Carrd (no code, ~$9/mo)

Upload the HTML files or re-create the pages visually.  
Good if you want to maintain it with drag-and-drop later.

---

## App Store Connect Fields

Once hosted, paste these URLs in App Store Connect:

| Field                     | Value                           |
|---------------------------|---------------------------------|
| **Marketing URL**         | `https://fightcafe.app`       |
| **Privacy Policy URL**    | `https://fightcafe.app/privacy` |
| **Support URL**           | `https://fightcafe.app` or `mailto:hello@fightcafe.app` |

---

## Before You Submit — Checklist

- [ ] `privacy@fightcafe.app` email actually reaches you (set up forwarding)
- [ ] `legal@fightcafe.app` email actually reaches you
- [ ] Privacy Policy URL returns 200 (test in Safari)
- [ ] Terms URL returns 200
- [ ] Replace `https://apps.apple.com/app/fight-cafe` in index.html with real App Store link (after first submission)
- [ ] Review privacy nutrition label in App Store Connect matches what's in the policy
