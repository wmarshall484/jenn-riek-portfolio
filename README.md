# Jenn Riek — Portfolio

Static portfolio site for Jenn Riek (creative strategist & marketing manager).
No build step, no framework: one HTML file, one stylesheet, and an `assets/` folder.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The whole site. Every project card, link, and paragraph lives here. |
| `styles.css` | Colors, fonts, layout. Tokens are at the top under `:root`. |
| `assets/work/` | Project images (WebP). `about-jenn.webp` is the headshot. |
| `assets/social/` | The 19 social-media gallery images, in display order. |
| `favicon.svg` | Browser-tab icon. |
| `_headers` | Cloudflare Pages cache headers for `assets/`. |

## Deploy on Cloudflare Pages

Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → pick this repo.

| Setting | Value |
| --- | --- |
| Framework preset | None |
| Build command | *(leave blank)* |
| Build output directory | `/` |

Then **Custom domains** → add the domain (and `www`). DNS records and the certificate are created automatically.
Every push to `main` redeploys.

## Editing

- **Change text or a link:** edit `index.html` directly. Each project is an `<article class="card">` or `<article class="feature">` block.
- **Add a project:** copy an existing `<article>` block in the matching section, swap the image, title, description, and `href`.
- **Add a social post:** drop the image in `assets/social/`, then copy one `<a class="tile">` block in the `#social-media` section. Change the platform label inside `tile__tag` if needed (Instagram, LinkedIn, X, YouTube, Imgur).
- **Swap the headshot:** replace `assets/work/about-jenn.webp` (portrait orientation, roughly 4:5 works best).
- **Add an email address:** in the `#contact` section, add a second button:
  `<a class="btn btn--ghost" href="mailto:you@example.com">Email me</a>`
- **Change the accent color:** edit `--accent`, `--accent-ink`, and `--accent-soft` in `styles.css`.

### Images

Convert new images to WebP to keep the site fast (needs `brew install webp`):

```sh
cwebp -q 82 my-image.png -o assets/work/my-image.webp
```

### Preview locally

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Fonts

Fraunces (headings) and Manrope (body) load from Google Fonts. If the fonts ever fail to load, the site falls back to Georgia and the system sans-serif.
