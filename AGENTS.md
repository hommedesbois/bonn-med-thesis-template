# AGENTS.md — AI Agent Instructions

This file provides instructions and context for AI agents (Cursor, Claude, Codex, etc.) working in this repository.

---

## Repository Purpose

This is a **LaTeX dissertation template** for the Medizinische Fakultät of the Rheinische Friedrich-Wilhelms-Universität Bonn. It is intended to be published as a GitHub and/or Overleaf template repository, providing a ready-to-use structure and formatting for doctoral dissertations.

All original content has been replaced with anonymous placeholder material (lorem ipsum text, dummy figures, dummy references). The formatting, chapter structure, and style settings reflect actual submission requirements and must be preserved exactly.

---

## Repository Structure

```
dissertation_template_uni_bonn/
├── main.tex                        # Root document — entry point for compilation
├── titlepage.tex                   # Title page (author, title, institution, examiners)
├── mystyle.sty                     # Custom style package (fonts, margins, bibliography, etc.)
├── Kapitel/                        # Chapter files
│   ├── Einleitung.tex              # Chapter 1: Introduction
│   ├── Hauptteil.tex               # Chapter 2: Hauptteil (main body)
│   ├── Diskussion.tex              # Chapter 3: Discussion
│   ├── Kurzzusammenfassung.tex     # Chapter 4: Summary (German + English)
│   ├── Eigenanteil.tex             # Declaration of own contribution
│   ├── Danksagung.tex             # Acknowledgements (not included in main.tex by default)
│   └── Teil2.tex                   # Optional additional chapter (not included by default)
├── Abbildungen/                    # Figure directory (use placeholder images here)
└── Bibliographie/
    └── references.bib              # All bibliography entries (one dummy per type)
```

### Files NOT included in `main.tex` by default

- `Kapitel/Danksagung.tex` — acknowledgements; uncomment the `\input` in `main.tex` to include
- `Kapitel/Teil2.tex` — optional second main chapter; add `\input{Kapitel/Teil2}` after `\input{Kapitel/Hauptteil}` to include
- `Kapitel/Hauptteil_nur_Kapitel.tex` — scratch/outline file; not part of the compiled document

---

## Compilation

The document uses **XeLaTeX** (required for the Arial font via `fontspec`) and **Biber** (for `biblatex` with `authoryear` style).

Recommended build sequence:

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

Or use `latexmk` with an appropriate `.latexmkrc`.

> **Note:** `main.tex` references `\includepdf[pages=1]{CV_Mustermann.pdf}` for the CV page. You must provide a file with that name, or comment out those lines to compile without it.

---

## Style & Formatting (`mystyle.sty`)

Key formatting decisions encoded in `mystyle.sty` — **do not modify these** unless intentionally changing the template for your faculty's requirements:

- Font: Arial via `fontspec` (requires XeLaTeX)
- Line spacing: 1.5× via `setspace`
- Margins: left/right 2.2 cm, top 3.2 cm, bottom 3.0 cm via `geometry`
- Bibliography: `biblatex` with `authoryear` style, backend `biber`; loaded from the four `.bib` files
- Chapter/section headings: 14 pt bold for chapters, 12 pt for sections — formatted via `titlesec`
- Figures/tables: `float`, `subcaption`, `graphicx`, `wrapfig`
- PDF inclusion: `pdfpages` (used for the CV page at the end)
- Hyperlinks: `hyperref` (all links in black)
- Figure/table numbering: continuous (not reset per chapter)

---

## Template Placeholders

Every element in `[square brackets]` is a placeholder that must be replaced by the actual author.

| Location | Placeholder | Replace with |
|---|---|---|
| `titlepage.tex` | `[Titel der Dissertation]` | Full dissertation title |
| `titlepage.tex` | `Max Mustermann` | Author's full name |
| `titlepage.tex` | `Musterstadt` | Author's city of birth |
| `titlepage.tex` | `[Jahr]` | Year of submission |
| `titlepage.tex` | `[Name 1. Gutachter]` | First examiner's name and title |
| `titlepage.tex` | `[Name 2. Gutachter:in]` | Second examiner's name and title |
| `titlepage.tex` | `[Institut]` | Full name of the institute |
| `titlepage.tex` | `UNI_Bonn_Logo_Standard.pdf` | Uncomment the `\includegraphics` line and provide the logo file |
| `Kapitel/*.tex` | Lorem ipsum body text | Actual dissertation content |
| `Kapitel/Eigenanteil.tex` | `[Titel der Dissertation]`, `[Ort]`, `[Datum]`, `Max Mustermann` | Actual title, city, date, name |
| `Abbildungen/` | Placeholder images (`example-image`) | Actual figures |
| `Bibliographie/references.bib` | Dummy references (one per type) | Actual bibliography entries |
| `main.tex` | `CV_Mustermann.pdf` | Your own CV as a single-page PDF |

