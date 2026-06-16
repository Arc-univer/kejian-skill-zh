# 📚 kejian-skill-zh

> **Courseware Summarization Skill** — Convert lecture notes, slides, and handouts into exam-focused study material

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE.txt) [![Skill](https://img.shields.io/badge/Claude-Skill-purple)](SKILL.md)

English | **[中文](README.md)**

---

## Features

- **Multi-format input** — Markdown (preferred), plain text, PDF (requires OCR tooling)
- **Markdown by default** — PDF export optional (requires pandoc + LaTeX)
- **Automatic chunking** — Intelligently splits long documents, reads section by section
- **Bilingual terminology** — Chinese as primary language, key terms annotated in English
- **Page references** — Every knowledge point traced back to its source page
- **Validation** — Ensures content coverage and accuracy

## Installation

### Option 1: Install via npx

```bash
npx skills add Arc-univer/kejian-skill-zh --skill kejian-skill-zh
```

### Option 2: Manual installation

Clone the entire project into your agent's skill directory:

```bash
# CLAUDE
git clone https://github.com/Arc-univer/kejian-skill-zh.git ~/.claude/skills/kejian-skill-zh

# CODEX
git clone https://github.com/Arc-univer/kejian-skill-zh.git ~/.agent/skills/kejian-skill-zh
```

## Quick Start

### Path 1: Full dependencies installed (recommended)

```
Feed in courseware → skill processes automatically → outputs Summary - <filename>.md
```

### Path 2: No dependencies installed

1. Paste non-Markdown courseware into a web-based AI and ask it to convert to Markdown
2. Save the output to a `.md` file and run the skill on it
3. Get `Summary - <filename>.md`

### Path 3: No agent available

1. Download [SKILL.md](SKILL.md) directly
2. Feed the courseware along with SKILL.md into a web-based AI
3. Get a plain-text summary in the browser

## Workflow

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Input File │ ──▶ │   Convert   │ ──▶ │  Skim Full  │
│ MD/TXT/PDF  │     │ (if needed) │     │  Build Map  │
└─────────────┘     └─────────────┘     └─────────────┘
                                              │
                                              ▼
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ Output File │ ◀── │  Validate   │ ◀── │ Deep-Read   │
│  .md / .pdf │     │  Coverage   │     │  per Chunk  │
└─────────────┘     └─────────────┘     └─────────────┘
```

## Recommended Tools

### Input Conversion

| Tool | Purpose | Notes |
|------|---------|-------|
| [Marker](https://github.com/VikParuchuri/marker) | PDF → Markdown | Optimized for academic docs; high quality, slower |
| [Markitdown](https://github.com/microsoft/markitdown) | Multi-format → Markdown | Fast and versatile |
| [Surya](https://github.com/VikParuchuri/surya) | General-purpose OCR | Solid results, developer-friendly |
| [Pandoc](https://pandoc.org) | Format conversion | Cannot import PDF; PDF export requires LaTeX |

### Markdown Viewers

| Viewer | Highlights | Platform |
|--------|------------|----------|
| [Obsidian](https://obsidian.md/) | Full-featured with built-in note system ⭐ Recommended | Win/Mac/Linux/Mobile |
| [VS Code](https://code.visualstudio.com/) | Developer-friendly, rich plugin ecosystem | Win/Mac/Linux |
| [Typora](https://typora.io/) | WYSIWYG, best reading experience (paid) | Win/Mac/Linux |
| [Mark Text](https://github.com/marktext/marktext) | Open-source, free Typora alternative | Win/Mac/Linux |

### LaTeX Environment (optional, for PDF export)

| Tool | Notes |
|------|-------|
| TeXWorks | Lightweight, beginner-friendly |
| TeX Live | Full distribution, feature-complete |
| MiKTeX | Windows-friendly, installs packages on demand |

## Project Structure

```
kejian-skill-zh/
├── SKILL.md                      # Skill definition (core)
├── README.md                     # Project documentation (Chinese)
├── README.en.md                  # Project documentation (English)
├── LICENSE.txt                   # MIT License
├── test-prompts.json             # Test cases
└── references/
    ├── example-output.md         # Full output example
    └── latex-style-guide.md      # LaTeX typesetting guide
```

## Output Example

```
Summary - Signals and Systems Ch.3.md      # Default output
Summary - Signals and Systems Ch.3.pdf     # Optional (requires pandoc + LaTeX)
```

## FAQ

<details>
<summary><strong>How do I handle PPT files?</strong></summary>

Convert to Markdown using [Pandoc](https://pandoc.org), or extract the content manually.

</details>

<details>
<summary><strong>Can I export to other formats (e.g. .docx)?</strong></summary>

Install [Pandoc](https://pandoc.org) and let the agent know what you need.

</details>

## License

[MIT](LICENSE.txt) © 2026 Li Baichuan, Dai Zhengyu

## Links

- [Example Output](references/example-output.md) — A complete courseware summary sample
- [LaTeX Style Guide](references/latex-style-guide.md) — Typesetting standards and common pitfalls
