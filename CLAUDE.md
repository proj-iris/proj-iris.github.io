# IRIS website

Static GitHub Pages site for IRIS, the JST NEXUS Japan–Vietnam project on a low-power event-driven AI system-on-chip (grant JPMJNX26D3). `index.html` is the whole site: plain HTML/CSS with a small inline script, no libraries or build step.

## Layout

- A sticky header with the text "IRIS" at the top left and a menu of in-page links. There is no logo in the header. Below 760px the menu collapses behind a "Menu" button.
- One `<section id="...">` per menu entry inside `main`. The script highlights the menu link of the section in view.
- **To add a section:** add a `<section id="name">` in `main` and a matching `<li><a href="#name">Label</a></li>` in the menu.
- Palette: `#b394df`, `#c5a6eb`, `#f5efff` on `#171321` (CSS variables on `:root`).
- The footer credit line (E3Computing Group and "Site built with Claude Code") is hidden until the footer scrolls into view, then decodes left to right through random katakana and digits (the last part of the second script). With reduced motion or no JavaScript it shows plainly.
- Background: the spiking-neuron animation (first script in `index.html`) runs in `.backdrop`, fixed in the middle of the window behind all content and faded by the wrapper's `opacity`. It draws radial fibers around the eye (`iris-logo-transparent-no-text.svg`, whose dots match the `LOGO` array) on `#field` and spikes over the eye on `#spark`. With reduced motion it renders one still frame. It was the full-screen hero until commit 650345c; on 2026-11-10 the hero was removed and the animation came back as this background.

## Build and deploy

There is no build step. GitHub Pages serves the repo root of `main` at the custom domain in `CNAME`, so pushing to `main` publishes the site within a minute or two.

1. Edit `index.html` (and add any images next to it).
2. Preview locally: `python3 -m http.server 8000` in this folder, then open http://localhost:8000. Opening `index.html` directly in a browser also works.
3. Check phone width (about 390px) as well as desktop. For a headless check: `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --screenshot=out.png --window-size=1280,2400 file://$PWD/index.html`. Headless Chrome won't go below about 500px wide, so to test a phone, load the page in a 390px `<iframe>` in a scratch HTML file.
4. Commit and push to `main` of `proj-iris/proj-iris.github.io`.
5. This repo is a submodule of `proj-iris/project-management` (at `website/`). After pushing here, commit the new submodule pointer there too (`git add website`).

`_site/` is local preview output from Jekyll or an editor plugin; do not commit it. This repo is public: everything in it, including this file and commit messages, can be read by anyone. Internal project details stay in the coordination repo.

## Content

Project facts and the member list come from the coordination repo (`proj-iris/project-management`, mainly `docs/team.md`); keep them in sync with it. Emails, admin staff and unconfirmed ECR candidates are not listed. The Ph.D. call has a deadline (2026-11-20 for the April 2027 start), so update or remove the "Join us" box once it passes. `phd-call.pdf` is the published call: a copy of the PDF made from `training/ecr-call.md` in the coordination repo. Replace it whenever the call changes, and keep the stipend and research-budget figures in the "Join us" box in step with it. Only figures already in the public call go on the site; project budgets do not.