---

## Bibliography Reference Types

Each `.bib` file contains exactly one dummy entry demonstrating the required format. The four supported types are:

| Entry type | Example key |
|---|---|
| `@article` | `DummyArticle2024` |
| `@book` | `DummyBook2024` |
| `@incollection` | `DummyIncollection2024` |
| `@misc` | `DummyMisc2024` |

All entries live in `Bibliographie/references.bib`.

Additional entry types with custom bibliography drivers defined in `mystyle.sty`: `@phdthesis`, `@techreport`, `@report`. These can be added to any of the four `.bib` files.

Use `\cite{key}` (remapped to `\parencite`) or `\footcite{key}` for citations.

---

## Agent Task Guide

When an AI agent is asked to help adapt this template for a new dissertation, follow these guidelines:

### Text

- Replace lorem ipsum text section by section with the actual content.
- Preserve all LaTeX commands: `\section`, `\subsection`, `\subsubsection`, `\cite`, `\ref`, `\label`, `\footnote`, `\textit`, `\textbf`, `\enquote`, etc.
- Do not alter heading hierarchy or numbering.
- Replace all `[placeholder]` markers with actual values.

### Figures

- Placeholder figures use `example-image` (built into all LaTeX distributions). Replace with real files in `Abbildungen/`.
- The template shows two figure styles: `wrapfigure` (for inline/portrait figures) and standard `figure` (centered, full-width).
- When adding a figure: keep the `\label` command, update the `\caption`, and replace `example-image` with the actual filename.
- Do not remove `figure` environments or `\caption` commands — replace the image file only.

### Tables

- The template contains one example `table` environment in `Hauptteil.tex`. Copy and adapt it for additional tables.
- Tables use the `booktabs` package (`\toprule`, `\midrule`, `\bottomrule`). Do not use `\hline`.

### Bibliography

- Each `.bib` file contains one dummy entry as a structural placeholder.
- Add real entries in standard BibTeX format. The `authoryear` citation style is active.
- Do not remove the dummy entry until at least one real entry has been added (avoids `biblatex` errors).
- Citation format in text: Author name + year in parentheses, e.g. `(Mustermann, 2024)`.

### Do Not Modify

- `mystyle.sty` — unless intentionally changing layout for your faculty's requirements
- `main.tex` document class options (`report`, `twoside`, `12pt`, `a4paper`)
- The overall chapter order in `main.tex`
- `.gitignore`

---

## Publishing

### GitHub

Push the repository to GitHub and enable *Template repository* under *Settings → General*. Users can then click *Use this template* to create their own copy.

### Overleaf Template Gallery

This template can also be published on the [Overleaf template gallery](https://www.overleaf.com/latex/templates):

1. **Create an Overleaf project** — upload all `.tex`, `.sty`, `.bib` files and any placeholder figures
2. **Publish as template** — go to *Share → Publish as Template*, set a title, description, category (e.g. *Thesis*), and tags
3. **Review** — Overleaf reviews submissions before they appear publicly (typically a few days)

**Before submitting to Overleaf, ensure:**

- The project compiles cleanly (XeLaTeX + Biber — already the required engine for this template)
- Comment out the `\includepdf` lines in `main.tex` (or provide a placeholder PDF) since Overleaf will not have a CV file
- The `UNI_Bonn_Logo_Standard.pdf` line remains commented out in `titlepage.tex` (it already is)
- All figures use `example-image` or other generic placeholders, with no personal or copyrighted content

### GitHub + Overleaf (combined workflow)

Overleaf supports importing directly from a GitHub repository (*New Project → Import from GitHub*). This allows maintaining the source on GitHub while keeping an Overleaf project in sync. Note: this feature requires an Overleaf premium account.
