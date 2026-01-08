# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A BibTeX bibliography style (`OU.bst`) for Open University referencing, based on the Harvard `agsm.bst` style. Implements Cite Them Right Harvard format.

Reference: https://www.citethemrightonline.com/category-list?docid=CTRHarvard

## Build Commands

```bash
# Install to TeX Live
make install

# Build documentation (PostScript)
make harvard.ps

# Install documentation
make install_doc
```

The `prefix` variable in `Makefile` points to the TeX Live installation (default: `/usr/local/texlive/2020`).

## Key Files

- **OU.bst** - BibTeX style file for Open University Harvard referencing
- **harvard.sty** - LaTeX package providing citation commands (`\cite`, `\citeasnoun`, `\possessivecite`, `\citeyear`, `\citename`, `\citeaffixed`)

## OU.bst Features

### Custom Fields

| Field | Purpose |
|-------|---------|
| `place` | Place of publication (use instead of `address`) |
| `DOI` | Digital Object Identifier (auto-prefixed with `https://doi.org/`) |
| `URL` | Web address for online resources |
| `URLDate` | Access date for online resources |
| `director` | Film/video director |
| `distributor` | Film distribution company |
| `media` | Media format (e.g., "DVD") |
| `moduletitle` | OU module title |
| `translatedfrom` | Original language |
| `translatedby` | Translator name(s) |

### Entry Types

Standard: `article`, `book`, `booklet`, `inbook`, `incollection`, `inproceedings`, `conference`, `manual`, `mastersthesis`, `phdthesis`, `proceedings`, `techreport`, `unpublished`, `misc`

Custom OU types: `film`, `photograph`, `bookchapter`, `module`, `multimedia`

### Formatting

- All entry types support DOI/URL output
- Entries without year display "n.d." (no date)
- Edition format: "2nd edn" (user provides ordinal in `edition` field)
- Use `place` field for location (not `address`)

## BibTeX Style Architecture

The `.bst` file uses BibTeX's stack-based language:
- Entry types: `FUNCTION {article}`, `FUNCTION {book}`, etc.
- `format.*` functions handle field formatting
- `output.*` functions manage output state and punctuation
- `ENTRY` block defines available fields
- `DOI_or_URL` function outputs DOI (preferred) or URL with access date
