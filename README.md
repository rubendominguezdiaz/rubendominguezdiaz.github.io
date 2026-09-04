# rubendominguezdiaz.github.io

My personal academic website. Plain HTML and CSS, no JavaScript, no build
step. Published by GitHub Pages from the repository root.

Live at <https://rubendominguezdiaz.github.io/>

## Files

```
index.html     home: bio, working papers, publications, work in progress
contact.html   contact page
style.css      all styling; the palette lives in the :root block at the top
assets/
├── photo.jpg  headshot (800x600, web-sized)
├── cv.pdf     CV
└── fonts/     Erewhon webfont (SIL Open Font License)
```

## Two repositories

The **PDFs live in a separate repository**, `papers_PDF`, and are served from
`https://rubendominguezdiaz.github.io/papers_PDF/papers/...`. This site only
links to them.

So adding a paper is two steps in two places:

1. Put the PDF in `papers_PDF` and push it there.
2. Add the entry to `index.html` here and push.

Updating an existing PDF only needs step 1 — the link does not change.

## Publishing

Nothing is live until it is pushed. From this folder:

```
git add -A
git commit -m "<what changed>"
git push
```

The site updates about a minute later. Browsers cache CSS and PDFs for around
ten minutes, so press Ctrl+F5 before concluding a change did not work.

## Adding a paper

Copy this block into `index.html`, under the right `<h2>` heading, and edit it.
Drop any line that does not apply — a solo-authored paper has no `authors`
line, an unsubmitted one has no `status` line.

```html
    <div class="item">
      <h3><a href="https://rubendominguezdiaz.github.io/papers_PDF/papers/FOLDER/FILE.pdf" target="_blank" rel="noopener">Paper Title</a></h3>
      <p class="authors">with Coauthor One and Coauthor Two</p>
      <p class="status">R&amp;R at Journal Name</p>
      <details>
        <summary>Abstract</summary>
        <p class="abstract">Abstract text.</p>
      </details>
    </div>
```

Two things that will bite otherwise:

- Write `&` as `&amp;` — so `R&amp;R`, not `R&R`.
- Keep `target="_blank" rel="noopener"` so the PDF opens in a new tab.

## When a paper gets published

Move its whole `<div class="item">` block from Working Papers up to
Publications, then:

- change the link from the PDF to the journal DOI,
- replace the `status` line with `Journal Name, Year`,
- keep the abstract, but check it against the published version.

## Editing the bio or contact details

The bio is the four `<p class="hero-subtitle">` paragraphs near the top of
`index.html`. The contact page is `contact.html`. Both carry the email
address, so change it in both places.

## Changing colours

Every colour is a variable in the `:root` block at the top of `style.css`.
Change it there and it applies everywhere.

Check contrast if you change text or background colours: body text should be
at least 4.5:1 against its background (WCAG AA). The current palette is well
clear of that.
