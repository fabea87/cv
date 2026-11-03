# Curriculum Vitae

[![Build LaTeX CV](https://github.com/fabea87/cv/actions/workflows/build.yml/badge.svg)](https://github.com/fabea87/cv/actions/workflows/build.yml)
[![English CV PDF](https://img.shields.io/badge/PDF-English_CV-0066CC?style=flat-square&logo=adobeacrobatreader&logoColor=white)](https://fabea87.github.io/cv/CV.pdf)
[![Chinese CV PDF](https://img.shields.io/badge/PDF-中文简历-2ea44f?style=flat-square&logo=adobeacrobatreader&logoColor=white)](https://fabea87.github.io/cv/CV-cn.pdf)

LaTeX source files and automated continuous delivery workflow for my academic Curriculum Vitae.

PDF outputs are automatically compiled via GitHub Actions with XeLaTeX, deployed to [GitHub Pages](https://fabea87.github.io/cv/) for direct browser access, and published to [GitHub Releases](https://github.com/fabea87/cv/releases/latest).

## Curriculum Vitae Documents

| Document | Source File | Hosted PDF (Direct View) | Direct Download |
| :--- | :--- | :--- | :--- |
| **English CV** | [`CV.tex`](CV.tex) | [📄 `CV.pdf`](https://fabea87.github.io/cv/CV.pdf) | [📥 Download](https://github.com/fabea87/cv/releases/latest/download/CV.pdf) |
| **Chinese CV** | [`CV-cn.tex`](CV-cn.tex) | [📄 `CV-cn.pdf`](https://fabea87.github.io/cv/CV-cn.pdf) | [📥 Download](https://github.com/fabea87/cv/releases/latest/download/CV-cn.pdf) |

> Build artifacts can also be downloaded directly per commit from [GitHub Actions Runs](https://github.com/fabea87/cv/actions).

---

## Typography & Fonts

- **Bundled Fonts** (located in `fonts/`):
  - **Roboto Condensed**: Document typeface used in `CV.tex` (Regular, Medium, SemiBold, Bold)
  - **Oswald**: Heading and document title typeface used in `CV.tex`
- **External / System Fonts** (automatically fetched & cached by CI):
  - **Noto Serif SC**: Simplified Chinese serif typeface used in `CV-cn.tex`

## Local Compilation

If compiling locally with XeLaTeX:

```bash
latexmk -xelatex CV.tex
latexmk -xelatex CV-cn.tex
```

Compiled PDF files (`*.pdf`) and LaTeX auxiliary build files (`.aux`, `.log`, `.out`, etc.) are ignored by git to keep the repository clean and source-only.
