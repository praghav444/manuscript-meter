# ManuscriptMeter 📄

**A free, privacy-first tool for computing journal submission statistics from Word manuscripts.**

---

## Live Demo

> **Anyone can click the link below and use the tool immediately — no download, no install, no account.**
> The tool runs entirely inside the browser; nothing is sent to any server.

→ **[Open ManuscriptMeter](https://praghav444.github.io/manuscript-meter/manuscript-stats.html)**
*(Right-click → "Open in new tab" to keep this page open)*

---

## How it works for end users

1. Click the Live Demo link above
2. Drop or browse your `.docx` manuscript
3. Tick which sections to exclude (title, abstract, references, etc.)
4. Click **Analyse Manuscript**
5. And this will give you detailed information on word counts across the document.

That is all. The file never leaves the browser — there is no server, no upload, and no account.

---
### Built to handle real-world manuscripts

- **Journal-specific heading styles** — e.g. IOP Publishing's `IOPH1` style is detected via same-style recurrence and keyword matching
- **Poorly formatted / informal headings** — inline bold text like `**Funding:**` or `**Decalarations:**` is detected even without a paragraph heading style; trailing colons are stripped; misspellings are handled with fuzzy matching
- **Space-fragmented headings** — `A BSTRACT`, `I ntroduction` etc. are matched after whitespace normalisation
- **Anchored text boxes** — figure captions inside `<w:txbxContent>` are counted separately and never mixed into body-paragraph word totals
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

### GitHub Pages (recommended)

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

Your tool will then be live at:
```
https://YOUR-USERNAME.github.io/manuscript-meter/manuscript-stats.html
```

Update the Live Demo link at the top of this README with that URL.
Anyone who clicks it will open the tool instantly in their browser — no download or setup required on their end.

### Download and open locally (no hosting needed)

Users who prefer not to use the hosted version can:

1. Download `manuscript-stats.html` from this repository (click the file → **Download raw file**)
2. Double-click the downloaded file — it opens in any modern browser (Chrome, Firefox, Safari, Edge)
3. Works fully offline after the first open (JSZip loads from a CDN on the very first visit only)

---

## Limitations

- Only `.docx` files are supported for now (will work to generalize it across other formats like .pdf, LaTex, ODT. etc.)
- Author block detection uses heuristics and may misclassify unusual title-page layouts
- Figures embedded as linked (not embedded) OLE objects may not be counted
- Word count may differ slightly from Microsoft Word's built-in counter

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
