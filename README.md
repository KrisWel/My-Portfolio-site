# Krzysztof Weltrowski — Portfolio

Personal portfolio site for Krzysztof Weltrowski, QA Engineer (Security & Identity
Testing, Test Automation in Python).
Static HTML/CSS/JS, no build step, no framework, no backend — deploys directly
to GitHub Pages.

## Structure

```
index.html                  Main one-page site
privacy.html                Privacy policy (required before enabling ads for EU visitors)
404.html                    Custom "not found" page (GitHub Pages serves this automatically)
robots.txt / sitemap.xml    Search-engine files
assets/css/styles.css       All styling (colors/fonts as CSS variables at the top)
assets/js/main.js           Mobile nav, scroll-reveal animation, footer year
assets/img/favicon.svg      Site icon
assets/resume/
  krzysztof-weltrowski-resume.pdf    CV served by the "Download CV" buttons
```

## Editing content

All page copy lives directly in `index.html` (experience, skills, education, contact
links). Edit it like a normal HTML file — there's no CMS or data file.

The page content mirrors the CV. When the CV changes, update both:

- **CV file:** overwrite `assets/resume/krzysztof-weltrowski-resume.pdf` with the
  new PDF. Keep the file name — every "Download CV" link points to it. Visitors
  get it saved as `Krzysztof_Weltrowski_CV_EN.pdf` (set by the links' `download`
  attribute).
- **Page text:** update the matching sections in `index.html` so the site and
  the PDF don't contradict each other.

## Deploying to GitHub Pages

Deployment runs through the GitHub Actions workflow
`.github/workflows/deploy-pages.yml`:

1. One-time setup: in **Settings → Pages → Build and deployment**, set
   **Source** to **GitHub Actions**. (With "Deploy from a branch" the workflow's
   deploy step fails.)
2. Every push to `main` (including merging a PR) deploys the site automatically.
   Progress is visible in the **Actions** tab as "Deploy site to GitHub Pages";
   the site updates about a minute after the run turns green.
3. To redeploy without a code change: **Actions → Deploy site to GitHub Pages →
   Run workflow**.
4. If you use a custom domain, add it in the same Pages settings screen and
   update the `canonical`/`og:url` links and `sitemap.xml`/`robots.txt` to match.

Pages also caches responses for up to 10 minutes (`cache-control: max-age=600`),
so use a hard refresh (Ctrl+F5) if you still see the old version right after a
deploy.

The canonical URLs in `index.html`, `sitemap.xml`, and `robots.txt` currently
assume `https://kriswel.github.io/My-Portfolio-site/`. Update them if the repo
is renamed or moved to a custom domain.

## Activating Google AdSense

Ads are prepared in `index.html` but **fully disabled** — nothing ad-related is
visible on the page. There are three commented-out pieces: the loader script in
`<head>`, `AD SLOT 1` (banner below the hero) and `AD SLOT 2` (between Experience
and Education). To go live:

1. **Get an approved AdSense account.** Google requires a live site with real
   content and a privacy policy (already included here as `privacy.html`) before
   approving an account — this can't be done from localhost or a private repo.
2. Once approved, get your **Publisher ID** (`ca-pub-XXXXXXXXXXXXXXXX`) from the
   AdSense dashboard.
3. In `index.html`'s `<head>`, uncomment the `adsbygoogle.js` loader script and
   replace `ca-pub-XXXXXXXXXXXXXXXX` with your real Publisher ID.
4. For each slot, create a matching **Ad unit** in AdSense to get a
   `data-ad-slot` ID. Then enable the slot by deleting its opening line
   (`<!-- AD SLOT N ... disabled ...`) and closing line (`END AD SLOT N -->`),
   and fill in your `data-ad-client` and `data-ad-slot` values. Enable only the
   slots you want — each one is independent.
5. **EU/UK/Swiss visitors — consent is required.** Google requires publishers
   serving those regions to use a Google-certified Consent Management Platform
   (e.g. Google's own [Funding Choices](https://fundingchoices.google.com/)) before
   showing personalized ads. Set this up in your AdSense account before ads go
   live; `privacy.html` already discloses that ads may use cookies once active.

## Customizing design

Colors, fonts, and spacing are all controlled by CSS custom properties at the
top of `assets/css/styles.css` (`:root { --color-accent: ...; }` etc.) — change
them there rather than hunting through individual rules. The site also respects
`prefers-color-scheme: dark` automatically.

## License

Site code is MIT-licensed (see `LICENSE`). The content (name, experience, CV)
is personal information — reuse of the code template is fine, reuse of the
personal content is not.
