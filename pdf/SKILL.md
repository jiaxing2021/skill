---
name: pdf
description: Read and understand PDF file contents by converting to images and viewing them. Use when the user mentions PDF, reads a PDF, parses a PDF, views a PDF, or provides a .pdf file path. Handles multi-page PDFs by rendering each page as a separate image.
---

# PDF Reader

## How It Works

PDFs cannot be read directly as text (layout-based content gets garbled). This skill converts PDF pages to high-resolution PNG images, then reads them visually.

Pipeline: `pdftoppm` → PNG images → Read tool → understand content

## Usage

When a user provides a PDF path or mentions reading a PDF:

### Step 1: Convert PDF to Images

Use `pdftoppm` to render each page as a PNG image. Save to a temp directory alongside the PDF:

```bash
# Create temp directory next to the PDF
PDF_PATH="/path/to/document.pdf"
TMP_DIR="$(dirname "$PDF_PATH")/tmp_pdf_images"
mkdir -p "$TMP_DIR"

# Convert all pages to PNG (300 DPI for clarity)
pdftoppm -png -r 300 "$PDF_PATH" "$TMP_DIR/page"
```

Output files: `page-01.png`, `page-02.png`, etc.

If `pdftoppm` is not available, try:

```bash
# Fallback: use ghostscript
gs -dNOPAUSE -dBATCH -sDEVICE=png16m -r300 -sOutputFile="$TMP_DIR/page-%02d.png" "$PDF_PATH"
```

### Step 2: Read Each Page Image

Use the Read tool on each generated PNG file:

```
Read: /path/to/tmp_pdf_images/page-01.png
Read: /path/to/tmp_pdf_images/page-02.png
...
```

Read pages sequentially. After reading each page, note the key content before moving to the next.

### Step 3: Summarize Content

After reading all pages, provide a structured summary to the user:

- Document title/type (architecture diagram, text document, form, etc.)
- Key content per page
- Overall structure and relationships

### Step 4: Clean Up

Delete the temp directory and all generated images:

```bash
rm -rf "$TMP_DIR"
```

## Important Notes

- Always use `-r 300` (300 DPI) for readable output. Use `-r 150` only if disk space is constrained.
- For very large PDFs (50+ pages), ask the user which page range to read:

  ```bash
  pdftoppm -png -r 300 -f 1 -l 5 "$PDF_PATH" "$TMP_DIR/page"  # pages 1-5 only
  ```

- Architecture diagrams and visual content render well at 300 DPI.
- Text-heavy PDFs: also try `pdftotext -layout` first as a faster alternative. Only fall back to image rendering if text extraction is garbled.

## Decision Flowchart

```
User provides PDF path
  │
  ├─ Text-heavy PDF (reports, articles)?
  │     → Try pdftotext first (faster, smaller)
  │     → If output is garbled → fall back to image pipeline
  │
  └─ Visual PDF (diagrams, charts, forms)?
        → Go directly to image pipeline (pdftoppm)
```

## Example

User: "Read /robot_agent/Robot_Agent_Architecture.pdf"

```bash
# 1. Convert
mkdir -p /robot_agent/tmp_pdf_images
pdftoppm -png -r 300 /robot_agent/Robot_Agent_Architecture.pdf /robot_agent/tmp_pdf_images/page

# 2. Read images (use Read tool on each page-01.png, page-02.png, etc.)

# 3. Summarize content to user

# 4. Clean up
rm -rf /robot_agent/tmp_pdf_images
```
