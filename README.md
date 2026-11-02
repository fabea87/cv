# Curriculum Vitae

[![Build LaTeX CV](https://github.com/fabea87/cv/actions/workflows/build.yml/badge.svg)](https://github.com/fabea87/cv/actions/workflows/build.yml)
[![English CV PDF](https://img.shields.io/badge/PDF-English_CV-0066CC?style=flat-square&logo=adobeacrobatreader&logoColor=white)](https://github.com/fabea87/cv/releases/latest/download/CV.pdf)
[![Chinese CV PDF](https://img.shields.io/badge/PDF-中文简历-2ea44f?style=flat-square&logo=adobeacrobatreader&logoColor=white)](https://github.com/fabea87/cv/releases/latest/download/CV-cn.pdf)

LaTeX source files and automated continuous delivery workflow for my academic Curriculum Vitae.

PDF outputs are automatically compiled via GitHub Actions with XeLaTeX and published to [GitHub Releases](https://github.com/fabea87/cv/releases/latest) upon every update.

## Download Latest PDFs

| Document | Source File | Compiled PDF (CI Output) |
| :--- | :--- | :--- |
| **English CV** | [`CV.tex`](CV.tex) | [📥 Download `CV.pdf`](https://github.com/fabea87/cv/releases/latest/download/CV.pdf) |
| **Chinese CV** | [`CV-cn.tex`](CV-cn.tex) | [📥 Download `CV-cn.pdf`](https://github.com/fabea87/cv/releases/latest/download/CV-cn.pdf) |

> Build artifacts can also be downloaded directly per commit from [GitHub Actions Runs](https://github.com/fabea87/cv/actions).

---

## Typography & Fonts

- **Bundled Fonts** (located in `fonts/`):
  - Alegreya Sans SC
  - Bona Nova SC
- **External / System Fonts** (automatically fetched & cached by CI):
  - **PT Sans**: Document sans-serif typeface used in `CV.tex`
  - **Noto Serif SC**: Simplified Chinese serif typeface used in `CV-cn.tex`

## Local Compilation

If compiling locally with XeLaTeX:

```bash
latexmk -xelatex CV.tex
latexmk -xelatex CV-cn.tex
```

Auxiliary build files and compiled `.pdf` files are ignored by git to keep the repository strictly focused on source code and assets.
