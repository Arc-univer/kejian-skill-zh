# 📚 kejian-skill-zh

> **Courseware Summarization Skill** — Convert lecture slides, handouts, and textbooks into exam-focused study guides, cheat sheets, and key-point summaries

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE.txt) [![Skill](https://img.shields.io/badge/Claude-Skill-purple)](SKILL.md)

English | **[中文](README.md)**

---

## What Is This?

`kejian-skill-zh` is an AI Agent skill (for Claude Code and compatible platforms) purpose-built for **exam preparation**. Feed in a set of lecture notes (Markdown, PDF, or plain text) and it produces:

- **`Summary - <filename>.md`** — A structured Markdown review document (default)
- **`Summary - <filename>.pdf`** — A compiled PDF (optional, requires LaTeX)

The output is **exam-oriented**, not a generic chapter summary. It distills: core concepts, formulas, representative worked examples, problem-solving techniques, and common pitfalls. Every single knowledge point includes a **clickable link that jumps to the exact line in the source file**.

---

## Core Features

| Feature | Details |
|---------|---------|
| **Precise line-level links** | Every reference links to the exact source line (`[pp. 1468](source.md#L256)`). Click → jump directly to the content. |
| **Automatic chunking** | Long documents are intelligently split by lecture/topic, read section-by-section (parallel when possible), then merged globally. |
| **Independent validation** | After merging, a fresh validator checks coverage, link clickability, line-anchor correctness, bilingual terms, and exam relevance. Fails → back to revision. |
| **Bilingual terminology** | Primary language is Chinese; key technical terms are annotated with their original English names in parentheses (e.g., "指令集架构 (Instruction Set Architecture, ISA)"). |
| **Math formula preservation** | Formulas use LaTeX syntax (`$...$` / `$$...$$`), rendered correctly in any math-capable Markdown viewer. |
| **Multi-format input** | Markdown (preferred), plain text, PDF (direct reading or via Marker/Markitdown/Surya conversion). |
| **Minimal, purposeful diagrams** | Diagrams are included only when they substantively aid understanding (block diagrams, waveforms, pole-zero plots). No decorative fluff. |
| **Exam-focused output** | Priority tagging (🔴 Must-know / ⚡ Important / 📌 Understand), representative problem patterns, and test-taking tips. |

---

## Output Structure (Preview)

```markdown
# Course Name · Chapter Title

## Core Concepts

### CPU Time Formula [pp. 1468-1534](source.md#L256-L420)

**Definition**: CPU Time = IC × CPI × T_c [pp. 1468](source.md#L256)

**Formula**:
$$CPU\ Time = IC \times CPI \times T_c$$
*Source: [pp. 1470](source.md#L280)*

**Worked Example**: Given IC=10⁶, CPI=2.5, f=2GHz, compute CPU Time [pp. 1500](source.md#L350)

**Common Pitfalls**:
- CPI is independent of clock frequency [pp. 1520](source.md#L400)

---

## Exam Key Points

| Priority | Topic | Page (click to jump to source line) |
|----------|-------|-------------------------------------|
| 🔴 **Must-know** | CPU Time formula & comprehensive calculation | [pp. 1468-1534](source.md#L256-L420) |
| ⚡ **Important** | CPI — meaning, factors, optimization | [pp. 1476-1518](source.md#L435-L510) |
| 📌 **Understand** | Instruction execution cycle | [pp. 754-782](source.md#L180-L245) |
```

> **Click any `pp.` link to jump directly to the starting line of that content in the source file.** No more scrolling through hundreds of lines hunting for a concept.

---

## Pipeline: Controller → Readers → Validator

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  Receive  │───▶│  Global   │───▶│  Chunk    │───▶│  Section  │
│  Input    │    │  Read+Map │    │ by Topic  │    │  Read     │
└──────────┘    └──────────┘    └──────────┘    └─────┬─────┘
                                                       │
┌──────────┐    ┌──────────┐    ┌──────────┐          │
│  Write    │◀───│  Validator│◀───│  Merge   │◀─────────┘
│  Output   │    │  (fresh)  │    │  Draft   │
└──────────┘    └──────────┘    └──────────┘
```

### Key Roles

- **Controller** — performs a global read of the entire document, builds a section map, delegates to readers, merges draft, normalizes style, and reports results
- **Section Reader** — one per independent lecture block or topic chunk; returns structured notes (key points, formulas, **line numbers**, English terms); never writes the final document
- **Validator** — a fresh-context reviewer that checks coverage, verifies every page link is clickable with correct line anchors, audits bilingual terminology, and assesses exam utility. Returns `Pass` / `Pass with notes` / `Fail`

---

## Installation

### Option 1: Install via npx

```bash
npx skills add Arc-univer/kejian-skill-zh --skill kejian-skill-zh
```

### Option 2: Manual Installation

```bash
# CLAUDE CODE
git clone https://github.com/Arc-univer/kejian-skill-zh.git ~/.claude/skills/kejian-skill-zh

# CODEX
git clone https://github.com/Arc-univer/kejian-skill-zh.git ~/.agent/skills/kejian-skill-zh
```

---

## Quick Start

### Path 1: Full Setup (Recommended)

```
User: "Summarize 'Computer Systems Overview' — exam key points only"
      ↓
Skill auto: global read → chunk → per-section extract (with line numbers)
            → merge → validate → write file
      ↓
Output: Summary - Computer Systems Overview.md (every point links to source lines)
```

### Path 2: Without any conversion tool

1. Convert non-Markdown source to Markdown using a web-based AI
2. Save as `.md` and proceed with Path 1

### Path 3: No Agent Environment

1. Download [SKILL.md](SKILL.md)
2. Feed the courseware + SKILL.md to a web-based AI (Claude / ChatGPT / Gemini)
3. Receive a text summary (same structure, no line-anchor navigation)

---

## Recommended Companion Tools

### Input Conversion (PDF → Markdown)

| Tool | Purpose | Quality | Speed |
|------|---------|---------|-------|
| [Marker](https://github.com/VikParuchuri/marker) | PDF → Markdown | ⭐⭐⭐ Best | Slower |
| [Markitdown](https://github.com/microsoft/markitdown) | Multi-format → Markdown | ⭐⭐ Good | Fast |
| [Surya](https://github.com/VikParuchuri/surya) | General-purpose OCR | ⭐⭐ Good | Moderate |
| [Pandoc](https://pandoc.org) | Format conversion | ⭐⭐ Good | Fast |

> **Recommended combo**: Convert academic PDFs with Marker → summarize with this skill

### Markdown Viewers (for `.md` output)

| Viewer | Math Rendering | Link Navigation | Platform | Notes |
|--------|---------------|-----------------|----------|-------|
| [Obsidian](https://obsidian.md/) | ✅ | ✅ | All | ⭐ Top pick |
| [VS Code](https://code.visualstudio.com/) | ✅ (plugin) | ✅ | All | Dev-friendly |
| [Typora](https://typora.io/) | ✅ | ✅ | All | WYSIWYG (paid) |
| [Mark Text](https://github.com/marktext/marktext) | ✅ | ✅ | All | Free & open-source |

> **Obsidian and VS Code natively support `#L<line>` anchor navigation** — clicking a page-reference link jumps straight to the matching line in the source file.

### LaTeX Environment (Optional — PDF output only)

| Tool | Notes |
|------|-------|
| [TeXWorks](https://www.tug.org/texworks/) | Lightweight, beginner-friendly |
| [TeX Live](https://www.tug.org/texlive/) | Full distribution |
| [MiKTeX](https://miktex.org/) | Windows-friendly, on-demand package install |

---

## Project Structure

```
kejian-skill-zh/
├── SKILL.md                      # Skill definition (core logic)
├── README.md                     # Documentation (Chinese)
├── README.en.md                  # Documentation (English)
├── LICENSE.txt                   # MIT License
├── .gitignore
├── test-prompts.json             # Evaluation test prompts
└── references/
    ├── example-output.md         # Full output example (LaTeX version)
    └── latex-style-guide.md      # LaTeX typesetting conventions & troubleshooting
```

---

## FAQ

<details>
<summary><strong>How do I handle PPT/PPTX files?</strong></summary>

1. PPTX files:
  - Install [Pandoc](https://pandoc.org) or [Markitdown](https://github.com/microsoft/markitdown) to convert to Markdown (the skill will auto-detect and process), then continue normally. If neither tool is available, manually extract the text content into a `.md` file.
2. PPT files (legacy format):
  - [Pandoc](https://pandoc.org) does not support the old `.ppt` format. Install [Markitdown](https://github.com/microsoft/markitdown) instead, or feed it to a web-based AI and save as `.md` manually.

</details>

<details>
<summary><strong>What about scanned (image-based) PDFs?</strong></summary>

OCR is required first. Install [Marker](https://github.com/VikParuchuri/marker) (optimized for academic documents) or [Surya](https://github.com/VikParuchuri/surya) (general-purpose OCR) to convert the PDF to Markdown (the skill will auto-detect and process). Directly reading scanned PDFs yields poor quality — formulas and symbols may be lost.

</details>

<details>
<summary><strong>I want PDF output but don't want to install LaTeX. Alternatives?</strong></summary>

Two alternatives:
1. Open the `.md` in Obsidian and export to PDF via plugin
2. Use VS Code + Markdown PDF extension

</details>

<details>
<summary><strong>Can I export to .docx?</strong></summary>

Yes. With Pandoc installed, tell the agent you want `.docx` output: `pandoc Summary-xxx.md -o Summary-xxx.docx`

</details>

<details>
<summary><strong>Will summarizing a 300+ page textbook lose content?</strong></summary>

No. The skill enforces mandatory chunking: long documents must be split by lecture/topic into independent sections, each read and extracted separately, then globally merged and validated. The validator checks that every section in the segment map has coverage in the final draft. A single missing section = fail.

</details>

<details>
<summary><strong>How is this different from just asking an AI to "summarize this"?</strong></summary>

| Plain AI Summary | This Skill |
|------------------|------------|
| One-pass read; later sections tend to drift | Enforced chunking + independent validation |
| Page references often missing or inaccurate | Every knowledge point has a precise line-number link |
| May produce vague prose summaries | Structured key-point output with priority tags + pitfalls |
| English terminology often dropped | Bilingual terms are a mandatory deliverable |
| Single conversation round | Multi-round validation until passing, then file write |

</details>

---

## Design Principles

1. **Non-skippable validation** — Merged drafts must pass a fresh validator review. Fail = rework.
2. **Page references are links, not decoration** — Must be clickable, must jump to the exact source line.
3. **Chinese + English bilingual annotation** — Key terms include original English on first occurrence.
4. **Mandatory chunking for long documents** — Summarizing a 300-page textbook in one pass is forbidden.
5. **Diagrams only when needed** — Include a visual only when it substantively clarifies a concept.

---

## License

[MIT](LICENSE.txt) © 2026 Li Baichuan, Dai Zhengyu

---

## Links

- [SKILL.md](SKILL.md) — Complete skill definition and execution rules
- [Example Output](references/example-output.md) — A full courseware summary sample (LaTeX)
- [LaTeX Style Guide](references/latex-style-guide.md) — Typesetting standards, common issues & solutions
- [Test Prompts](test-prompts.json) — Evaluation prompts for skill quality assessment
