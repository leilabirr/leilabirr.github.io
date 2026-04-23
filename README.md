# Leila Birr Clothing Resale

A simple, static two-page website for **Leila Birr Clothing Resale** that links out to all of Leila's selling platforms and provides a donate / sell-to-me landing page.

- **Live site:** <https://leilabirr.github.io/>
- **Donate page:** <https://leilabirr.github.io/donate.html>
- **Repo:** <https://github.com/leilabirr/leilabirr.github.io>

Pure HTML + CSS, no build step, no JavaScript frameworks. Hosted on GitHub Pages. Default branch is `main`; pushes to `main` redeploy automatically.

---

## For AI coding assistants: read this first

This is the canonical handoff doc. If you're a fresh Cursor session, everything you need to make changes safely is in this file.

### Project layout
```
Leila_Birr_Resale/
├── index.html            # home: logo, tagline, 8-card shop grid, footer
├── donate.html           # hero, Donate/Sell CTAs, pricing section, workflow icons
├── css/styles.css        # all styles; design tokens in :root
├── assets/
│   ├── logo.png          # transparent-bg brand logo
│   ├── favicon.png
│   ├── shops/            # 8 vendor-brand SVGs (mercari, poshmark, ..., donate)
│   └── art/              # 8 clothing illustration SVGs (bag, hanger-dress, ...)
├── .nojekyll             # disables Jekyll on GitHub Pages (serve files as-is)
├── .gitignore
└── README.md
```

### Stack & conventions
- Plain HTML5 + CSS3, no JS, no framework, no build step.
- Design tokens live in `:root` of `css/styles.css`. **Never hardcode colors in HTML/SVG — use the tokens below.**
- Typography: Playfair Display (display) + Inter (body), loaded from Google Fonts CDN.
- Responsive grid breakpoints at 1024px and 640px.
- SVGs in `assets/art/` are loaded via `<img>`, so they use **explicit hex fills** (`#b5745a`), not `currentColor`. `<img>`-embedded SVGs cannot inherit parent CSS color.
- Inline `<svg>` elements (e.g. the work-step icons in `donate.html`) **do** use `currentColor` because they live in the main document.
- External shop links: `target="_blank"` + `rel="noopener noreferrer"`.
- `.nojekyll` must stay at the repo root, otherwise GitHub Pages will start processing with Jekyll and ignore files/folders starting with `_`.

### Brand tokens (from `:root` in `css/styles.css`)
| Token | Hex | Purpose |
| ----- | ---- | ------- |
| `--bg-cream` | `#f4ece1` | Page background |
| `--bg-cream-warm` | `#f0e3d3` | Warm-tinted surfaces |
| `--card-cream` | `#ebe1d2` | Shop cards |
| `--accent-terracotta` | `#b5745a` | Primary accent, illustrations, terracotta button |
| `--accent-terracotta-deep` | `#9b5b42` | Work-step icons, hover/emphasis |
| `--sage` | `#a0a882` | Sage button, "Sold" price tag |
| `--sage-deep` | `#8c9570` | Sage hover |
| `--text-dark` | `#3a2a24` | Primary text |
| `--text-muted` | `#6b5a50` | Secondary text |
| `--radius-card` | `16px` | Card corner radius |
| `--radius-pill` | `999px` | Button pill radius |
| `--max-width` | `1100px` | Content container width |

### Shop URLs (source of truth: `index.html`)
| Vendor | Live URL |
| ------ | -------- |
| Mercari | <https://www.mercari.com/u/user737369980?sv=0> |
| Poshmark | <https://posh.mk/dyVOHcmDy2b> |
| Depop | <https://depop.app.link/zdPhcHyAt2b> |
| eBay | <https://ebay.us/m/yiCmKi> |
| Curtsy | <https://curtsyapp.com/closet/FHgtPt5w7H> |
| Vinted | <https://www.vinted.com/member/263346776-birracres> |
| Facebook Marketplace | <https://www.facebook.com/marketplace/profile/1435923431/?ref=permalink&mibextid=6ojiHh> |
| Donate / Sell *(internal)* | `donate.html` |

