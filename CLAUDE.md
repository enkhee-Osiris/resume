# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an Org-mode resume that compiles to PDF via LaTeX. The main content file is `enkherdene_bolormaa.org`, styled by `enkherdene_bolormaa.sty`, with personal contact info separated into `personal-info.org`.

## Building

Compile the resume to PDF using Emacs with org-mode:

```sh
emacs --batch --eval '(setq org-confirm-babel-evaluate nil)' -l org enkherdene_bolormaa.org -f org-latex-export-to-pdf
```

Or interactively in Emacs: open `enkherdene_bolormaa.org` and use `C-c C-e l p` (org-export → LaTeX → PDF).

Requires: Emacs with org-mode, TeX Live (including `lato`, `titlesec`, `microtype`, `fullpage`, `xstring` packages), and `pdflatex`.

## Architecture

- `enkherdene_bolormaa.org` — main resume content in Org-mode markup; uses `#+INCLUDE: personal-info.org` to pull in contact macros and `#+LaTeX_HEADER` directives to load the custom style
- `personal-info.org` — defines Org macros (`FULL`, `BLOG`, `MAIL`, `PHONE`, `HEADER`) that are referenced in the main file via `{{{MACRO_NAME}}}`
- `enkherdene_bolormaa.sty` — custom LaTeX package defining layout, colors, fonts (Lato), and the `\resheader` command used by the `{{{HEADER}}}` macro. Header is a two-line layout: name on line 1, contact info (email | phone | blog) separated by muted `|` dividers on line 2. Section and header rules use a subtle `rule-color` (gray 0.75).

The `{{{HEADER}}}` macro expands to `\resheader{name}{blog}{email}{phone}` as defined in the `.sty` file. The years-of-experience in the Summary section uses an inline Elisp expression: `src_elisp[:results raw]{(- (string-to-number (format-time-string "%Y")) 2017)}` — this requires `eval:export` in `#+OPTIONS` and Emacs to evaluate during export.

## CI

`.github/workflows/deploy.yml` builds the PDF and deploys to GitHub Pages on every push to `main`. Requires GitHub Pages to be enabled in repository settings with Source set to "GitHub Actions". The PDF is available at `https://<username>.github.io/resume/enkherdene_bolormaa.pdf`.
