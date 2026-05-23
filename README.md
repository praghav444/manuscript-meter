# ManuscriptMeter 📄

**A free, privacy-first tool for computing journal submission statistics from Word manuscripts.**

→ **[Live Demo](https://YOUR-USERNAME.github.io/manuscript-meter/manuscript-stats.html)** ← Replace `YOUR-USERNAME` with your GitHub username after setup

---

## Quick start

**Option A — Run directly in your browser (no download needed)**
1. Go to your GitHub Pages URL: `https://YOUR-USERNAME.github.io/manuscript-meter/manuscript-stats.html`
2. Drop your `.docx` file onto the page
3. Done — results appear instantly

**Option B — Download and run locally**
1. Download `manuscript-stats.html` from this repository
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge) — double-click the file
3. Drop your `.docx` file onto the page

> No installation, no server, no internet connection required once the file is open.

---

## What it does

When submitting a manuscript to a journal, you are often asked for:

- **Word count** (main text only, excluding title, abstract, tables, references, etc.)
- **Number of tables**
- **Number of figures**

ManuscriptMeter extracts all three from your `.docx` file automatically.
Every section that contributes to the word count has its own checkbox so you can match exactly what your target journal requires.

---

## Privacy & Security

> **Your file never leaves your device.**

All parsing happens entirely inside your browser using JavaScript. There is:

- No server
- No upload
- No network request with your document
- No analytics on file content

This means your manuscript is end-to-end protected — it cannot be intercepted in transit because it never travels anywhere.

---

## Sections detected and counted

| Section | Detection method |
|---|---|
| **Title** | First `Heading 1` / `Title` styled paragraph, or first short paragraph at the top |
| **Abstract** | Heading matching "Abstract" or "Graphical Abstract"; or paragraphs using an `Abstract` paragraph style |
| **Keywords** | Paragraphs beginning with "Keywords:", "Key words:", "Index terms:", or a standalone "Keywords" heading |
| **Plain-language summary / Key Points** | Heading matching "Plain Language Summary", "Lay Summary", "Key Points", "Highlights", "Significance Statement", etc. |
| **Author list & affiliations** | Short paragraphs between title and body — detects names, affiliations, emails, and ORCIDs |
| **Tables** | All `<w:tbl>` elements; nested tables inside table cells are not double-counted; single-cell layout tables are excluded |
| **References** | Section heading matching "References", "Bibliography", "Works Cited", etc. |
| **Figure & table captions** | Paragraphs in figure text boxes; standalone caption lines beginning with "Figure N" / "Fig. N" / "Table N" |
| **Acknowledgements** | Heading matching "Acknowledgement", "Acknowledgment", "Acknowledgements" (any spelling) |
| **Data & Code Availability** | Heading matching "Data availability statement", "Data and source code availability statement", "Software availability", "Open research", and many other phrasings |
| **Author Contributions** | Heading matching "Author contributions", "Authors' contributions", "CRediT author statement", etc. |
| **Declarations** | Heading matching "Declarations", "Competing interests", "Conflict of interest", "Ethics statement", "Decalarations" (misspelling tolerated), and similar |
| **Funding** | Heading matching "Funding", "Financial support", "Grant support", etc. |
| **Figures** | Unique images deduped by file size (handles double-column layouts that embed each figure twice); figure numbers extracted from captions as ground truth |

### Robustness features

- **Custom journal heading styles** — `styles.xml` is parsed to follow `basedOn` chains; journal-specific styles like `IOPH1` (IOP Publishing) that do not inherit from a standard Heading are detected via same-style recurrence and section-keyword matching
- **Space-stripped matching** — headings like `A BSTRACT` or `I ntroduction` (letters separated by spaces) are normalised before matching
- **Inline bold headings with colons** — informal headings like `**Funding:**` or `**Decalarations:**` are detected even without a paragraph heading style; trailing colons are stripped before keyword matching
- **Misspelling tolerance** — fuzzy regex `\bdec[la]{1,4}ar(?:ation|at)\w*` matches "Declarations", "Decalarations", and similar transpositions
- **Multi-column layouts** — figure text boxes that appear twice (once per column) are deduplicated by image file size so figures are counted once
- **Anchored text boxes** — figure captions embedded inside `<w:txbxContent>` are extracted separately and never mixed into body-paragraph word counts
- **Tracked changes** — inserted text (`<w:ins>`) is included; deleted text (`<w:del>`) is excluded
- **Documents without formal headings** — heuristic fallback uses paragraph length and punctuation patterns

