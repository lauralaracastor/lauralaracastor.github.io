# lauralaracastor.github.io

Personal/academic website for Laura Lara-Castor (Postdoctoral Scholar, Institute for Health Metrics & Evaluation, University of Washington). Plain static HTML/CSS, no build step, deployed automatically via GitHub Pages.

## How it's hosted

- Repo name `lauralaracastor.github.io` → GitHub Pages serves it automatically from the `main` branch root at `https://lauralaracastor.github.io`. No `CNAME`, no `_config.yml`, no GitHub Actions workflow, no Jekyll — just static files served as-is.
- Remote: `git@github.com:lauralaracastor/lauralaracastor.github.io.git`
- To deploy a change: commit to `main` and push. Pages redeploys within ~1–2 minutes.

## File structure

```
index.html          Home / About Me (bio, affiliations, social links)
cv.html              Resume & CV download buttons
publications.html    List of publications (.card entries)
projects.html        Research projects (.card entries, some with placeholder GitHub links)
speaker.html         Speaking engagements (editable placeholder template)
media.html           Press coverage, grouped by paper
contact.html         Contact form (Formspree) + LinkedIn link
style.css            All site styling (single shared stylesheet)
assets/
  Laura_LaraCastor_Resume_20260203.pdf   Resume PDF (linked from cv.html)
  profile_pic2.jpg                        Headshot used on index.html (~1.7MB)
  profile_pic.jpg                         Unused alternate headshot (~900KB)
  profile.jpg                             Unused, 0 bytes — stray/broken file
```

**Known gap**: `cv.html` also links to `assets/Laura_LaraCastor_CV.pdf`, which does not exist in `assets/` — that download button is currently broken. Not yet fixed (out of scope of the last content update); add the PDF or remove the button when addressing it.

## Shared page anatomy

Every page follows the same skeleton — copy any existing page (`speaker.html` is a good minimal example) rather than writing one from scratch:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{Page Title}}</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
  <link rel="stylesheet" href="style.css">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
</head>
<body>

<nav>
  <a href="index.html">Home</a>
  <a href="cv.html">CV</a>
  <a href="publications.html">Publications</a>
  <a href="projects.html">Projects</a>
  <a href="speaker.html">Speaker</a>
  <a href="media.html">Media</a>
  <a href="contact.html">Contact</a>
</nav>

<main>
  <!-- page content -->
</main>

<footer>
  <!-- same footer-links block (Google Scholar, LinkedIn, GitHub, email) on every page -->
</footer>

</body>
</html>
```

Add `class="active"` to the `<nav>` link matching the current page. The footer's four icon links (Scholar SVG, LinkedIn, GitHub, email) are identical byte-for-byte across every page — copy them verbatim from any existing page.

## Design system (`style.css`)

- **Font**: Inter (Google Fonts), sans-serif
- **Accent color**: `#2a6f7d` (seafoam teal) — used for nav active state, links, headings, buttons
- **Background**: `#fafafa`; card/content surfaces are white
- **Nav**: sticky top bar, pill-shaped links, teal fill on hover/active
- **`.card`**: the core content block — white box, rounded corners, subtle shadow. Used for every list-style page (Publications, Projects, Speaker, Media). Optional `.card h3` (title) and `.card .meta` (muted gray subtitle line) for structured entries.
- **`.placeholder-note`**: small italic gray text (`#999`) — used to mark "coming soon" / not-yet-real content (e.g. unpublished GitHub repo links) without faking a real link.
- **`.media-group` / `.group-title`**: groups `.card` entries under a teal subheading — used on `media.html` to cluster press coverage by paper.
- **`.btn` / `.btn.secondary`**: teal / gray pill buttons — used for the CV download buttons.
- **`.contact-container` / `.contact-form`**: white card wrapping the Formspree contact form.
- Mobile breakpoint at `850px`: sidebar layout on `index.html` stacks vertically; nav font shrinks.

## Page content reference (for rebuilding)

