# resume

My personal resume built with Org-mode and LaTeX.

## Building

```sh
emacs --batch -l org enkherdene_bolormaa.org -f org-latex-export-to-pdf
```

**Requirements:** Emacs, TeX Live (`lato`, `titlesec`, `microtype`, `fullpage`, `xstring`)

Or interactively in Emacs: `C-c C-e l p`

## CI

Pushing to `main` automatically builds the PDF via GitHub Actions. Download it from the **Actions** tab → latest run → **Artifacts → resume**. Artifacts expire after 90 days.

## Structure

| File | Purpose |
|------|---------|
| `enkherdene_bolormaa.org` | Resume content |
| `personal-info.org` | Contact info macros |
| `enkherdene_bolormaa.sty` | LaTeX style |
