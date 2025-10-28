# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is an academic poster template repository designed for creating A0-sized conference posters in Japanese, specifically for the Shimokawa Lab (下川研). It uses the `tikzposter` document class with LuaLaTeX for flexible and visually appealing poster creation.

This template is intended to be used with the [Shimokawa Lab LaTeX environment](https://github.com/smkwlab/latex-environment). For other document types, dedicated templates are available:
- [Thesis template](https://github.com/smkwlab/sotsuron-template) for graduation theses
- [Weekly report template](https://github.com/smkwlab/wr-template) for weekly reports
- [General LaTeX template](https://github.com/smkwlab/latex-template) for basic documents

## Build Commands

The repository uses GitHub Actions for automated builds, but for local development:

```bash
# Using lualatex (required for tikzposter with Japanese support)
lualatex a0poster.tex

# Or using latexmk (configured in .latexmkrc)
latexmk a0poster.tex

# Clean build artifacts
latexmk -c

# View PDF (example)
open a0poster.pdf  # macOS
xdg-open a0poster.pdf  # Linux
```

Note: This template requires LuaLaTeX with Japanese font support (LuaTeX-ja).

## Key Architecture

- **a0poster.tex**: The primary LaTeX source file using `tikzposter` document class
- **GitHub Actions**: Automated build and release workflow using `ghcr.io/smkwlab/texlive-ja-textlint:2025d` Docker container via `smkwlab/latex-release-action@v2.2.0`
- **Output**: Generates `a0poster.pdf` (which is gitignored)

## Release Workflow

The repository automatically builds and releases PDFs when:
- Tags are pushed (creates GitHub releases with attached PDF)
- Pull requests are opened (builds PDF and uploads as workflow artifact for review)

## Important Configuration

The template uses:
- `tikzposter` document class (25pt font size, A0 paper, portrait orientation)
- `lualatex` engine for Unicode-based Japanese text processing
- `luatexja` and `luatexja-fontspec` for Japanese font support
- Simple theme with Slide block style (customizable)
- Two-column layout (50% each column)

## Working with the Template

When modifying `a0poster.tex`:
- The `tikzposter` class provides a flexible block-based layout system
- Use `\block{Title}{Content}` to create content blocks
- Organize content using `\begin{columns}` and `\column{width}` for multi-column layouts
- Japanese text is fully supported through LuaTeX-ja
- Customize appearance by changing themes: Simple, Minimal, Basic, etc.
- Customize block styles: Minimal, Basic, Slide, Default, etc.
- Pull requests automatically generate PDF artifacts for review

## Themes and Customization

Available themes (change with `\usetheme{}`):
- `Simple`: Clean and minimal design (default)
- `Minimal`: Ultra-minimal appearance
- `Basic`: Traditional academic poster style
- And many more in the tikzposter documentation

Available block styles (change with `\useblockstyle{}`):
- `Slide`: Modern presentation style (default)
- `Minimal`: Simple blocks without decoration
- `Basic`: Traditional bordered blocks
- `Default`: Standard tikzposter blocks

## Use Cases

This template is ideal for:
- Conference poster presentations
- Research symposium posters
- Lab meeting poster presentations
- Student research showcases
- Academic event poster displays
