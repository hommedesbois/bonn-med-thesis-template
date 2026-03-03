# Dissertation Template — Medizinische Fakultät, Universität Bonn

A ready-to-use LaTeX template for doctoral dissertations (Dr. med.) at the Medical Faculty of the Rheinische Friedrich-Wilhelms-Universität Bonn. All formatting requirements are pre-configured in `mystyle.sty` — no manual style adjustments needed.

---

## Quick Start

1. Clone or download this repository
2. Replace every `[placeholder]` in the `.tex` files with your own content
3. Add your bibliography entries to `Bibliographie/references.bib`
4. Place your figures in `Abbildungen/`
5. Compile with **XeLaTeX + Biber** (see [Compilation](#compilation))

---

## File Structure

```
dissertation_template_uni_bonn/
├── main.tex                    # Root document — compile this file
├── titlepage.tex               # Title page
├── mystyle.sty                 # All formatting — do not modify
├── CV_Mustermann.pdf           # Placeholder CV — replace with your own (see below)
├── Kapitel/
│   ├── Einleitung.tex          # Chapter 1: Introduction
│   ├── Hauptteil.tex           # Chapter 2: Main body
│   ├── Diskussion.tex          # Chapter 3: Discussion
│   ├── Kurzzusammenfassung.tex # Chapter 4: Summary
│   ├── Eigenanteil.tex         # Declaration of own contribution
│   └── Danksagung.tex          # Acknowledgements (optional)
├── Abbildungen/                # Place your figures here
└── Bibliographie/
    └── references.bib          # All bibliography entries
```

---

## Compilation

The document requires **XeLaTeX** (for the Arial font) and **Biber** (for the bibliography). Run the full sequence:

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

In **VS Code / Cursor** with the LaTeX Workshop extension the recipe `xelatex → biber → xelatex × 2` is pre-configured in `.vscode/settings.json` and will run automatically on save.

In **Overleaf**, set the compiler to *XeLaTeX* under *Menu → Compiler*.

---

## Formatting Specification (`mystyle.sty`)

All formatting is implemented exactly as required by the Medical Faculty. The table below documents every relevant setting.

| Property | Value | Notes |
|---|---|---|
| **Font** | Arial | Loaded via `fontspec` — requires XeLaTeX |
| **Body font size** | 12 pt | Set via document class option |
| **Line spacing** | 1.5× | `\setstretch{1.5}`, equivalent to Word 1.5 line spacing |
| **Paragraph spacing** | 12 pt | No first-line indent |
| **Left margin** | 2.2 cm | |
| **Right margin** | 2.2 cm | |
| **Top margin** | 3.2 cm | Includes header (15 pt) + headsep (1.1 cm) |
| **Bottom margin** | 3.0 cm | |
| **Page numbers** | Centred in header | No header rule; applies to all pages |
| **Chapter headings** | 14 pt, bold | Format: `1.  Title` (number + period) |
| **Section headings** | 12 pt, regular | Format: `1.1.  Title` |
| **Subsection headings** | 12 pt, regular | Format: `1.1.1.  Title` |
| **Heading depth** | 3 levels in template | Chapter → Section → Subsection (1. / 1.1 / 1.1.1); increase `secnumdepth` in `mystyle.sty` for deeper nesting |
| **TOC depth** | 3 levels in template | Increase `tocdepth` in `mystyle.sty` if needed |
| **Figure label** | `Abb.` | German caption prefix |
| **Table label** | `Tab.` | German caption prefix |
| **Caption style** | Single-spaced, bold label, left-aligned | |
| **Figure/table numbering** | Continuous | Not reset per chapter |
| **Figure list entry format** | `Abbildung 1: Title` | |
| **Table list entry format** | `Tabelle 1: Title` | |
| **Bibliography style** | Author–year (`authoryear`) | Backend: Biber |
| **Citation format** | `(Lastname, Year)` | `\cite{}` is remapped to `\parencite{}` |
| **Author name format** | `Lastname Initials` | e.g. `Mustermann M.` |
| **Reference list spacing** | 12 pt between entries | Left-aligned, no indent |
| **All hyperlinks** | Black | Internal links, citations, URLs |
| **Tables** | Single-spaced | `booktabs` style (`\toprule`, `\midrule`, `\bottomrule`) |
| **Language** | German (`ngerman`) | Correct hyphenation and `\enquote{}` quotation marks |

---

## How to Adapt the Template

### Title page (`titlepage.tex`)

Replace all `[placeholder]` entries:

| Placeholder | Replace with |
|---|---|
| `[Titel der Dissertation]` | Full title of your dissertation |
| `Max Mustermann` | Your full name |
| `Musterstadt` | Your city of birth |
| `[Jahr]` | Year of submission |
| `[Name 1. Gutachter]` | First examiner (name + title) |
| `[Name 2. Gutachter:in]` | Second examiner (name + title) |
| `[Institut]` | Full name of your institute |


### Chapters

Each chapter file contains lorem ipsum placeholder text. Replace it section by section with your own content. The heading hierarchy is:

```latex
\chapter{Titel}       % 1.
  \section{Titel}     % 1.1
    \subsection{Titel} % 1.1.1
```

### Figures

Place image files in `Abbildungen/` and include them with:

```latex
% Standard centred figure
\begin{figure}[H]
    \centering
    \includegraphics[width=0.8\textwidth]{Abbildungen/dateiname}
    \caption{Beschriftung der Abbildung. Quelle: Autor Jahr.}
    \label{fig:meinlabel}
\end{figure}

% Inline portrait figure (text wraps around)
\begin{wrapfigure}{l}{\wrapfigwidth}
    \includegraphics[width=0.28\textwidth]{Abbildungen/dateiname}
    \caption*{Unterschrift ohne Nummer}
\end{wrapfigure}
```

### Bibliography (`Bibliographie/references.bib`)

Add entries in standard BibTeX format. The following types are supported with custom formatting:

| Type | Format |
|---|---|
| `@article` | Lastname Initials. Title. Journal Year; Volume: Pages |
| `@book` | Lastname Initials. Title. City: Publisher, Year |
| `@incollection` | Lastname Initials. Title. in: Editor Hrsg. Booktitle. City: Publisher, Year: Pages |
| `@misc` | Lastname Initials. Title. URL, accessed Month Year |
| `@phdthesis` | Lastname Initials. Title. School, Year |
| `@techreport` / `@report` | Lastname Initials. Title. Institution, Year |

Use `\cite{key}` in the text (automatically rendered as a parenthetical author–year citation).

### CV

Add your CV as a single-page PDF to the root of the repository, then update the filename in `main.tex`:

```latex
\includepdf[pages=1]{YourCV.pdf}
```

Replace `YourCV.pdf` with the actual name of your file. The PDF is included as the last numbered chapter of the dissertation.

### Acknowledgements (`Kapitel/Danksagung.tex`)

Uncomment the following line in `main.tex` to include acknowledgements before the list of figures:

```latex
\input{Kapitel/Danksagung}
```

---

---

# Dissertationsvorlage — Medizinische Fakultät, Universität Bonn

Eine fertige LaTeX-Vorlage für Dissertationen (Dr. med.) an der Medizinischen Fakultät der Rheinischen Friedrich-Wilhelms-Universität Bonn. Alle Formatierungsvorgaben sind in `mystyle.sty` umgesetzt — keine manuellen Stilanpassungen erforderlich.

---

## Schnellstart

1. Repository klonen oder herunterladen
2. Alle `[Platzhalter]` in den `.tex`-Dateien durch eigene Inhalte ersetzen
3. Literaturangaben in `Bibliographie/references.bib` eintragen
4. Abbildungen im Ordner `Abbildungen/` ablegen
5. Mit **XeLaTeX + Biber** kompilieren (siehe [Kompilierung](#kompilierung))

---

## Dateistruktur

```
dissertation_template_uni_bonn/
├── main.tex                    # Hauptdokument — diese Datei kompilieren
├── titlepage.tex               # Titelseite
├── mystyle.sty                 # Gesamte Formatierung — nicht verändern
├── CV_Mustermann.pdf           # Platzhalter-Lebenslauf — durch eigene PDF ersetzen (s. u.)
├── Kapitel/
│   ├── Einleitung.tex          # Kapitel 1: Einleitung
│   ├── Hauptteil.tex           # Kapitel 2: Hauptteil
│   ├── Diskussion.tex          # Kapitel 3: Diskussion
│   ├── Kurzzusammenfassung.tex # Kapitel 4: Zusammenfassung
│   ├── Eigenanteil.tex         # Erklärung zum Eigenanteil
│   └── Danksagung.tex          # Danksagung (optional)
├── Abbildungen/                # Abbildungen hier ablegen
└── Bibliographie/
    └── references.bib          # Alle Literaturangaben
```

---

## Kompilierung

Das Dokument erfordert **XeLaTeX** (für die Schriftart Arial) und **Biber** (für das Literaturverzeichnis). Vollständige Build-Sequenz:

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

In **VS Code / Cursor** mit der LaTeX-Workshop-Erweiterung ist das Rezept `xelatex → biber → xelatex × 2` bereits in `.vscode/settings.json` konfiguriert und wird beim Speichern automatisch ausgeführt.

In **Overleaf**: Compiler unter *Menu → Compiler* auf *XeLaTeX* umstellen.

---

## Formatierungsvorgaben (`mystyle.sty`)

Alle Vorgaben der Medizinischen Fakultät sind vollständig umgesetzt:

| Eigenschaft | Wert | Hinweis |
|---|---|---|
| **Schriftart** | Arial | Über `fontspec` — erfordert XeLaTeX |
| **Schriftgröße** | 12 pt | |
| **Zeilenabstand** | 1,5-zeilig | `\setstretch{1.5}`, entspricht Word-Stil |
| **Absatzabstand** | 12 pt | Kein Erstzeilen-Einzug |
| **Linker Rand** | 2,2 cm | |
| **Rechter Rand** | 2,2 cm | |
| **Oberer Rand** | 3,2 cm | Inkl. Kopfzeile (15 pt) + Abstand (1,1 cm) |
| **Unterer Rand** | 3,0 cm | |
| **Seitenzahlen** | Zentriert in der Kopfzeile | Keine Trennlinie |
| **Kapitelüberschriften** | 14 pt, fett | Format: `1.  Titel` |
| **Abschnittsüberschriften** | 12 pt, nicht fett | Format: `1.1.  Titel` |
| **Unterabschnittsüberschriften** | 12 pt, nicht fett | Format: `1.1.1.  Titel` |
| **Gliederungstiefe** | 3 Ebenen in der Vorlage | Kapitel → Abschnitt → Unterabschnitt (1. / 1.1 / 1.1.1); für tiefere Gliederung `secnumdepth` in `mystyle.sty` erhöhen |
| **Inhaltsverzeichnis** | 3 Ebenen in der Vorlage | Bei Bedarf `tocdepth` in `mystyle.sty` erhöhen |
| **Abbildungsbezeichnung** | `Abb.` | |
| **Tabellenbezeichnung** | `Tab.` | |
| **Legendenstil** | 1-zeilig, Label fett, linksbündig | |
| **Abbildungs-/Tabellennummerierung** | Fortlaufend | Kein Zurücksetzen pro Kapitel |
| **Abbildungsverzeichnis-Format** | `Abbildung 1: Titel` | |
| **Tabellenverzeichnis-Format** | `Tabelle 1: Titel` | |
| **Zitierstil** | Autor–Jahr (`authoryear`) | Backend: Biber |
| **Zitatformat** | `(Nachname, Jahr)` | `\cite{}` → `\parencite{}` |
| **Autorenformat** | `Nachname Initialen` | z. B. `Mustermann M.` |
| **Literaturverzeichnis** | 12 pt Abstand, linksbündig, kein Einzug | |
| **Hyperlinks** | Schwarz | Interne Links, Zitate, URLs |
| **Tabellen** | 1-zeilig | `booktabs`-Stil |
| **Sprache** | Deutsch (`ngerman`) | Silbentrennung und `\enquote{}` |

---

## Vorlage anpassen

### Titelseite (`titlepage.tex`)

Alle `[Platzhalter]` ersetzen:

| Platzhalter | Ersetzen durch |
|---|---|
| `[Titel der Dissertation]` | Vollständiger Titel der Arbeit |
| `Max Mustermann` | Vollständiger Name |
| `Musterstadt` | Geburtsort |
| `[Jahr]` | Einreichungsjahr |
| `[Name 1. Gutachter]` | Name und Titel des 1. Gutachters |
| `[Name 2. Gutachter:in]` | Name und Titel des 2. Gutachters/Gutachterin |
| `[Institut]` | Vollständiger Name des Instituts |


### Kapitel

Lorem-ipsum-Text in den Kapiteldateien wird Abschnitt für Abschnitt durch eigene Inhalte ersetzt. Gliederung:

```latex
\chapter{Titel}        % 1.
  \section{Titel}      % 1.1
    \subsection{Titel} % 1.1.1
```

### Abbildungen

Bilddateien in `Abbildungen/` ablegen und einbinden:

```latex
% Zentrierte Abbildung
\begin{figure}[H]
    \centering
    \includegraphics[width=0.8\textwidth]{Abbildungen/dateiname}
    \caption{Beschriftung. Quelle: Autor Jahr.}
    \label{fig:meinlabel}
\end{figure}

% Abbildung mit Textumfluss (z. B. Porträt)
\begin{wrapfigure}{l}{\wrapfigwidth}
    \includegraphics[width=0.28\textwidth]{Abbildungen/dateiname}
    \caption*{Unterschrift ohne Nummer}
\end{wrapfigure}
```

### Literaturverzeichnis (`Bibliographie/references.bib`)

Einträge im BibTeX-Format ergänzen. Unterstützte Typen mit angepasstem Format:

| Typ | Format |
|---|---|
| `@article` | Nachname Initialen. Titel. Zeitschrift Jahr; Band: Seiten |
| `@book` | Nachname Initialen. Titel. Ort: Verlag, Jahr |
| `@incollection` | Nachname Initialen. Titel. in: Herausgeber Hrsg. Buchtitel. Ort: Verlag, Jahr: Seiten |
| `@misc` | Nachname Initialen. Titel. URL, Zugriff Monat Jahr |
| `@phdthesis` | Nachname Initialen. Titel. Universität, Jahr |
| `@techreport` / `@report` | Nachname Initialen. Titel. Institution, Jahr |

Zitation im Text mit `\cite{schlüssel}` (wird automatisch als Autor–Jahr-Zitat dargestellt).

### Lebenslauf

Eigene Lebenslauf-PDF in das Stammverzeichnis des Projekts legen und den Dateinamen in `main.tex` anpassen:

```latex
\includepdf[pages=1]{EigenerLebenslauf.pdf}
```

`EigenerLebenslauf.pdf` durch den tatsächlichen Dateinamen ersetzen. Die PDF wird als letztes nummeriertes Kapitel eingebunden.

### Danksagung (`Kapitel/Danksagung.tex`)

In `main.tex` die folgende Zeile auskommentieren, um die Danksagung einzubinden:

```latex
\input{Kapitel/Danksagung}
```
