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
  - **Roboto Condensed**: Document typeface used in both `CV.tex` and `CV-cn.tex`
    (Regular, Medium, Italic, MediumItalic; plus SemiBold/Bold for the Chinese CV headings)
  - **Oswald**: Heading and document title typeface used in `CV.tex` (Regular, Medium, SemiBold)
- **External / System Fonts**:
  - **Noto Serif CJK SC**: Simplified Chinese body serif in `CV-cn.tex`. Install with
    `brew install font-noto-serif-cjk-sc`; CI fetches the static Regular + Bold OTFs.
  - **汇文正楷 (Huiwen ZhengKai)**: the **only** CJK heading face in `CV-cn.tex`.
    **No fallback font** — the build fails hard if `fonts/HuiwenZhengKai.ttf` is missing.
    - Local: drop `HuiwenZhengKai.ttf` into `fonts/` (gitignored).
    - CI: the font is committed **encrypted** as `assets/HuiwenZhengKai.ttf.gz.enc`
      (gzip + AES-256-CBC, PBKDF2-HMAC-SHA256) because the personal-use licence forbids
      redistribution and GitHub's 48 KB secret limit rules out storing it as base64.
      The workflow decrypts it with the `HUIWEN_FONT_KEY` secret, checks the result
      against `assets/HuiwenZhengKai.ttf.sha256`, and finally asserts via `pdffonts`
      that the PDF really embeds `HuiwenZhengkai` (and no `FZYTK`).

    To re-seal after replacing the font locally:

    ```bash
    gzip -9 -c fonts/HuiwenZhengKai.ttf > /tmp/hw.gz
    openssl enc -aes-256-cbc -pbkdf2 -iter 200000 -md sha256 -salt \
      -pass env:HUIWEN_FONT_KEY -in /tmp/hw.gz -out assets/HuiwenZhengKai.ttf.gz.enc
    shasum -a 256 fonts/HuiwenZhengKai.ttf | awk '{print $1}' > assets/HuiwenZhengKai.ttf.sha256
    ```

> `CV-cn.tex` deliberately uses the **static** Noto Serif CJK SC family. The variable
> `Noto Serif SC` (`NotoSerifSC[wght].ttf`) has no separate bold face, and XeTeX ignores
> its `wght` axis — a bold request against it renders Regular weight without any error.

### Chinese punctuation

`CV-cn.tex` follows APA punctuation with Chinese content: `, . : ; ( )` instead of
`，。：；（）`, `\textit{}` instead of `《》`, periods inside closing quotes, and `\&`
before the final author in Chinese reference entries. CJK italics use `FakeSlant`
(Noto Serif CJK has no italic face).

## Local Compilation

If compiling locally with XeLaTeX:

```bash
texliveonfly --compiler=xelatex --terminal_only CV.tex
texliveonfly --compiler=xelatex --terminal_only CV-cn.tex
```

Compiled PDF files (`*.pdf`) and LaTeX auxiliary build files (`.aux`, `.log`, `.out`, etc.) are ignored by git to keep the repository clean and source-only.
