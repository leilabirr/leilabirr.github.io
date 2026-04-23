# Leila Birr Clothing Resale

A simple, static two-page website for **Leila Birr Clothing Resale** that links out to all of Leila's selling platforms and provides a donate / sell-to-me landing page.

- `index.html` — home page with the logo, tagline, and a gallery of shop cards (Mercari, Poshmark, Depop, eBay, Curtsy, Vinted, Facebook Marketplace, plus a Donate / Sell card).
- `donate.html` — "Give Your Clothes a Second Life" page with Donate / Sell buttons, the "How I Price" section, and the "Work Behind the Sale" icon row.

Pure HTML + CSS, no build step, no JavaScript frameworks. Ready to deploy to GitHub Pages.

## Project Structure

```
Leila_Birr_Resale/
  index.html          # Home / shop gallery
  donate.html         # Donate or sell page
  css/
    styles.css        # Shared design tokens + layout
  assets/
    logo.png          # Brand logo (user-provided)
    favicon.png
    shops/            # Per-shop wordmark/logo SVGs
  .nojekyll           # Tells GitHub Pages to serve files as-is
  README.md
```

## Preview Locally

The easiest way is to just open `index.html` in your browser. If your browser blocks some things over `file://`, run a tiny local server instead:

```bash
cd Leila_Birr_Resale
python3 -m http.server 8080
```

Then visit <http://localhost:8080> in your browser.

## Deploy to GitHub Pages

1. Create a new GitHub repository (e.g. `leila-birr-resale`).
2. From the `Leila_Birr_Resale` folder, initialize git and push:

   ```bash
   cd Leila_Birr_Resale
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin git@github.com:YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

3. On GitHub, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Set **Branch** to `main` and folder to `/ (root)`, then click **Save**.
6. GitHub will publish the site at `https://YOUR_USERNAME.github.io/YOUR_REPO/` within a minute or two.

### Using a custom domain

If you want to use a domain like `leilabirr.com`:

1. In repo **Settings → Pages**, enter the domain in the **Custom domain** field.
2. At your DNS provider, add the GitHub Pages DNS records (A records pointing to GitHub's IPs, or a CNAME for a subdomain).
3. GitHub will automatically create a `CNAME` file in the repo so the setting sticks.

## Editing Content

Common things you might want to tweak:

- **Shop links** — update the `href` on each `<a class="shop-card">` in `index.html`.
- **Email address** — search both HTML files for `leilabirr@yahoo.com` and replace if it ever changes. It's used on the Contact Us footer link and both Donate / Sell buttons.
- **Copyright year** — search for `2026` in both HTML files.
- **Colors & fonts** — edit the `:root` design tokens at the top of `css/styles.css`.
- **"How I Price" paragraph** — edit the `<p class="pricing-copy">` block in `donate.html`.

## Notes

- Google Fonts (Playfair Display + Inter) load from a CDN. They work fine on GitHub Pages.
- The `.nojekyll` file prevents GitHub Pages from running Jekyll, which would otherwise ignore files/folders starting with an underscore.
- All external shop links open in a new tab with `rel="noopener noreferrer"` for safety.
