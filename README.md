# rubendominguezdiaz.github.io

My personal academic website, including the PDFs of my papers. Plain HTML and
CSS, no JavaScript, no build step. Published by GitHub Pages from the
repository root.

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
papers/
└── <n>_<shorttitle>/
    └── v<year>[_<tag>]_<shorttitle>.pdf
```

**This repository is the only place papers live.** The older `papers_PDF`
repository is frozen: it still serves the URLs that were shared before the
move, but nothing new goes there and its copies are not maintained.

Everything here is public, whether or not it is linked from a page. Papers
that must not be distributed do not belong in this repository at all.

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

1. Create `papers/<n>_<shorttitle>/` and put the PDF in it, named
   `v<year>_<shorttitle>.pdf`. Add a tag between the two when the version was
   made for a particular audience or milestone: the venue (`BdE`, `CEMFI`,
   `ECB`, `EER`) or its status (`published`).
2. Copy this block into `index.html`, under the right `<h2>`, and edit it.
   Drop any line that does not apply.

```html
    <div class="item">
      <h3><a href="papers/FOLDER/FILE.pdf" target="_blank" rel="noopener">Paper Title</a></h3>
      <p class="authors">with Coauthor One and Coauthor Two</p>
      <p class="status">R&amp;R at Journal Name</p>
      <details>
        <summary>Abstract</summary>
        <p class="abstract">Abstract text.</p>
      </details>
    </div>
```

3. Commit and push.

Two things that will bite otherwise:

- Write `&` as `&amp;` — so `R&amp;R`, not `R&R`.
- Keep paper links **relative** (`papers/...`, not `https://...`). Relative
  links work unchanged on both the github.io address and the custom domain.

## Updating an existing paper

Replace the PDF, keeping the same filename, then commit and push. The URL does
not change, so nothing else needs editing and any link already shared keeps
working. Only a change of year justifies a rename — and that breaks shared
links, so also update `index.html`.

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
