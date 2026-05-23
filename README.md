# ManuscriptMeter 📄

**A free, privacy-first tool for computing journal submission statistics from Word manuscripts.**

---

## 🚀 Live Demo

> **Anyone can click the link below and use the tool immediately — no download, no install, no account.**
> The tool runs entirely inside the browser; nothing is sent to any server.

→ **[Open ManuscriptMeter](https://YOUR-USERNAME.github.io/manuscript-meter/manuscript-stats.html)**

*(Replace `YOUR-USERNAME` with your GitHub username — see [Hosting](#hosting) below to make this link work in two minutes.)*

---

## How it works for end users

1. Click the Live Demo link above
2. Drop or browse your `.docx` manuscript
3. Tick which sections to exclude (title, abstract, references, etc.)
4. Click **Analyse Manuscript**
5. Copy the word count, table count, and figure count into your journal submission form

That is all. The file never leaves the browser — there is no server, no upload, and no account.

---

## What it detects

ManuscriptMeter automatically finds and separately counts every standard section of a scientific manuscript:

| Section | How detected |
|---|---|
| **Title** | First `Heading 1` / `Title` styled paragraph, or first short heading at the top |
| **Abstract** | Heading matching "Abstract" or "Graphical Abstract"; or an `Abstract` paragraph style |
| **Keywords** | Lines starting with "Keywords:", "Key words:", "Index terms:", or a standalone Keywords heading |
| **Plain-language summary / Key Points** | Heading matching "Plain Language Summary", "Lay Summary", "Key Points", "Highlights", "Significance Statement", etc. |
| **Author list & affiliations** | Short paragraphs between the title and body — detects names, affiliations, emails, ORCIDs |
| **Tables** | All `<w:tbl>` elements; nested and single-cell layout tables are excluded |
| **References** | Heading matching "References", "Bibliography", "Works Cited", etc. |
| **Figure & table captions** | Captions inside figure text boxes; standalone lines beginning with "Figure N" / "Fig. N" / "Table N" |
| **Acknowledgements** | Heading matching any spelling of "Acknowledgement/s" or "Acknowledgment/s" |
| **Data & Code Availability** | Heading matching "Data availability statement", "Data and source code availability statement", "Software availability", "Open research", and many other phrasings |
| **Author Contributions** | Heading matching "Author contributions", "Authors' contributions", "CRediT author statement", etc. |
| **Declarations** | Heading matching "Declarations", "Competing interests", "Conflict of interest", "Ethics statement", misspellings tolerated |
| **Funding** | Heading matching "Funding", "Financial support", "Grant support", "Funding:" (inline bold style), etc. |
| **Figures** | Unique images deduplicated by file size (handles double-column layouts that embed each figure twice); figure numbers from captions used as ground truth |

All end-matter sections (Acknowledgements, Data & Code Availability, etc.) only appear in the breakdown when actually present in the document — absent sections are hidden rather than shown as zero.

### Built to handle real-world manuscripts

- **Journal-specific heading styles** — e.g. IOP Publishing's `IOPH1` style (which does not inherit from standard Heading 1) is detected via same-style recurrence and keyword matching
- **Poorly formatted / informal headings** — inline bold text like `**Funding:**` or `**Decalarations:**` is detected even without a paragraph heading style; trailing colons are stripped; misspellings are handled with fuzzy matching
- **Space-fragmented headings** — `A BSTRACT`, `I ntroduction` etc. are matched after whitespace normalisation
- **Multi-column figures** — each figure in a two-column layout is embedded twice; deduplicated by image file size so figures are counted once
- **Anchored text boxes** — figure captions inside `<w:txbxContent>` are counted separately and never mixed into body-paragraph word totals
- **Tracked changes** — inserted text (`<w:ins>`) included; deleted text (`<w:del>`) excluded

---

## Exclusion checkboxes

Every section has its own checkbox. Defaults match the most common journal requirements:

| Section | Default |
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

---

## Hosting

You only need to do this **once**. After that, the link works for everyone forever.

### Option A — Netlify Drop (fastest, ~30 seconds, no account needed)

1. Go to **[netlify.com/drop](https://app.netlify.com/drop)**
2. Drag `manuscript-stats.html` onto the page
3. Netlify gives you a public URL immediately — share it

### Option B — GitHub Pages (recommended for a permanent link)

```bash
# 1. Create a GitHub repository called "manuscript-meter"

# 2. Clone it and add the file
git clone https://github.com/YOUR-USERNAME/manuscript-meter.git
cd manuscript-meter
cp /path/to/manuscript-stats.html manuscript-stats.html
git add manuscript-stats.html
git commit -m "Add ManuscriptMeter"
git push

# 3. Enable GitHub Pages
#    Repository → Settings → Pages → Source: Deploy from branch → main → / (root) → Save
```

Your tool is then live at:
```
https://YOUR-USERNAME.github.io/manuscript-meter/manuscript-stats.html
```

Update the Live Demo link at the top of this README with that URL, and anyone who clicks it will open the tool instantly in their browser.

### Option C — Download and open locally (no hosting at all)

Users who prefer not to use the hosted version can:
1. Download `manuscript-stats.html` from this repository
2. Double-click the file — it opens in any modern browser
3. Works fully offline once the page has loaded once (JSZip loads from a CDN on first visit only)

---

## Limitations

- Only `.docx` files are supported (see [Roadmap](#roadmap) for planned formats)
- Author block detection uses heuristics and may misclassify unusual title-page layouts
- Figures embedded as linked (not embedded) OLE objects may not be counted
- Word count may differ slightly from Microsoft Word's built-in counter

---

## Roadmap

- **PDF support** — extract statistics from text-layer PDFs
- **LaTeX / `.tex` support** — parse TeX source files
- **ODT / `.odt` support** — OpenDocument Text (LibreOffice)
- **`.doc` support** — legacy Word binary format
- **Batch processing** — analyse multiple files at once
- **Journal-specific presets** — one-click exclusion profiles for Nature, AGU, ERL, and other common journals

---

## Bug reports & feature requests

### Bug report

```
**Bug description**
[What went wrong]

**Expected result**
[What count you expected]

**Actual result**
[What ManuscriptMeter reported]

**Document details** (no need to attach the file)
- Layout: single column / double column / mixed
- Heading style: formal (Heading 1/2/3) / informal / custom journal template
- Abstract: yes / no / separate section
- End-matter sections present: Acknowledgements / Data Availability / Declarations / Funding
- Figures: inline / anchored / inside tables / in text boxes
- Created with: Microsoft Word / Google Docs export / LibreOffice / other

**Browser & OS**
[e.g. Chrome 124 on macOS 14]
```

### Feature request

```
**Feature description**
[What you would like ManuscriptMeter to do]

**Use case**
[Which journal, workflow, or document type this helps with]

**Alternatives considered**
[Any workarounds you currently use]
```

> 💡 You never need to attach your manuscript to a bug report. A structural description is enough to reproduce most issues.

---

## Tech stack

- Pure HTML + JavaScript — one self-contained file, no build step, no framework, no backend
- [JSZip](https://stuk.github.io/jszip/) — reads the `.docx` ZIP archive in the browser
- All XML parsing uses native browser DOM/XML APIs

---

## License

MIT — free to use, share, and modify.