All external cards share the CTA `"Shop now →"`. The Donate / Sell card uses `"Learn more →"`.

### Verbatim copy (search/replace cheat sheet)
| Element | Copy | File |
| ------- | ---- | ---- |
| Home tagline | `Curating a cycle of sustainable style.` | `index.html` |
| Home `<title>` | `Leila Birr Clothing Resale` | `index.html` |
| Donate `<title>` | `Give Your Clothes a Second Life — Leila Birr Clothing Resale` | `donate.html` |
| Donate headline | `Give Your Clothes a Second Life` | `donate.html` |
| Pricing section title | `How I Price` | `donate.html` |
| Work section title | `The Work Behind the Sale` | `donate.html` |
| Work step labels | Steam & Clean · Photograph · List & Crosslist · Send Offers · Answer Questions · Package · Ship | `donate.html` |
| Footer | `Copyright © 2026 Leila Birr Clothing Resale · Contact Us` | both pages |
| Contact email | `leilabirr@yahoo.com` | footer + all donate buttons |

### `mailto:` links (three places)
| Button / link | URL |
| ------------- | --- |
| Footer "Contact Us" (both pages) | `mailto:leilabirr@yahoo.com` |
| Donate page "Donate Items" button | `mailto:leilabirr@yahoo.com?subject=Donation%20inquiry` |
| Donate page "Sell to Me" button | `mailto:leilabirr@yahoo.com?subject=Selling%20inquiry` |

---

## Account safety: read before you push

**The repo lives under the `leilabirr` GitHub account, not Reid's personal account.** `gh` and `git` must be acting as `leilabirr` whenever a push happens.

### Pre-flight check (mandatory — run every session)
```bash
gh auth status
# Expected: "✓ Logged in to github.com account leilabirr (keyring)"
#           "- Active account: true"
```

If it shows a different account:
```bash
gh auth switch --user leilabirr
# or, if leilabirr isn't in the keyring on this machine:
gh auth login --hostname github.com --git-protocol https --web
```

**Also verify git's credential helper routes through gh.** `gh auth status` being green does **not** guarantee `git push` will use the gh token — git has its own credential cache (macOS Keychain, etc.) which can silently use a different account and cause a `403 Permission denied` on push.

Check and fix:
```bash
git config --global --get-all credential.https://github.com.helper
# Expected to include:  !/opt/homebrew/bin/gh auth git-credential

# If the gh helper isn't listed, run:
gh auth setup-git --hostname github.com
```
This is a one-time-per-machine step. Once set, `git push` uses whichever account is active in `gh`.

The repo-local `git config` is also scoped to this project:
```
user.name  = Leila Birr
user.email = leilabirr@yahoo.com
```
This is set with `git config` (not `--global`), so it doesn't bleed into other repos.

---

## Preview locally

```bash
cd "Leila_Birr_Resale"
python3 -m http.server 8080
# → http://localhost:8080
```

**Run the server from inside the project folder.** Running it from a parent directory will serve a directory listing instead of `index.html`.

---

## Deploy (commit & push)

From inside `Leila_Birr_Resale/`:

```bash
git add .
git commit -m "describe the change"
git push
```

GitHub Pages rebuilds in ~30–60 seconds. No clicks in the GitHub UI required.

### Verify the deploy succeeded

```bash
# Build status — look for "built"
gh api /repos/leilabirr/leilabirr.github.io/pages/builds/latest --jq '{status, error: .error.message, updated_at}'

# Live HTTP check
curl -sSI https://leilabirr.github.io/ | head -1
# Expected: HTTP/2 200
```

---

## Rollback (if the live site breaks)

Every past commit is a known-good snapshot. Rollback is additive — no history rewriting, no force-pushing.