---

## Exclusion options

Every detected section has its own checkbox in the UI.
Sections checked by default (typical journal requirements):

| Checkbox | Default |
|---|---|
| Title | ✅ excluded |
| Abstract | ✅ excluded |
| Keywords | ✅ excluded |
| Plain-language summary / Key Points | ✅ excluded |
| Author list & affiliations | ✅ excluded |
| Tables | ✅ excluded |
| References | ✅ excluded |
| Figure & table captions | ☐ included |
| Acknowledgements | ☐ included |
| Data & Code Availability | ☐ included |
| Author Contributions | ☐ included |
| Declarations | ☐ included |
| Funding | ☐ included |

End-matter rows (Acknowledgements, Data & Code Availability, etc.) only appear in the detailed breakdown when the section is actually present in the document — absent sections are hidden rather than shown as zero.

---

## Hosting on GitHub Pages

```bash
# 1. Create a new repository on GitHub named "manuscript-meter" (or any name you like)

# 2. Clone it locally
git clone https://github.com/YOUR-USERNAME/manuscript-meter.git
cd manuscript-meter

# 3. Copy the tool into the repo root and rename it
cp /path/to/manuscript-stats.html manuscript-stats.html

# 4. Commit and push
git add manuscript-stats.html
git commit -m "Add ManuscriptMeter"
git push

# 5. Enable GitHub Pages
#    Go to: https://github.com/YOUR-USERNAME/manuscript-meter/settings/pages
#    Source: Deploy from branch → main → / (root) → Save

# Your tool will be live at:
# https://YOUR-USERNAME.github.io/manuscript-meter/manuscript-stats.html
```

Once live, anyone can open the URL in their browser and use the tool immediately — no download required.
The tool also works fully offline after the page has loaded once (JSZip is loaded from a CDN on first visit only).

---

## Limitations

- Only `.docx` files are supported (see [Roadmap](#roadmap) for planned formats)
- Author block detection uses heuristics and may misclassify unusual title-page layouts
- Figures embedded as linked (not embedded) OLE objects may not be counted
- Word count may differ slightly from Microsoft Word's built-in counter, which uses its own internal tokenisation rules
- Complex multi-section documents with highly unusual structures may need manual verification

---

## Roadmap

- **PDF support** — extract statistics from `.pdf` manuscripts (text-layer PDFs)
- **LaTeX / `.tex` support** — parse TeX source files for word and float counts
- **ODT / `.odt` support** — OpenDocument Text format used by LibreOffice
- **`.doc` support** — legacy Word binary format
- **Batch processing** — analyse multiple files at once
- **Journal-specific presets** — one-click exclusion profiles for common journals (Nature, AGU, ERL, etc.)

---

## Feedback & Bug Reports

If you spot a counting error, an edge case that breaks the parser, or have a feature request, please open a GitHub Issue using one of the templates below.

### Bug report template

```
**Bug description**
[Brief description of the problem]

**Expected result**
[What count you expected]

**Actual result**
[What ManuscriptMeter reported]

**Document details** (no need to attach the file — just describe its structure)
- Layout: single column / double column / mixed
- Heading style: formal (Heading 1/2/3) / informal (no headings) / custom styles (e.g. journal template)
- Abstract: yes / no / separate section
- End-matter sections present: Acknowledgements / Data Availability / Author Contributions / Declarations / Funding
- Figures: inline / anchored / inside tables / in text boxes
- Word processor used: Microsoft Word / Google Docs export / LibreOffice / other

**Browser & OS**
[e.g. Chrome 124 on macOS 14]

**Additional context**
[Any other relevant information]
```

### Feature request template

```
**Feature description**
[What you would like ManuscriptMeter to do]

**Use case**
[Why this would be useful — which journal, workflow, or document type]

**Alternatives considered**
[Any workarounds you currently use]
```

> 💡 **Privacy note:** You never need to attach your manuscript to a bug report. A structural description of the document is enough to reproduce most issues.

---

## Tech stack

- Pure HTML + JavaScript — single self-contained file, no build step, no framework, no backend
- [JSZip](https://stuk.github.io/jszip/) — loads the `.docx` ZIP archive in the browser
- All XML parsing uses native browser DOM/XML APIs

---

## License

MIT — free to use, share, and modify.
