# Jenn Riek — Portfolio

Static portfolio site for Jenn Riek (creative strategist & marketing manager).
No build step, no framework: one HTML file, one stylesheet, and an `assets/` folder.

The site is a two-column "dossier" layout: a terracotta bio rail on the
left (headshot, positioning, facts, skills, contact) and a scrolling work column
on the right — an intro, then four work sections (Content strategy, Social
media & influencer, Creative strategy, Events) and a contact band with a
message form.

The rail has no scrollbar of its own: it scrolls up with the page until its
bottom reaches the bottom of the window, then stays pinned (pure CSS — see the
`.rail-col` / `.rail` comment in `styles.css`). Below 900px wide it becomes a
normal block above the work.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The whole site. Every project card, link, and paragraph lives here. |
| `styles.css` | Colors, fonts, layout. Tokens are at the top under `:root`. |
| `assets/work/` | Project images (WebP). `about-jenn.webp` is the headshot. |
| `assets/social/` | Social-media post images (the always-on grid, plus the @corporatenatalie influencer card). |
| `Jenn-Riek-Resume.pdf` | The résumé behind both "Download résumé" buttons. Replace the file (same name) to update it. It lives at the root, not in `assets/`, because `assets/` is cached for a year. |
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

- **Change text or a link:** edit `index.html` directly. Work items are `<article>`/`<div>` blocks — `.study` (image + copy cards; add `study--media-right` to put the image on the right; `.study--redesign` is the website redesign with stats and browser-framed screenshots; `.study--feature` is used for the influencer program and brand advocates), `.influencer` (influencer cards), `.ad-card` (native ads), `.case-card` (Creative multi-post), `.event` (Events).
- **Add a project:** copy an existing block in the matching section, swap the image, title, description, and `href`.
- **Add a social post:** drop the image in `assets/social/`, then copy one `<a class="social-tile">` block in the `.social-grid` of the `#social` section. Tiles fill left to right, row by row, in the order they appear in the HTML.
- **Replace an image:** add it under a *new* file name and point the `<img>` at it. Files in `assets/` are cached by browsers for a year, so overwriting one in place won't reach returning visitors.
- **Contact form:** posts to [FormSubmit](https://formsubmit.co). The first real submission triggers an activation email to the address in the form's `action`; after activating, you can swap the address for the random alias FormSubmit gives you so the email isn't in the page source.
- **Swap the headshot:** add the new photo under a new name in `assets/work/` and update the rail's `<img>` (portrait orientation, roughly 4:5 works best).
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
