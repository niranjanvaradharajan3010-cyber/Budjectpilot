# BudgetPilot — GitHub Pages deployment

This is a static household budget and trip-planning app. `index.html` is the entry point. No installation, build command, backend, development server, API key, or environment variables are required.

## Files to upload

Upload these files directly to the **root of your GitHub repository**:

```text
REPOSITORY-NAME/
├── index.html
├── .nojekyll
└── README.md       (optional documentation)
```

Do not upload the enclosing `Website for Financial handeling` folder as another folder inside the repository. Do not upload `.git` or any temporary testing files. Include `.nojekyll`, even if your file picker hides dotfiles.

## Enable GitHub Pages

1. Commit the uploaded files to your repository's `main` branch.
2. Open the repository's **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select **main** and **/(root)**, then save.
5. Wait for the Pages deployment to finish. Open the URL GitHub displays, usually `https://USERNAME.github.io/REPOSITORY-NAME/`.

If your branch has a different name, select that branch instead. No custom Actions workflow or Jekyll build is needed. `.nojekyll` marks this as a plain static site.

[GitHub's publishing-source instructions](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

## Subdirectory compatibility and dependencies

- All application JavaScript and custom CSS are inside `index.html`.
- Icons are inline SVG. There are no image downloads, local imports, local fonts, or separate asset folders.
- The three views switch in place; navigation does not request routes such as `/dashboard`. A repository subdirectory therefore needs no routing fallback, base URL setting, or URL rewrite.
- There are no `file:`, localhost, Windows drive, or root-relative asset references.
- Tailwind retains the existing HTTPS dependency, `https://cdn.tailwindcss.com`. This is a public external CDN, not a local-server dependency. It requires network access; the app's custom styling is also inline. The existing Tailwind Play CDN can emit a production-use warning, which is distinct from an application JavaScript error.
- The design, app features, calculations, and data storage key are unchanged by the deployment preparation.

## Saved data

Household data and trips stay in browser `localStorage`. HTTPS GitHub Pages supports this browser API. Storage must be allowed in the visitor's browser; the app displays a warning when it cannot save.

Existing data saved while opening a local file does **not** automatically transfer to the GitHub Pages origin. Storage also does not sync across devices or browsers. GitHub project sites under the same `USERNAME.github.io` hostname share an origin, so copies of BudgetPilot under that hostname currently share its existing storage key.

## Validation performed

- JavaScript syntax check passed.
- All 31 isolated JavaScript regression test groups passed, including Dashboard calculations, Smart Recommendations, Trip Planner, three-view navigation, subscriptions, salary migration, saved trips, simulated localStorage recovery, reset, and invalid inputs.
- Source paths and external dependencies were audited for repository-subdirectory compatibility. All 31 regression groups also passed with the simulated page base set to `https://USERNAME.github.io/REPOSITORY-NAME/`.
- The Tailwind CDN returned HTTP 200 with JavaScript content during the HTTPS reachability check. Actual browser execution of the CDN script remains unverified.
- Browser execution and actual console/CSS rendering were not verified: the browser tool blocked access to the local file. The regression checks use a simulated DOM and storage, not a real browser.

After publishing, open the displayed Pages URL and check all three tabs, change a value, reload to confirm persistence, and inspect the browser console and Tailwind loading. The GitHub deployment itself has not been performed by this preparation.
