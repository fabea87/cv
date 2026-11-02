# Curriculum Vitae

[![Build LaTeX CV](https://github.com/fabea87/cv/actions/workflows/build.yml/badge.svg)](https://github.com/fabea87/cv/actions/workflows/build.yml)

Source code and automated build workflow for my academic Curriculum Vitae.

- **English CV**: [`CV.tex`](CV.tex) → [`CV.pdf`](CV.pdf)
- **Chinese CV**: [`CV-cn.tex`](CV-cn.tex) → [`CV-cn.pdf`](CV-cn.pdf)

## Fonts

- **Local fonts** (in `fonts/`):
  - Alegreya Sans SC
  - Bona Nova SC
- **External / System fonts**:
  - PT Sans (Main typeface for English CV)
  - Noto Serif SC (Main CJK typeface for Chinese CV)

## Local Compilation

Compile with XeLaTeX:

```bash
latexmk -xelatex CV.tex
latexmk -xelatex CV-cn.tex
```

## Continuous Integration

A GitHub Actions workflow (`.github/workflows/build.yml`) automatically downloads external fonts, compiles both `.tex` files with XeLaTeX via `latexmk`, and uploads the generated PDF artifacts on every push, pull request, and manual trigger (`workflow_dispatch`).
