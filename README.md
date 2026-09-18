# Krzysztof Weltrowski — Portfolio

Personal portfolio site for Krzysztof Weltrowski, QA Automation Engineer.
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
  krzysztof-weltrowski-resume.html   Source of the downloadable CV (ATS-friendly, single column)
  krzysztof-weltrowski-resume.pdf    Generated PDF served by the "Download CV" buttons
```

## Editing content

All page copy lives directly in `index.html` (experience, skills, education, contact
links). Edit it like a normal HTML file — there's no CMS or data file.

The CV/resume is a **separate, plainer HTML file** so it stays parseable by
Applicant Tracking Systems: single column, standard fonts, no tables or icons.
After editing `assets/resume/krzysztof-weltrowski-resume.html`, regenerate the PDF:

- **Easiest:** open the file in Chrome → `Print` → destination "Save as PDF" →
  paper size **A4**, margins **default**, "Background graphics" **on** → save over
  `assets/resume/krzysztof-weltrowski-resume.pdf`.
- The current PDF was generated headlessly with Playwright/Chromium at 94% scale,
  which is what keeps it to one page — if you add content, either trim something
  else or accept a second page.

## Deploying to GitHub Pages

1. Push this repo to GitHub (already done if you're reading this from the repo).
2. In the repo, go to **Settings → Pages**.
3. Under "Build and deployment", choose **Deploy from a branch**, branch **main**,
   folder **/ (root)**.
4. Save. The site will be live at `https://<your-username>.github.io/<repo-name>/`
   within a minute or two.
5. If you use a custom domain, add it in the same Pages settings screen (this
   creates a `CNAME` file for you) and update the `canonical`/`og:url` links and
   `sitemap.xml`/`robots.txt` to match the new domain.

The canonical URLs in `index.html`, `sitemap.xml`, and `robots.txt` currently
assume `https://kriswel.github.io/My-Portfolio-site/`. Update them if the repo
is renamed or moved to a custom domain.

## Activating Google AdSense

Three ad slots are already placed in `index.html` (below the hero, mid-page, and
the head script), each wrapped in an HTML comment with a placeholder box shown
instead. To go live:

1. **Get an approved AdSense account.** Google requires a live site with real
   content and a privacy policy (already included here as `privacy.html`) before
   approving an account — this can't be done from localhost or a private repo.
2. Once approved, get your **Publisher ID** (`ca-pub-XXXXXXXXXXXXXXXX`) from the
   AdSense dashboard.
3. In `index.html`'s `<head>`, uncomment the `adsbygoogle.js` loader script and
   replace `ca-pub-XXXXXXXXXXXXXXXX` with your real Publisher ID.
4. For each `<div class="ad-slot">`, create a matching **Ad unit** in AdSense to
   get a `data-ad-slot` ID, then uncomment the `<ins class="adsbygoogle">` block
   and fill in your `data-ad-client` and `data-ad-slot` values. Remove or keep
   the `.ad-slot__placeholder` div as you like (it's just a visual fallback).
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
