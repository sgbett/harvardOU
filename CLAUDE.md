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

## Adding Cite Them Right Example Comments

Each entry type function in OU.bst should have example comments showing the correct reference format. To add examples for a new entry type:

### Process

1. **Get the Cite Them Right source**: Download the relevant page from https://www.citethemrightonline.com as XML and save to `citethemright/<entrytype>.xml`. The user can log in via their institution and save page source.

2. **Read the XML file**: Extract the "Reference list" examples from the XML. Look for `<strong>Reference list</strong>` sections followed by `<p>` tags containing the formatted examples.

3. **Find the function in OU.bst**: Search for `FUNCTION {<entrytype>}` and locate the closing brace `}`.

4. **Add comments before the closing brace**: Insert examples as comments between `fin.entry` and `}`:
   ```
     fin.entry

   % Example description:
   % Author, A. (Year) Title details. Publisher.
   }
   ```

5. **Verify format matches**: Ensure the example format matches what the OU.bst function produces. Note any discrepancies (e.g., place of publication was removed in 2025 update).

### Entry Types with Examples Added

- `article` - journal articles (print, DOI, URL, article number)
- `book` - printed books (one author, multiple authors, editors, no author, organisation, editions)
- `bookchapter` - chapters in edited books
- `film` - films/movies
- `module` - web pages / OU module materials

### Entry Types Still Needing Examples

- `misc`, `multimedia`, `photograph`, `incollection`
- Standard types: `booklet`, `inbook`, `inproceedings`, `conference`, `manual`, `mastersthesis`, `phdthesis`, `proceedings`, `techreport`, `unpublished`

### Notes

- The Cite Them Right 13th edition (2025) removed place of publication for books
- OU follows this updated style
- When examples don't match the function output, update the function to match Cite Them Right (after verification)
