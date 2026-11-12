# LaTeX Style Guide & Templates

A single-page reference for LaTeX writing rules, with a macro pack and ready-to-compile document templates.

- **88 rules** in 18 groups, each with a Required / Recommended / Optional level, a document mode, and an aligned Don't / Do source comparison plus a rendered KaTeX preview where it helps.
- **Macro Pack**: five groups of definitions (`\R`, `\abs`, `\E`, `\dd`, …) with rendered previews and the full `mymath.sty` to copy or download.
- **Templates**: Article, Book/Report, Beamer and Homework × pdfLaTeX / XeLaTeX × Vietnamese / English, plus a custom Book/Report setup and a three-file Vietnamese exam template. Each file is shown in a source pane with its own copy and download, and `Download .zip` fetches the whole template as a single archive (plus the sample `refs.bib` for Book/Report only: Article, Homework and Beamer keep the bibliography inside `main.tex` in a `thebibliography` block).
- **Minimal switch** (Templates filter bar, off by default, remembered): swaps the custom Book/Report (XeLaTeX · Vietnamese) for a version with functional packages only. It is dimmed for Article, Beamer, Homework and Exam; Article is always the lean version.
- **Review**: a 21-row pitfalls table and a 12-item submission checklist that remembers what you ticked.
- **AI prompt**: a segmented control with four rule sets, each with its own copy and download: **Common** (9 lines for any template), **Article**, **Book/Report**, and **Full** (every rule, convention, common mistake and the checklist, `latex-rules.md`).

## Use

Open `index.html` in a browser (internet needed for the CDN libraries), or publish it with GitHub Pages:
**Settings → Pages → Deploy from a branch → `main` → `/ (root)`**.

No build step, no `npm install`. Dark is the default theme; the toggle in the top bar switches to light and the choice is remembered.

## Navigation

The left rail is the index: resources at the top, then filters and the rule groups (or macro groups, templates, review sections) for the current view. Selecting an item changes the URL, so every view can be linked to and the browser Back button works.

The rail's right edge is a drag handle — grab it to widen or narrow the index between 216 px and 42% of the window (max 520 px); the reading pane takes whatever is left. The handle shows a grab pill and a hairline on hover, and a brass line with a live `px` readout while dragging. Double-click it to go back to the default width. The chosen width is saved and restored before first paint. Below 900 px the rail collapses to the slide-over drawer and the handle is hidden.

| Route | Opens |
|---|---|
| `#/rules/LAB` | rule group |
| `#/rules/THM-05` | one rule, scrolled into view |
| `#/macros/operators` | macro group |
| `#/templates/book-xe-vi` | template |
| `#/templates/book-xe-vi/setup.tex` | template file |
| `#/review/pitfalls`, `#/review/checklist` | review section |
| `#/ai` | Markdown export |
| `#LAB-01` | old-style link, redirected to `#/rules/LAB-01` |

## Keyboard

| Key | Action |
|---|---|
| `Ctrl/⌘ K` or `/` | focus search |
| `↑` `↓` `⏎` | move through search results, open |
| `Esc` | close search, clear it, close the rail |
| `←` `→` | move within a focused filter (Type / Engine / Language) |
| `←` `→` | resize the index (focus the handle first); `Shift` for larger steps, `Home` / `End` for min / max |
| `j` / `k` | next / previous rule in the current group |
| `t` | switch theme |

## Edit

Everything lives in `index.html`:

| To change | Edit |
|---|---|
| Rules | `const RULES` — `[id, level, mode, title, explanation, don't, do, KaTeX preview]` |
| Rule groups | `const GR`, and `MD` / `LV` for mode and level labels |
| Pitfalls and checklist | `const DD`, `const CK` |
| Macros | `const MACROS`, `const KM` (preview macros), `const STY` (the generated `.sty`) |
| Template generator | `buildArticle()` (minimal Article, full environment names), `build()`, `thms()`, `body()`, `listcfg()`; extra Article environments come from `genExtra()` in the Macro Pack |
| Custom templates | `bookMain()`, `bookSetup()`, `bookMainMin()`, `bookSetupMin()`, `CUSTOM_BOOK_MIN` (swapped in by `applyMin()`), `EX_MAIN` / `EX_SETUP` / `EX_HEADER`, `CUSTOM_BOOK`, `CUSTOM_EXAM` |
| AI Markdown export | `guide()` (Full), `G_BODY` / `G_ART` / `G_BOOK` with `guideCommon()`, `guideArticle()`, `guideBook()` (short sets) |
| Colours and spacing | the token block at the top of `<style>` — `:root` for light, `.dark` for dark |
| Type | `Inter` (UI), `Newsreader` (titles), `JetBrains Mono` (code, IDs) |

Adding a rule to `RULES` is enough — the rail counts, the group reading view, search, deep links and the Markdown export all pick it up. A new group needs an entry in `GR` and an id prefix.

## Notes

- The comparison panes and template source are read-only; nothing is executed or validated in the browser.
- Long LaTeX lines wrap inside their panes and the pitfall table shrinks to the viewport, so the page never scrolls sideways — the rail width and gutters scale with the window.
- The top bar cannot wrap, so the search field is its only flexible item (`flex:1 1 0`, `min-width:0`): it gives up width first and the brand, scope chip and theme switch stay on screen down to a 320 px window. Without that, the input's default 20-character width acts as a floor and pushes the theme switch past the right edge.
- The Template filters are segmented controls: one track with a sliding knob, radio semantics (`←` / `→`), and only the results below them re-render so the selection visibly moves. Below 900px the Type control scrolls sideways and keeps the selected option in view.
- The `.zip` download is built in the browser with a small stored-mode ZIP writer, so it works offline and needs no library.
- Motion (ambient drift, group transition, panel spotlight, theme reveal) is disabled under `prefers-reduced-motion` and the theme switch falls back to an instant swap where the View Transitions API is unavailable.
- Printing (`Print rules` in the Export menu, or the browser's own print) drops the rail, bar and actions and prints the rule sheet.