```bash
# 1. See recent commits
git log --oneline -5

# 2. Undo the most recent commit by creating a new revert commit.
#    Safe on a pushed branch — no --force required.
git revert HEAD --no-edit
git push

# 3. Verify the rebuild and live site
gh api /repos/leilabirr/leilabirr.github.io/pages/builds/latest --jq '.status'
# Expected: "built"

curl -sSI https://leilabirr.github.io/ | head -1
# Expected: HTTP/2 200
```

### Roll back several commits at once
To restore to a known-good commit `<sha>` (e.g. `6bcb899`):
```bash
git revert --no-commit <sha>..HEAD
git commit -m "revert: restore to <sha>"
git push
```

### Restore a single file from history
```bash
git checkout <sha> -- path/to/file
git add path/to/file
git commit -m "restore path/to/file from <sha>"
git push
```

**Do not use `git reset --hard` + `git push --force` as a rollback strategy** on this repo. `git revert` is the safe, always-correct approach for pushed commits.

---

## Common edits

- **A shop URL changed** — update the `href` on the matching `<a class="shop-card">` in `index.html`.
- **Email address changed** — search both HTML files for `leilabirr@yahoo.com` and replace. It's used in the footer link and in both `mailto:` buttons on `donate.html`.
- **Copyright year** — search for `2026` in both HTML files.
- **Colors / fonts** — edit the `:root` custom properties at the top of `css/styles.css`. Don't hardcode colors elsewhere.
- **"How I Price" paragraph** — edit the `<p class="pricing-copy">` block in `donate.html`.
- **Add a new shop** — duplicate an existing `<a class="shop-card">` block in `index.html`, swap the `href`, shop-logo SVG (`assets/shops/`), illustration SVG (`assets/art/`), and description. Grid layout adapts automatically.

### Adding a new SVG illustration
If you add a new SVG to `assets/art/`, it will be loaded via `<img>`. Set fills to the explicit terracotta hex, not `currentColor`:
```svg
<svg ... fill="#b5745a" xmlns="http://www.w3.org/2000/svg">
```

---

## Scripts & helpers

### Strip a white background from Leila's logo

If Leila ever sends a new logo with a white background, re-run this to regenerate `assets/logo.png` and `assets/favicon.png` as transparent PNGs. Requires `Pillow`.

```python
from PIL import Image

src = "Leila_Birr_Resale/assets/logo.png"
img = Image.open(src).convert("RGBA")
w, h = img.size
pixels = img.load()

# Solid white → fully transparent.
# Near-white (edges / anti-aliasing) → proportionally transparent.
threshold_solid = 245
threshold_edge = 200

for y in range(h):
    for x in range(w):
        r, g, b, a = pixels[x, y]
        brightness = (r + g + b) / 3
        if brightness >= threshold_solid and abs(r - g) < 10 and abs(g - b) < 10:
            pixels[x, y] = (r, g, b, 0)
        elif brightness >= threshold_edge and abs(r - g) < 15 and abs(g - b) < 15:
            fade = 1 - (brightness - threshold_edge) / (threshold_solid - threshold_edge)
            new_a = int(max(0, min(255, a * fade)))
            pixels[x, y] = (r, g, b, new_a)

img.save(src, "PNG")
img.save("Leila_Birr_Resale/assets/favicon.png", "PNG")
```

Run from the parent of `Leila_Birr_Resale/`. First-time setup if Pillow isn't installed:
```bash
python3 -m venv /tmp/leila_venv
source /tmp/leila_venv/bin/activate
pip install --quiet Pillow
```

---

## Custom domain (future, if ever wanted)

If Leila wants a domain like `leilabirrresale.com`:

1. Create a `CNAME` file at the repo root containing just the domain, e.g. `leilabirrresale.com`.
2. At her DNS provider, add GitHub Pages' apex A records (or a `CNAME` record for a `www.` subdomain pointing to `leilabirr.github.io`).
3. In repo **Settings → Pages**, confirm the custom domain is detected and enable HTTPS once the DNS check passes.

No other site code needs to change — all internal links are relative.
