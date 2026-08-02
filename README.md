# Tyler Kometani — Portfolio Website

A static portfolio site (semantic HTML, modern CSS, vanilla JS — no build step, no framework) built to be hosted for free on GitHub Pages.

## File structure

```
/
├── index.html                 Homepage — hero, about, featured project, other projects, capabilities, experience, education, contact
├── styles.css                 All styling (CSS variables at the top define the design tokens)
├── script.js                  Mobile menu behavior + footer year
├── 404.html                   Custom not-found page
├── README.md                  This file
├── assets/
│   ├── images/                Project photos (bench-setup-1.jpg, bench-setup-2.jpg, etc.)
│   ├── diagrams/               Block diagram / FSM diagram images
│   ├── documents/             Put resume.pdf here
│   └── icons/                 favicon.svg
└── projects/
    └── fpga-camera.html        Full case study for the flagship FPGA project
```

## Previewing locally

No build step is required. Either:

- Double-click `index.html` to open it directly in a browser, or
- Run a tiny local server from this folder so relative paths behave exactly like they will on GitHub Pages:
  ```
  python3 -m http.server 8000
  ```
  then visit `http://localhost:8000`.

## Publishing on GitHub Pages

1. Push this folder to a GitHub repository (e.g. `tkometani0512.github.io` for a root-level site, or any repo name for a project site).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch," pick the `main` branch and the `/ (root)` folder.
4. Save. GitHub will publish the site at `https://<username>.github.io/` (or `https://<username>.github.io/<repo-name>/` for a project repo).

If you use a project-repo URL (with a path segment), double-check that all the relative links (e.g. `projects/fpga-camera.html`, `assets/...`) still resolve — they're written as relative paths so they should work either way, but it's worth a click-through after the first deploy.

## Adding your résumé

Drop your résumé PDF into `assets/documents/` and name it `resume.pdf`. Every "Download Résumé" button already points to `assets/documents/resume.pdf` (or `../assets/documents/resume.pdf` from the project subpage), so no other changes are needed.

## Replacing images

- **Project photos**: replace files in `assets/images/` and update the `src` attribute on the corresponding `<img>` tag. Keep filenames descriptive (e.g. `water-turret-cad.jpg`) and update the `alt` text to describe what's actually in the photo.
- **Diagrams**: `assets/diagrams/block-diagram.png` and `assets/diagrams/capture-fsm.png` are pulled directly from the GitHub repository. If you regenerate these diagrams, drop the new PNGs in the same location with the same filenames, or update the `src` paths in `projects/fpga-camera.html`.
- Avoid stretching a low-resolution image — if you only have a small crop, either source a higher-resolution original or leave a placeholder rather than enlarging it.

## Updating project text

All project copy lives directly in the HTML:
- The five "other projects" cards are in `index.html` inside `<section id="projects">`.
- The flagship FPGA project summary is in `index.html` inside `<section id="featured-project">`; the full write-up is in `projects/fpga-camera.html`.

Search for `[ADD INFORMATION]`, `[CONFIRM DATE]`, `[ADD TEST RESULT]`, `[ADD GITHUB LINK]`, and `[CONFIRM CAPTION]` — these mark every spot that needs a fact from your portfolio PDF or résumé before publishing. A quick way to find them all:
```
grep -rn "ADD INFORMATION\|CONFIRM\|ADD TEST RESULT\|ADD GITHUB LINK" index.html projects/*.html
```

## Adding another project

Copy one of the existing `<article class="project-card">` blocks in `index.html`, replace the content, and give the `<details class="card-details">` block its own expanded write-up. If the project deserves its own full case-study page, duplicate `projects/fpga-camera.html` as a starting template (it already has the breadcrumb, table of contents, figure, code-block, and callout styles you'll likely reuse).

## Updating social links

Email, GitHub, and LinkedIn links appear in three places: the header/mobile-menu résumé button area, the hero section, and the contact section/footer. All use the same URLs (`mailto:tkometani0512@gmail.com`, `https://github.com/tkometani0512`, `https://www.linkedin.com/in/tyler-kometani-47664233b`) — update all instances if any of these change.

## Connecting a custom domain later

1. Buy a domain from any registrar.
2. Add a `CNAME` file at the repo root containing just your domain (e.g. `tylerkometani.com`).
3. At your registrar, add a `CNAME` record pointing your domain (or `www` subdomain) to `<username>.github.io`, or use the four GitHub Pages A records if pointing the apex domain directly.
4. Back in **Settings → Pages**, enter the custom domain and enable "Enforce HTTPS" once DNS has propagated.
