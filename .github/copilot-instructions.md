## Quick context

- This repository is a single-page static site. The main content is in `index.html` (and `README.md` contains the same HTML). There are no build tools, package.json, or tests.
- The HTML file contains inline CSS (in the `<head>`) and inline JavaScript (at the end of `<body>`). Changes are usually done directly in `index.html`.

## Big-picture architecture

- Single-file static site: markup, styles, and scripts are colocated for simplicity.
- No server-side code, no frameworks, no bundlers. Deploy by publishing the static files to a static host (Netlify, GitHub Pages, S3, etc.).
- Data flow is purely client-side: the booking form is handled by the inline JS (currently shows an alert). There are no API integrations in the repo.

## What a coding agent should assume/do first

1. Open `index.html` in a browser for a quick preview. You can run a local static server from the repo root:

   python3 -m http.server 8000

   Then visit http://localhost:8000/ in the browser.

2. Inspect and edit `index.html`. Typical edits include:
   - Change site text (title `<title>`, header `<h1>`, hero copy) in the HTML body.
   - Update visual styles in the `<style>` block at the top of the file.
   - Modify client logic in the `<script>` block at the bottom (form submission, particle animation, smooth scroll, etc.).

3. For larger changes, prefer extracting CSS/JS to new files (e.g., `styles.css`, `app.js`) and link them from `index.html`. Keep changes small and test in the browser.

## Project-specific patterns & examples

- Inline styles: The repo places all styling inside `<style>` in `index.html`. When adjusting layout/typography, modify the CSS variables and grid sections inside that block.
- JS placement: Behavioral code (particles, smooth scrolling, form submit handler) is at the bottom of `index.html`. Example: the booking form's submit handler currently prevents default and uses alert to simulate submission.
-- Sections identified by IDs: home, about, services, gallery, booking — use these IDs when adding anchors or linking behavior (see `index.html`).

## README duplication note

- `README.md` currently contains the same full HTML as `index.html`. This repository keeps a copy of the site in both places. When editing the site, prefer editing `index.html` and then sync or update `README.md` as needed.
- Recommendations:
   - Keep `README.md` as a short description that links to `index.html` and contains quick preview commands, or
   - If you need the README to include the HTML (for a specific reason), document why and add a short maintenance note at the top explaining how to regenerate it.
   - Suggested PR message when changing both: "Sync `README.md` with `index.html` — updated [area(s)]".

## Build, test, debug workflows (discoverable)

- Local preview: serve files and open the URL (see above). No build step required.
- Debugging: use browser devtools (Elements, Console) for CSS/JS changes. After edits, refresh the page.
- Linting/tests: none present. Do not add heavy toolchains without owner consent; prefer minimal, reversible changes.

## Deploying

- A GitHub Actions workflow is included at `.github/workflows/deploy.yml` to publish the site to the `gh-pages` branch on pushes to `main` using `peaceiris/actions-gh-pages`.
- After merging to `main` the action will deploy the repository root (including `index.html`, `styles.css`, and `app.js`) to the `gh-pages` branch. A `.nojekyll` file is included to prevent Jekyll processing.
- You can preview locally before pushing with:

```bash
python3 -m http.server 8000
# open http://localhost:8000/
```

Notes:
- The action uses the built-in `GITHUB_TOKEN` so no additional secrets are required.
- If you prefer deploying to Netlify or another host, keep the repo root as the publish directory and configure the host to use the repository root.

## Custom domain / CNAME

- This repo can be served from a custom domain using a `CNAME` file at the repo root. I added `CNAME` with the value `www.ddmlight.com`.
- DNS steps you must perform at your DNS provider for `www.ddmlight.com` (recommended):
   - Create a CNAME record for `www` pointing to `ddmoonlight69.github.io`.
   - No A records required for the `www` subdomain.

- If you want the apex domain (`ddmlight.com`) to redirect to `www.ddmlight.com`, add the following A records for the apex pointing to GitHub Pages IPs:
   - 185.199.108.153
   - 185.199.109.153
   - 185.199.110.153
   - 185.199.111.153

- After DNS changes propagate (can take minutes to 48 hours), GitHub Pages will serve the site from your custom domain. You can verify in the repository Settings → Pages.


## Integration points & external dependencies

- There are no external service integrations or dependency manifests in the repository. All behavior is local to the page.
- If you add third-party libraries (e.g., for forms or analytics), add them as external script tags and document the change in the PR.

## Safety & content notes (important)

- The content is adult-oriented. When modifying copy or adding content, avoid introducing new explicit sexual text beyond what exists. Follow platform and legal content policies.
- When generating text, prefer neutral, descriptive language unless the repository owner explicitly requests more explicit content.

## PR / commit guidance for an AI agent

- Make small, focused changes with clear commit messages (e.g., `extract CSS to styles.css`, `fix booking form handler`).
- Include a short manual test checklist in the PR description (preview URL, steps to reproduce, screenshots if UI changed).

## Files to check when touching major areas

- `index.html` — primary: markup, styles, behavior.
- `README.md` — contains same HTML; keep in sync if you update `index.html` or remove duplication.

---
If anything in this file is unclear or you'd like more specific examples (for instance, splitting inline JS into a module and a small test harness), tell me which area to expand and I will iterate.
