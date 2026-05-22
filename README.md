# ManuscriptMeter 📄

**A free, privacy-first tool for computing journal submission statistics from Word manuscripts.**

→ **[Live Demo via GitHub Pages](https://your-username.github.io/manuscript-meter)**

---

## What it does

When submitting a manuscript to a journal, you're often asked for:

- **Word count** (excluding title, abstract/plain-language summary, author list, tables, references)
- **Number of tables**
- **Number of figures**

ManuscriptMeter extracts all three from your `.docx` file automatically, with fully configurable exclusions.

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

## Usage

1. Open `manuscript-stats.html` in any modern browser (Chrome, Firefox, Safari, Edge)
2. Drop or browse your `.docx` file
3. Select which sections to exclude from the word count
4. Click **Analyse Manuscript**
5. Copy the summary to paste into your journal submission form

---

## Hosting on GitHub Pages (recommended)

```bash
# 1. Fork or clone this repo
git clone https://github.com/your-username/manuscript-meter.git
cd manuscript-meter

# 2. The single file is already ready
# manuscript-stats.html is the entire app

# 3. Enable GitHub Pages in repo Settings → Pages → Deploy from branch (main)
# Your tool will be live at: https://your-username.github.io/manuscript-meter/manuscript-stats.html
```

---

## What gets detected

| Element | Detection method |
|---|---|
| **Title** | First `Heading 1` / `Title` styled paragraph, or first short paragraph at the top |
| **Abstract / Plain-language summary** | Heading matching keywords (Abstract, Summary, Plain-language summary, Lay summary, etc.), or paragraphs with an "Abstract" paragraph style |
| **Author list & affiliations** | Short paragraphs between title and body — detects names, affiliations (university, institute, department…), emails, and ORCIDs |
| **Tables** | Top-level `<w:tbl>` elements in the document body (nested tables inside tables are not double-counted) |
| **Figures** | Unique image relationship IDs referenced in drawing elements (inline + anchored), cross-checked against captioned figure lines |
| **References** | Section heading matching References, Bibliography, Works Cited, etc. |
| **Figure / table captions** | Paragraphs starting with "Figure N", "Fig. N", "Table N", or using the built-in "Caption" paragraph style |
| **Text boxes** | `<w:txbxContent>` elements are included in the word count |

### Robustness across document formats

- **Single-column and multi-column layouts** — both handled equally (word extraction is layout-agnostic)
- **Custom heading styles** — `styles.xml` is parsed to follow `basedOn` chains, so custom styles derived from Heading 1 are correctly identified
- **Figures inside tables or text boxes** — counted via relationship IDs embedded anywhere in the document XML
- **Tracked changes** — inserted text (`<w:ins>`) is included; deleted text (`<w:del>`) is excluded
- **Documents without formal headings** — heuristic fallback uses paragraph length and punctuation patterns

---

## Limitations

- Only `.docx` files are supported (see [Roadmap](#roadmap) for future formats)
- Author block detection uses heuristics and may mis-classify in unusual title-page formats
- Figures embedded as linked (not embedded) OLE objects may not be counted
- Complex multi-section documents with unusual structures may need manual verification
- Word count may differ slightly from Microsoft Word's built-in counter, which uses its own internal tokenisation rules

---

## Roadmap

We are actively working to expand ManuscriptMeter's capabilities. Planned improvements include:

- **PDF support** — extract statistics from `.pdf` manuscripts (text-layer PDFs)
- **LaTeX / `.tex` support** — parse TeX source files for word and float counts
- **ODT / `.odt` support** — OpenDocument Text format used by LibreOffice
- **`.doc` support** — legacy Word binary format
- **Batch processing** — analyse multiple files at once
- **Journal-specific presets** — one-click exclusion profiles for common journals

---

## Feedback & Bug Reports

Your feedback is what makes this tool better. If you spot a counting error, an edge case that breaks the parser, or have a feature request, please open an issue using one of the templates below.

### Bug report template

When filing a bug, please use this format (you can paste it directly into a GitHub Issue):

```
**Bug description**
[Brief description of the problem]

**Expected result**
[What count you expected]

**Actual result**
[What ManuscriptMeter reported]

**Document details** (no need to attach the file — just describe its structure)
- Layout: single column / double column / mixed
- Heading style: formal (Heading 1/2/3) / informal (no headings) / custom styles
- Abstract: yes / no / separate document section
- Figures: inline / anchored / inside tables / in text boxes
- Word processor used to create the file: Microsoft Word / Google Docs exported / LibreOffice / other

**Browser & OS**
[e.g. Chrome 124 on macOS 14]

**Additional context**
[Any other relevant information]
```

### Feature request template

```
**Feature description**
[What you'd like ManuscriptMeter to do]

**Use case**
[Why this would be useful — which journal, workflow, or document type]

**Alternatives considered**
[Any workarounds you currently use]
```

> 💡 **Privacy note:** You never need to attach your manuscript to a bug report. A structural description of the document is enough to reproduce most issues.

---

## Tech stack

- Pure HTML + JavaScript (no build step, no framework, no backend)
- [JSZip](https://stuk.github.io/jszip/) — loads the `.docx` ZIP archive
- All other parsing is native browser DOM/XML APIs

---

## License

MIT — free to use, share, and modify.