### `index.html`
Two-column layout (`.home-layout`): left `.sidebar` has circular profile photo (`profile_pic2.jpg`), name, title ("PhD Nutritional Epidemiology & Data Science"), affiliation lines (Postdoctoral Scholar, IHME, University of Washington), and social icon row (Google Scholar SVG, LinkedIn, GitHub, email → `contact.html`). Right `.about-content` has an "About Me" `<h2>` and three bio paragraphs covering: (1) current IHME/GBD postdoc work on SBP–heart failure meta-analysis, (2) doctoral SSB research and its recognition (AHA fellowship, Nature Medicine/BMJ, NYT/NPR coverage, ASN awards), (3) prior role at Mexico's National Institute of Public Health and academic background (MS Boston University, BS Universidad de las Américas Puebla).

### `cv.html`
Single `<section>` with a short intro line and `.cv-buttons` containing two `.btn` download links: Resume (`assets/Laura_LaraCastor_Resume_20260203.pdf`, works) and CV (`assets/Laura_LaraCastor_CV.pdf`, **currently broken — file missing**).

### `publications.html`
`<h2>Publications</h2>` + an `<ol>` of nine `.card` entries (newest first isn't strictly enforced — currently ordered 2026 → 2019), each with authors, bold title, italic journal + volume/pages/year, and a linked DOI.

### `projects.html`
`<h2>Research Projects</h2>` + four `.card` entries, each with an `<h3>` title, a description paragraph, and a repo-status line:
1. SSB Intakes and Attributable Burdens — links to `publications.html`; placeholder-note "GitHub repo: coming soon"
2. Global Burden of Disease (GBD) Study — IHME postdoc work; placeholder-note
3. Global Dietary Database (GDD) — placeholder-note
4. Personal Website (this repo) — **real** link to `https://github.com/lauralaracastor/lauralaracastor.github.io`

### `speaker.html`
`<h2>Speaking</h2>` + intro line + three `.card` **template** entries with bracketed placeholders (`[Talk Title]`, `[Event / Conference Name], [City, Country]`, `[Month Year]`, `[Slides / video link]`) and an HTML comment explaining how to duplicate/edit them. Not real data yet — Laura fills these in herself as she compiles her talk history.

### `media.html`
`<h2>Media Coverage</h2>` + three `.media-group` blocks, ordered by publication year with the latest first, each with a `.group-title` and `.card` entries linking to real press coverage ordered by outlet prominence within the group:
- **SSB burden (Nature Medicine, 2025)** — 8 outlets: NYT, NPR, NPR Goats and Soda, US News, UPI, Healio, Tufts Now, Medical Xpress
- **SSB intake, children/adolescents (BMJ, 2024)** — 6 outlets: US News, Euronews, HealthDay, Medical Xpress, News-Medical, BMJ Group
- **SSB intake, adults (Nature Communications, 2023)** — 4 outlets: NPR, Tufts Now, EurekAlert!, News-Medical

Full links are in the file itself — don't retype them from memory if re-adding; copy from the current `media.html`. Altmetric.com blocks non-browser fetches (403 on every URL tested, including its public API), so this list was compiled via targeted web search rather than scraped from the Altmetric mention pages; there may be additional minor/aggregator outlets not included here by design (low-value SEO reposts were skipped in favor of primary/reputable coverage).

### `contact.html`
Intro line + LinkedIn link + a Formspree form (`action="https://formspree.io/f/xvzygbpz"`, POST) with Name, Email (`_replyto`), and Message fields.

## Rebuilding from scratch (if the repo is ever lost)

1. Create a new GitHub repo named exactly `lauralaracastor.github.io` (this name is what triggers GitHub Pages' user-site auto-deploy).
2. Recreate `style.css` using the design system section above as the spec (or pull it from a browser cache / the live site's dev tools if the repo history is truly gone — `view-source:https://lauralaracastor.github.io/style.css` works as long as the last deploy is still live).
3. Recreate each HTML page using the shared skeleton above, filling in the page-specific content from the "Page content reference" section.
4. Re-add `assets/` files: résumé PDF, `profile_pic2.jpg` headshot. Skip `profile_pic.jpg` and `profile.jpg` — both were unused dead weight in the original repo.
5. Commit to `main` and push — no build step, no CI, nothing else to configure.
6. Verify locally before pushing: `python3 -m http.server` from the repo root, then open `http://localhost:8000` and click through all seven nav links.
