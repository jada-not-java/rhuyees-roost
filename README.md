# Rhuyee's Roost

A responsive static website for Haris Malik's professional tabletop roleplaying services and
original work. It is designed for low-maintenance hosting on GitHub Pages with no build step.

## Before publishing

The site deliberately labels every unknown detail with square-bracket placeholders. Search the
repository for `[` to find most content that still needs Haris's input. At minimum, replace:

- Haris's bio, experience, game systems, time zone, location, and service area
- Online/in-person availability, group size limits, accessibility practices, and safety tools
- Prices, booking terms, cancellation/refund policy, and any required legal language
- Business email, social profile, booking/storefront links, and approved testimonials
- Original works, descriptions, cover art, formats, and purchase/download links

Do not remove the placeholder notice from the testimonial section until genuine, approved quotes
are available.

## Connect the contact form

The form is intentionally disabled while its placeholder endpoint is present, so visitors cannot
mistake an unconfigured form for a successful submission.

1. Create a form at [Formspree](https://formspree.io/) and copy its form ID.
2. In `index.html`, replace `REPLACE_WITH_FORM_ID` with that ID:

   ```html
   action="https://formspree.io/f/your-form-id"
   ```

3. Remove the visible `form-banner` block after testing a real submission.
4. Configure Formspree's notification recipient, spam protection, redirect, and data-retention
   settings as appropriate.

That single endpoint replacement activates normal Formspree submission. The JavaScript only blocks
submission when the placeholder ID is still present.

## Preview locally

Because this is a static site, any local HTTP server works. From the repository root:

```powershell
python -m http.server 8000
```

Then open <http://localhost:8000>. A server is preferable to opening `index.html` directly because
it mirrors how GitHub Pages serves asset paths.

## Customize content and design

- Page content and metadata: `index.html`
- Color, typography, layout, and responsive styles: `styles.css`
- Navigation and safe form-placeholder behavior: `script.js`
- Original owl favicon/mark: `assets/favicon.svg`
- Social sharing image: `assets/social-card.svg`

The current fonts are loaded from Google Fonts. For a fully self-hosted site, download properly
licensed font files, commit them under `assets/fonts/`, and replace the `@import` in `styles.css`
with local `@font-face` declarations.

If the GitHub organization or repository name changes, update the `og:url` and `og:image` values in
`index.html`.

## Deploy to GitHub Pages

The workflow at `.github/workflows/pages.yml` deploys the repository root whenever `main` is
updated. It can also be run manually from the Actions tab.

After merging the site:

1. Open the repository **Settings → Pages**.
2. Under **Build and deployment**, select **GitHub Actions** as the source.
3. Run the **Deploy GitHub Pages site** workflow if it did not start automatically.
4. Confirm the published URL is <https://jada-not-java.github.io/rhuyees-roost/>.

Pull requests run a lightweight validation job but do not deploy.

## Accessibility and maintenance

The site includes semantic landmarks, a skip link, visible keyboard focus, labeled inputs,
responsive navigation, strong contrast, and reduced-motion handling. When editing:

- Keep heading levels in order.
- Add meaningful alternative text to informative images; use an empty `alt` for decorative images.
- Test keyboard navigation and the form at narrow and wide viewport sizes.
- Never publish placeholder claims, testimonials, prices, or policies as if they were final.
- Optimize new images before committing them.
