# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a fork of the Harvard bibliography styles (v2.0.5) for LaTeX/BibTeX, extended with a custom `OU.bst` style file for Open University referencing requirements. The Harvard family provides author-date citation styles commonly used in academic writing.

## Build Commands

```bash
# Build documentation (PostScript)
make harvard.ps

# Install styles to TeX Live
make install

# Install documentation
make install_doc

# Clean build artefacts
make clean
```

The `prefix` variable in `Makefile` points to the TeX Live installation (default: `/usr/local/texlive/2020`).

## Key Files

- **OU.bst** - Custom BibTeX style for Open University, based on `agsm.bst`. Adds support for:
  - DOI field with automatic `https://doi.org/` prefix
  - URL and URLDate fields for online resources
  - Translation fields (translatedby, translatedfrom, translationyear)
  - Film/video entries (director, distributor, media, place)
  - Module content (moduletitle)
  - Additional entry types: `@film`, `@photograph`, `@bookchapter`, `@module`, `@multimedia`

- **harvard.sty** - LaTeX package providing citation commands (`\cite`, `\citeasnoun`, `\possessivecite`, `\citeyear`, `\citename`, `\citeaffixed`)

- **harvard.tex** - Documentation source; compile with `latex` + `bibtex`

## BibTeX Style Architecture

The `.bst` files use BibTeX's stack-based language. Key functions in `OU.bst`:
- Entry types defined as `FUNCTION {article}`, `FUNCTION {book}`, etc.
- `format.*` functions handle field formatting
- `output.*` functions manage output state and punctuation
- `ENTRY` block defines available fields for bibliography entries
