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
| **Title** | First paragraph / Heading 1 style |
| **Abstract / Plain-language summary** | Heading matching keywords (Abstract, Summary, Plain-language summary, Lay summary, etc.) |
| **Author list & affiliations** | Short paragraphs between title and body (heuristic) |
| **Tables** | `<w:tbl>` elements in the document XML |
| **Figures** | Embedded image relationships + drawing anchors |
| **References** | Section heading matching References, Bibliography, Works Cited, etc. |
| **Figure captions** | Lines starting with "Figure N" or "Fig. N" |

---

## Limitations

- Only `.docx` files are supported (not `.doc`, `.odt`, `.pdf`)
- Author block detection uses a heuristic and may mis-classify in unusual formats
- Figures embedded as text boxes or shapes may not be counted
- Complex multi-section documents may need manual verification

---

## Tech stack

- Pure HTML + JavaScript (no build step, no framework, no backend)
- [JSZip](https://stuk.github.io/jszip/) — loads the `.docx` ZIP archive
- All other parsing is native browser DOM/XML APIs

---

## License

MIT — free to use, share, and modify.
