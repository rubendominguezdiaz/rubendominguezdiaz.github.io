# rubendominguezdiaz.github.io

Personal academic website of Rubén Domínguez-Díaz, including the PDFs of all
papers. Live at <https://rubendominguezdiaz.github.io/>.

This file is the complete maintenance manual. It is written for two readers:
the site owner, who does not write HTML, and any AI assistant asked to make a
change. **If you are an assistant, read [For AI assistants](#for-ai-assistants)
at the bottom before editing anything.**

---

## 1. How the site works

Plain HTML and CSS. **No JavaScript, no framework, no build step.** The files
in this repository are exactly what visitors receive.

GitHub Pages publishes the repository root. Pushing to the `main` branch makes
the change live in roughly one minute. There is nothing to compile and no
server to restart.

Because there is no build step, a mistake in the HTML shows up as a broken
page rather than an error message. Nothing validates the file before it goes
out. This is the main risk to be aware of.

---

## 2. What is where

```
index.html            Home page: bio, working papers, publications, work in progress
contact.html          Contact page
style.css             All styling. Colours are variables at the very top
README.md             This file
.nojekyll             Tells GitHub to publish files as-is. Do not delete
.gitignore            Keeps the camera-original photo out of the repository

assets/
├── photo.jpg         Headshot, 800x600, ~60 KB
├── cv.pdf            The CV that the CV button links to
└── fonts/            Erewhon webfont, four files, SIL Open Font License
    └── README.txt    Font attribution and licence note

papers/
└── <n>_<shorttitle>/          One folder per paper, numbered
    └── v<year>[_<tag>]_<shorttitle>.pdf
```

Everything in this repository is **public**, whether or not a page links to
it. Papers that must not be distributed do not belong here at all.

### Paper file naming

Folders are `<number>_<shorttitle>`, numbered in the order papers were added:
`5_defencespending`, `7_ONKIOtariffsECB`.

Files are `v<year>_<shorttitle>.pdf`. Insert a tag between the year and the
title when a version was produced for a particular audience or milestone —
the venue or institution (`BdE`, `CEMFI`, `ECB`, `EER`) or its status
(`published`):

```
papers/5_defencespending/v2026_defspending.pdf
papers/4_ONKIO/v2026_EER_ONKIO.pdf
papers/9_EGGEMenergy/v2026_EGGEMenergia.pdf
```

A plain `v<year>_<shorttitle>.pdf` is the general working version for that
year.

### The retired `papers_PDF` repository

The papers briefly lived in a separate repository, `papers_PDF`, and were
served from `/papers_PDF/papers/...`. That repository was deleted on
5 September 2026, so those URLs no longer resolve. This repository is the only
place papers live.

---

## 3. Publishing a change

Nothing is live until it is pushed. There are two ways to do it.

### Option A — on github.com, no software needed

1. Go to <https://github.com/rubendominguezdiaz/rubendominguezdiaz.github.io>
2. Click the file to change, then the pencil icon (**Edit this file**).
3. Make the edit.
4. Scroll down, write a short description in the commit box, click
   **Commit changes**.

To upload a file (a new PDF, a new photo): open the folder, click
**Add file → Upload files**, drag it in, then **Commit changes**.

To create a new folder: **Add file → Create new file**, and type
`papers/10_newpaper/placeholder.txt` in the name box — typing a `/` creates
the folder.

### Option B — locally with git

From `C:\Users\q32333\Dropbox\5_Research\00_PDFs_papers\rubendominguezdiaz.github.io`:

```
git add -A
git commit -m "what changed"
git push
```

### After publishing

The site rebuilds in about a minute. Browsers and GitHub's cache hold onto CSS
and PDFs for roughly ten minutes, so **press Ctrl+F5** to force a fresh copy
before concluding a change did not work. Most "it didn't work" moments are
this.

---

## 4. Task recipes

### 4.1 Update an existing paper (new draft of the same paper)

The easy case. **No HTML involved.**

1. Replace the PDF in `papers/<folder>/`, **keeping the filename exactly the
   same**.
2. Publish.

The URL does not change, so the website needs no edit and any link already
shared — on a CV, in an email, on a coauthor's page — keeps working.

The one exception is a change of year, e.g. `v2026_defspending.pdf` becoming
`v2027_defspending.pdf`. That changes the URL, so the link in `index.html`
must be updated too, and any link shared elsewhere will break. Renaming for
the sake of a new year is optional; keeping the old filename is perfectly
fine.

### 4.2 Add a new paper

This is the only task that involves editing HTML.

**Step 1 — add the PDF.** Create `papers/<n>_<shorttitle>/` using the next
number, and put the PDF inside, named per the convention above.

**Step 2 — add the entry.** Open `index.html`, find the right `<h2>` heading
(`Working Papers`, `Publications`, or `Work in Progress`), and paste this
block among the others under it. Papers appear in the order they appear in the
file.

```html
    <div class="item">
      <h3><a href="papers/FOLDER/FILE.pdf" target="_blank" rel="noopener">Paper Title</a></h3>
      <p class="authors">with Coauthor One and Coauthor Two</p>
      <p class="status">R&amp;R at Journal Name</p>
      <details>
        <summary>Abstract</summary>
        <p class="abstract">Abstract text goes here.</p>
      </details>
    </div>
```

Replace `FOLDER/FILE.pdf`, the title, the coauthors, the status, and the
abstract. **Delete whole lines that do not apply** — a solo-authored paper has
no `authors` line; a paper not under review has no `status` line; a paper with
no abstract has no `<details>` block.

**Step 3 — publish.**

### 4.3 Move a paper to Publications

When a paper is accepted:

1. Cut its entire `<div class="item">` block, from `<div class="item">` to its
   closing `</div>`, and paste it under the `<h2>Publications</h2>` heading.
2. Change the link from the local PDF to the journal DOI, i.e. replace
   `href="papers/..."` with `href="https://doi.org/..."`.
3. Replace the `status` line with the journal and year:
   `<p class="status">Journal Name, 2027</p>`
4. Check the abstract against the published version.
5. Publish.

The PDF can stay in `papers/` — nothing links to it, but the URL keeps working
for anyone who has it.

### 4.4 Remove a paper

Delete its whole `<div class="item">` block from `index.html`. Leave the PDF in
`papers/` unless it must genuinely disappear, since deleting it breaks any
link already shared.

### 4.5 Edit the bio

The bio is the four paragraphs near the top of `index.html`, each on its own
line, each looking like:

```html
      <p class="hero-subtitle">I am Research Economist at the <strong>Banco de España</strong>.</p>
```

Type over the sentence, leaving the tags at either end alone. `<strong>...</strong>`
makes text bold. To add another paragraph, copy a whole line and edit it.

### 4.6 Change the email address

It appears in **two** places, and both must change:

- `index.html`, in the last bio paragraph — twice on that line, once in
  `href="mailto:..."` and once as the visible text.
- `contact.html`, in the same two forms.

### 4.7 Replace the CV

Replace `assets/cv.pdf`, keeping the filename. No HTML change. Publish.

### 4.8 Replace the photo

The photo must be **web-sized before it goes in** — a camera original of
several megabytes will make the page slow. Target roughly 800×600 and under
200 KB, then save it as `assets/photo.jpg`, keeping the filename.

To resize on Windows without extra software, run this in PowerShell, editing
the source path and the crop rectangle (`x, y, width, height` in original-image
pixels):

```powershell
Add-Type -AssemblyName System.Drawing
$src = "C:\path\to\original.jpg"
$dst = "C:\Users\q32333\Dropbox\5_Research\00_PDFs_papers\rubendominguezdiaz.github.io\assets\photo.jpg"
$img = [System.Drawing.Image]::FromFile($src)
$crop = New-Object System.Drawing.Rectangle 850,150,4000,3000
$out  = New-Object System.Drawing.Bitmap 800,600
$g = [System.Drawing.Graphics]::FromImage($out)
$g.InterpolationMode = [System.Drawing.Drawing2D.InterpolationMode]::HighQualityBicubic
$g.DrawImage($img, (New-Object System.Drawing.Rectangle 0,0,800,600), $crop, [System.Drawing.GraphicsUnit]::Pixel)
$g.Dispose()
$codec = [System.Drawing.Imaging.ImageCodecInfo]::GetImageEncoders() | Where-Object { $_.MimeType -eq 'image/jpeg' }
$ep = New-Object System.Drawing.Imaging.EncoderParameters 1
$ep.Param[0] = New-Object System.Drawing.Imaging.EncoderParameter([System.Drawing.Imaging.Encoder]::Quality, 85L)
$out.Save($dst, $codec, $ep)
$out.Dispose(); $img.Dispose()
```

If the new photo has a different shape, update `width` and `height` in the
`<img>` tag in `index.html` to match, so the page does not jump while loading.

### 4.9 Add a button next to CV / Google Scholar / RePEc

The buttons live in `index.html` in the `<div class="hero-links">` block. Add a
line in the same form:

```html
        <a href="https://example.org/profile" target="_blank" rel="noopener">Label</a>
```

### 4.10 Change colours

Every colour is defined once, at the top of `style.css`:

```css
:root {
  --bg:        #fcf5ea;   /* page background, warm cream */
  --surface:   #f5eee1;   /* header and footer bands */
  --primary:   #0e2841;   /* headings, links, R&R lines: navy */
  --content:   #33302e;   /* body text */
  --secondary: #6b625a;   /* coauthor lines, footer text */
  --border:    #ded5c5;   /* rules and hairlines */
  --tint:      #ece4d5;   /* button fill */
  --band-border: #d8cdba; /* edge of the header and footer bands */
}
```

Change a value there and it applies everywhere it is used.

**Check contrast after changing text or background colours.** Body text needs
at least 4.5:1 against its background to meet WCAG AA. Paste both colours into
<https://webaim.org/resources/contrastchecker/> to check. The current palette
is far above the minimum — body text is 12:1.

### 4.11 Change font sizes

In `style.css`: body text is `--textsize` in `:root`; the name is
`.hero-bio h1`; section headings are `.research h2`; paper titles are
`.item h3`; coauthor and status lines are `.authors, .status`. A second set of
smaller values for phones sits in the `@media (max-width: 700px)` block at the
bottom — change both.

---

## 5. Rules that prevent breakage

1. **Write `&` as `&amp;`** in visible text. `R&amp;R`, not `R&R`. A bare `&`
   can silently break the text after it.
2. **Keep paper links relative.** `href="papers/..."`, never
   `href="https://rubendominguezdiaz.github.io/papers/..."`. Relative links
   keep working when the site moves to its own domain; absolute ones would all
   need rewriting.
3. **Every `<div>` needs its `</div>`.** Deleting one closing tag breaks the
   layout of everything below it. When removing a paper, delete the whole
   block including the final `</div>`.
4. **Do not delete `.nojekyll`.** Without it GitHub tries to process the site
   through Jekyll and files can disappear.
5. **Do not add JavaScript.** The site deliberately has none. The expanding
   abstracts use `<details>`, which is plain HTML.
6. **Do not rename a PDF casually.** The filename is the public URL. Renaming
   breaks every link already shared.
7. **Keep `assets/fonts/README.txt`.** The font is used under a licence that
   requires the attribution to travel with it.
8. **Never commit a paper that must not be public.** This repository is public
   and git keeps deleted files in its history.

---

## 6. Troubleshooting

**The change is not showing.** Wait a minute and press Ctrl+F5. Then check the
commit actually appears at
<https://github.com/rubendominguezdiaz/rubendominguezdiaz.github.io/commits/main>.

**The page layout is broken below a certain point.** A tag was not closed —
almost always a missing `</div>`. Compare the block you edited with a
neighbouring one.

**A paper link gives 404.** The path in `index.html` does not match the actual
file. Paths are case-sensitive: `papers/3_UIG/...` is not `papers/3_uig/...`.

**A build failed.** GitHub emails on a failed build. The status is at
Settings → Pages in the repository.

**Undoing a mistake.** Every version is kept. On github.com, open the file,
click **History**, open the previous version, and copy its contents back. Or
locally, `git revert <commit>`.

---

## 7. For AI assistants

You are working on a static site published by GitHub Pages from the root of
this repository. **The owner does not write HTML — do the edit rather than
explaining how.**

**Context**

- Stack: hand-written HTML + CSS. No JS, no framework, no build step, no
  package manager. Do not introduce any.
- Deployment: push to `main`; GitHub Pages serves the root. `.nojekyll` is
  present and must stay.
- Local path:
  `C:\Users\q32333\Dropbox\5_Research\00_PDFs_papers\rubendominguezdiaz.github.io`
- Live URL: `https://rubendominguezdiaz.github.io/` (a custom domain,
  `rubendominguezdiaz.com`, may be in front of it).

**Page structure of `index.html`**

```
nav.nav > .nav-inner > a.brand + .menu
main
├── section.hero
│   ├── .hero-bio > h1 + p.hero-subtitle x4 + .hero-links > a x3
│   └── .hero-photo > img
└── section.research
    ├── h2 "Working Papers"   + div.item x7
    ├── h2 "Publications"     + div.item x2
    └── h2 "Work in Progress" + div.item x2
footer > div
```

A `div.item` contains, in order: `h3 > a` (title, links to the PDF or DOI),
optional `p.authors`, optional `p.status`, optional
`details > summary + p.abstract`.

**Invariants — do not violate these**

- Paper links are relative (`papers/...`). Never absolute.
- Every external link carries `target="_blank" rel="noopener"`. Internal
  navigation (`index.html`, `contact.html`) and `mailto:` links do not.
- Escape `&` as `&amp;` in text content.
- Colours are CSS variables in `:root` in `style.css`. Do not hard-code a
  colour anywhere else.
- Any new text or background colour pairing must clear WCAG AA (4.5:1).
  Compute it; do not estimate.
- The repository is public. Never commit a file the owner has not agreed to
  publish.

**Verifying a change actually went live** — do this, do not assume:

```bash
# wait for the Pages build
gh api repos/rubendominguezdiaz/rubendominguezdiaz.github.io/pages/builds/latest --jq '.status'

# then confirm the deployed file really contains the change
curl -s -H 'Cache-Control: no-cache' https://rubendominguezdiaz.github.io/ | grep 'the new text'

# check every paper URL resolves
for f in $(git ls-files 'papers/*.pdf'); do
  echo "$(curl -s -o /dev/null -w '%{http_code}' -I "https://rubendominguezdiaz.github.io/$f")  $f"
done
```

GitHub's CDN caches for ten minutes; a stale response right after a push is
normal. Poll rather than concluding the change failed.

**Extracting an abstract from a PDF** (`pdftotext` is available in Git Bash):

```bash
pdftotext -f 1 -l 2 -layout papers/FOLDER/FILE.pdf - | sed -n '/Abstract/,/JEL\|Keywords/p'
```

Fix what extraction mangles: hyphens broken across lines, `-` where an en dash
belongs in ranges and compounds such as `US–China` and `input–output`, and
missing accents.

**Commit messages**: imperative mood, describing the effect rather than the
mechanics. One logical change per commit.
