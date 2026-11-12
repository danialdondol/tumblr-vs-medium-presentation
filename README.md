# Tumblr vs Medium — Presentation Deck

A single-file, 16:9 presentation comparing Tumblr and Medium for a five-person group. The deck is 19 slides: 18 presentation slides plus a source appendix. It needs no build step, package manager, or framework.

## Files

| File | Purpose |
|---|---|
| `index.html` | The complete deck, with inline CSS and JavaScript |
| `README.md` | This guide |

The only external resource is Google Fonts (Fraunces + Inter). If it is unavailable, the deck falls back to local serif and system fonts and still works offline.

---

## Presenting

1. Open `index.html` in a modern browser (Chrome, Edge, Safari, or Firefox).
2. Press **F** to enter fullscreen. In some browsers, click the page first if the browser requires a user gesture.
3. Use the arrow keys, Space, the on-screen buttons, or swipe on a touch screen.
4. Press **N** for the speaker notes panel. The notes follow the current slide.
5. Press **O** for the slide overview.
6. Press **Esc** to close the overview/notes or leave fullscreen.

The deck is built as a 16:9 stage that scales to the available window. On a phone held in portrait it will be letterboxed and small; a “Rotate your device” hint is shown. Landscape or a laptop/projector gives the intended experience.

### Keyboard shortcuts

| Key | Action |
|---|---|
| `→`, `↓`, `Space`, `Page Down` | Next slide |
| `←`, `↑`, `Page Up` | Previous slide |
| `Home` / `End` | First / last slide |
| `F` | Enter or exit fullscreen |
| `O` | Open or close the overview grid |
| `N` | Open or close speaker notes |
| `Esc` | Close overview/notes; exit fullscreen |
| Click | Use the toolbar buttons or any overview card |

### Direct links

Every slide has a URL hash: `index.html#1` through `index.html#19`. Opening a link with a hash starts on that slide. The hash updates as you navigate, so you can copy the address bar to share a specific slide.

### Speaker notes

Each slide has 2–3 short talking points in a hidden `<template class="slide-notes">`. Press **N** and the panel shows the current slide’s notes. You can keep notes open while presenting: the arrow keys still change slides, and the notes update automatically. Notes are hidden in print and in the overview.

---

## Editing the content

Open `index.html` in a plain text editor. All slides are in one `<main class="deck">` block.

### Group name, member names, and student IDs

Near the bottom of the file, inside the `<script>` block, find:

```js
const DECK_CONFIG = {
  groupName: "Group 5",
  members: [
    "Muhammad Danial bin Ibrahim",
    "Aiman Haqim",
    "Nadrah Izyan binti Shafi'e",
    "Siti Sara binti Mohd Azha",
    "Tuan Nurul Iman Izlin binti Tuan Sabri"
  ],
  studentIds: [
    "2026120427",
    "2026130001",
    "2026117533",
    "2026112435",
    "2026112587"
  ]
};
```

The values are inserted into the title slide and agenda automatically; the student IDs appear on both. Keep the quotation marks and commas, and keep the arrays in member order. To change the group name, edit `groupName`.

### Slide text

Each slide is a `<section class="slide ...">` with a `data-title`, `data-member-label`, and `data-member` attribute. Search for the visible heading (for example `Built for the reblog`) to jump to a slide, then edit the headings, paragraphs, cards, or table cells.

If you add or remove slides:

- Update the footer slide number (`<span class="foot-num">07</span>`) manually.
- Update the agenda slide ranges (`03–05`, etc.) manually.
- The progress bar, counter, URL hashes, and overview grid recalculate automatically from the number of slides.

### Speaker notes

Inside each slide, edit the `<template class="slide-notes">` list. Keep 2–3 bullet points for a comfortable speaking rhythm.

### Sources

Update the final slide if you change a fact, add a source, or replace a claim. Links are live in the browser. URLs are intentionally displayed in full for a printed handout.

### Colours and typography

The design tokens are in `:root` near the top of the file:

```css
--paper: #f4f1e9;
--ink: #171717;
--tumblr: #243b5a;
--medium: #1a8917;
```

Tumblr uses a deep navy accent; Medium uses its green accent over a neutral editorial base. The Google Fonts `<link>` can be removed if you want a completely local-only build; the fallback stack already works offline.

---

## Export to PDF

1. Open the deck in Chrome or Edge.
2. Press **Ctrl/Cmd + P**.
3. Choose **Save as PDF**.
4. Turn on **Background graphics**.
5. Use landscape orientation. The CSS declares a 13.333 × 7.5 in page (16:9) with zero margins, one slide per page.
6. Set Margins to **None** if your browser offers the option.

A test export produced 19 pages at 3.2 MB with the backgrounds intact. Brand colors and dark slides need “Background graphics” enabled. Safari’s print dialog is less consistent; Chrome or Edge gives the closest match to the on-screen design.

---

## Deploy on GitHub Pages

The deck is already a static site; `index.html` is the entry point.

### Option A — from the command line

```bash
cd path/to/the/deck
git init
git add index.html README.md
git commit -m "Add Tumblr vs Medium presentation"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main
```

Then:

1. Open the repository on GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**, then **Save**.
5. Wait for the Pages deployment to finish.

Your deck will be at:

```text
https://YOUR-USERNAME.github.io/YOUR-REPO/
```

Slide links look like:

```text
https://YOUR-USERNAME.github.io/YOUR-REPO/#13
```

### Option B — through the GitHub website

Create a new repository, upload `index.html` and `README.md`, then follow steps 2–5 above. No Jekyll configuration, build command, or `gh-pages` branch is needed.

---

## Notes and assumptions

- **Slide count:** the detailed outline names 18 presentation slides; the deck adds a final source appendix, for 19 total.
- **Group details:** the deck is configured for Group 5 with all five member names and student IDs. Edit `DECK_CONFIG` to change them.
- **Facts:** platform history, ownership, features, pricing, and audience claims were checked against official help pages and contemporaneous reporting in November 2026. The 60% “creative” figure is Tumblr’s own advertising audience research and is labelled as such on the slide.
- **Monetization:** Tumblr is described as ad-led with limited direct creator pay; Medium is described as reader-subscription-led with its Partner Program. These are comparative characterizations, not claims that creator earnings are impossible on Tumblr.
- **Fullscreen:** standard browsers support the Fullscreen API. iOS Safari may block element fullscreen; the deck shows a short message instead of failing silently.
- **No tracking, no analytics, no external scripts.** The only network request is for Google Fonts.

## Browser support

Modern Chrome, Edge, Firefox, and Safari. The deck uses container-query units (`cqw`) for precise 16:9 scaling; current evergreen browsers support them. Older browsers fall back to readable system fonts and may lose some of the intended sizing.
