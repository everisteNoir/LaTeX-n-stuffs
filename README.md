# LaTeX Style Guide & Templates

A single-page site (`index.html`) with:

- a LaTeX style guide (82 rules) with KaTeX previews,
- a macro pack (`mymath.sty`),
- templates: Article, Book/Report, Beamer, Homework (pdfLaTeX / XeLaTeX, Vietnamese / English) and an exam template,
- an "AI Prompt" tab that turns all rules into one Markdown text for AI assistants.

## Use

Open `index.html` in a browser (internet needed for the CDN libraries), or publish it with GitHub Pages:
**Settings → Pages → Deploy from a branch → `main` → `/ (root)`**.

## Edit

Everything lives in the script of `index.html`:

| To change | Edit |
|---|---|
| Rules | the `RULES` array |
| Rule groups | the `GR` object |
| Macros | `MACROS` and `KM` |
| Templates | `build()`, `thms()`, `body()` and the custom templates near the end of the script |
