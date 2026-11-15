# Rhuyee's Roost

A responsive static website for Haris Malik's professional tabletop roleplaying services and
original work. It is designed for low-maintenance hosting on GitHub Pages with no build step.

## Before publishing

The site deliberately labels every unknown detail with square-bracket placeholders. Search the
repository for `[` to find most content that still needs Haris's input. At minimum, replace:

- Haris's time zone, location, and service area
- In-person availability, group size limits, accessibility practices, and safety tools
- Service-specific quotes, booking terms, cancellation/refund policy, and any required legal language
- Business email, social profile, and any additional storefront links
- Original works, descriptions, cover art, formats, and purchase/download links

The testimonials section contains short, attributed excerpts from Erica, Sarah, and Yithaja's
public StartPlaying reviews, checked against Haris's profile on November 12, 2026.
Keep excerpts faithful to their source and retain the attribution and source links.

Online games link to [Haris's StartPlaying profile](https://startplaying.games/gm/rhuyee).
The contact section also includes his [StartPlaying review link](https://startplaying.games/gm/rhuyee/review).
Keep these links current if his profile changes.

The services section displays the **$35 per session** online rate listed on Haris's
StartPlaying profile, checked on November 12, 2026. The profile does not specify whether this
is per player or per group, or establish separate one-shot, campaign, or private-event rates.
Keep that qualification and confirm service-specific pricing before booking. Update the rate
in `index.html` when his listed price changes.

## Contact form

The inquiry form is connected to the Formspree endpoint configured in `index.html`. Manage its
notification recipient, Discord integration, spam protection, redirects, and data-retention
settings from the [Formspree dashboard](https://formspree.io/).

If the form is replaced later, update its `action` in `index.html`:

```html
action="https://formspree.io/f/your-form-id"
```

The JavaScript retains a safeguard that blocks submission if the endpoint is ever reset to
`REPLACE_WITH_FORM_ID`.

## Preview locally

Because this is a static site, any local HTTP server works. From the repository root:

```powershell
python -m http.server 8000
```

Then open <http://localhost:8000>. A server is preferable to opening `index.html` directly because
it mirrors how GitHub Pages serves asset paths.

## Biography page

`biography.html` is a standalone page linked from the homepage navigation, About teaser,
and footer. It contains Harry's supplied biography, campaign descriptions, and full list of
game systems, with light spelling and grammar corrections. Keep his first-person voice and
table expectations intact when editing. Links to adventures, the library, FAQ, and booking
return to the corresponding sections of `index.html`.

Preview it at <http://localhost:8000/biography.html>. Like the homepage, it deploys directly
to GitHub Pages with no build step.

## Customize content and design

- Page content and metadata: `index.html` and `biography.html`
- Color, typography, layout, and responsive styles: `styles.css`
- Navigation and safe form-placeholder behavior: `script.js`
- Original owl favicon/mark: `assets/favicon.svg`
- Harry's biography portrait: `assets/harry-portrait.jpg`
- Social sharing image: `assets/social-card.svg`

The current fonts are loaded from Google Fonts. For a fully self-hosted site, download properly
licensed font files, commit them under `assets/fonts/`, and replace the `@import` in `styles.css`
with local `@font-face` declarations.

If the GitHub organization or repository name changes, update the `og:url` and `og:image` values in
both HTML pages.

## Deploy to GitHub Pages

The workflow at `.github/workflows/pages.yml` publishes the static HTML, CSS, JavaScript, and
assets whenever `main` is updated. It can also be run manually from the Actions tab on `main`.
The `gh-pages` branch stores the published site and its PR previews; GitHub Actions deploys
that combined site using the official Pages artifact workflow. Keep **GitHub Actions**, not
deployment from a branch, selected as the Pages source.

After merging the site:

1. Open the repository **Settings → Pages**.
2. Under **Build and deployment**, select **GitHub Actions** as the source.
3. Run the **Deploy GitHub Pages site** workflow if it did not start automatically.
4. Confirm the published URL is <https://jada-not-java.github.io/rhuyees-roost/>.

### Pull request previews

Same-repository PRs targeting `main` receive a live preview at
`https://jada-not-java.github.io/rhuyees-roost/pr-preview/pr-<number>/`. The workflow updates
it when the PR opens, changes, or reopens, and removes its files when the PR closes or merges.
A single bot comment links to the preview and is updated only after Pages deployment succeeds.

Production stays at the root URL. Production updates preserve the `pr-preview/` directory,
and preview updates only change their own PR directory. Publishing runs are serialized to
avoid competing Pages deployments. Preview HTML tells search engines not to index it.
Previews are public and include the same working contact form as production.

Fork PRs still run validation but do not publish previews because their tokens cannot write
to this repository. This workflow deliberately uses `pull_request`, not `pull_request_target`.
Only allow trusted contributors to create same-repository branches.

Under **Settings → Environments → github-pages**, ensure deployment rules allow both `main`
and pull request refs if branch restrictions are enabled. Do not add a deployment approval
requirement if previews should publish automatically. Before the initial site PR is merged,
the preview can be available while the production root is still empty.

## Accessibility and maintenance

The site includes semantic landmarks, a skip link, visible keyboard focus, labeled inputs,
responsive navigation, strong contrast, and reduced-motion handling. When editing:

- Keep heading levels in order.
- Add meaningful alternative text to informative images; use an empty `alt` for decorative images.
- Test keyboard navigation and the form at narrow and wide viewport sizes.
- Never publish placeholder claims, testimonials, prices, or policies as if they were final.
- Optimize new images before committing them.
