# Jenn Riek — Portfolio

Static portfolio site for Jenn Riek (creative strategist & marketing manager).
No build step, no framework: one HTML file, one stylesheet, and an `assets/` folder.

The site is a two-column "dossier" layout: a fixed terracotta bio rail on the
left (headshot, positioning, facts, skills, contact) and a scrolling work column
on the right — an intro, then five work sections (Creative strategy, Content
strategy, Events, Social media) and a contact band.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The whole site. Every project card, link, and paragraph lives here. |
| `styles.css` | Colors, fonts, layout. Tokens are at the top under `:root`. |
| `assets/work/` | Project images (WebP). `about-jenn.webp` is the headshot. |
| `assets/social/` | Social-media gallery images (15 are shown, in display order). |
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

- **Change text or a link:** edit `index.html` directly. Work items are `<article>`/`<div>` blocks — `.case-card` (Creative multi-post), `.ad-card` (native ads), `.study` and `.featured` (Content strategy), `.event` (Events).
- **Add a project:** copy an existing block in the matching section, swap the image, title, description, and `href`.
- **Add a social post:** drop the image in `assets/social/`, then copy one `<a class="social-tile">` block in the `#social` section.
- **Swap the headshot:** replace `assets/work/about-jenn.webp` (portrait orientation, roughly 4:5 works best).
- **Add an email address:** in the `#contact` section, add a second button next to the LinkedIn one:
  `<a class="btn" href="mailto:you@example.com">Email me</a>`
- **Change the accent color:** edit `--terracotta` and `--brick` (and the related rail tokens) in the `:root` block of `styles.css`.

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

Newsreader (headings) and Manrope (body) load from Google Fonts in a single request. If the fonts ever fail to load, the site falls back to Georgia and the system sans-serif.
