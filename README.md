# 📚 kejian-skill-zh

> **课件总结 skill** — 将课件/讲义/PPT 转换为考试导向的复习资料

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE.txt) [![Skill](https://img.shields.io/badge/Claude-Skill-purple)](SKILL.md)

---

## 功能特性

- **多格式输入** — Markdown（优先）、纯文本、PDF（需 OCR 工具）
- **默认 Markdown 输出** — 可选 PDF（需 pandoc + LaTeX）
- **自动分段处理** — 长文档智能拆分，逐段阅读
- **双语术语** — 中文为主，重要术语附英文
- **页码引用** — 每个知识点标注来源页码
- **验证机制** — 确保内容覆盖率和准确性

## 安装

### 方式一：手动安装

将整个项目文件夹复制到你的 agent 的 skill 目录下：

```bash
# CLAUDE
git clone https://github.com/你的用户名/kejian-skill-zh.git ~/.claude/skills/kejian-skill-zh

# CODEX
git clone https://github.com/你的用户名/kejian-skill-zh.git ~/.agent/skills/kejian-skill-zh
```

### 方式二：通过 npx 安装（开发中）

```bash
npx skills install kejian-skill-zh
```

> ⚠️ 此方式尚在开发中，敬请期待

## 快速开始

### 方式 1：安装好全部依赖（推荐）

```
输入课件 → skill 自动处理 → 输出 Summary - <文件名>.md
```

### 方式 2：没有安装任何依赖

1. 将非 Markdown 课件扔给网页 AI，让其转成 Markdown
2. 将内容存入 `.md` 文件并用 skill 处理
3. 获得 `Summary - <文件名>.md`

### 方式 3：没有 Agent

1. 直接下载 [SKILL.md](SKILL.md)
2. 把需要总结的课件与 SKILL.md 一起喂给网页 AI
3. 获得网页文字版总结

## 工作流

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  输入文件   │ ──▶ │  格式转换   │ ──▶ │  全局阅读   │
│ MD/TXT/PDF  │     │（如需要）   │     │  建立分段   │
└─────────────┘     └─────────────┘     └─────────────┘
                                              │
                                              ▼
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  输出文件   │ ◀── │  验证检查   │ ◀── │  逐段阅读   │
│  .md / .pdf │     │  覆盖率    │     │  合并草稿   │
└─────────────┘     └─────────────┘     └─────────────┘
```

## 推荐工具

### 输入转换

| 工具 | 用途 | 特点 |
|------|------|------|
| [Marker](https://github.com/VikParuchuri/marker) | PDF → Markdown | 学术文档优化，质量高但较慢 |
| [Markitdown](https://github.com/microsoft/markitdown) | 多格式 → Markdown | 速度快，通用性强 |
| [Surya](https://github.com/VikParuchuri/surya) | 通用 OCR | 效果好，适合开发者 |
| [Pandoc](https://pandoc.org) | 格式转换 | 不支持输入 PDF，输出 PDF 需 LaTeX |

### Markdown 阅读器

| 阅读器 | 特点 | 平台 |
|--------|------|------|
| [Obsidian](https://obsidian.md/) | 功能强大，带笔记系统 ⭐推荐 | Win/Mac/Linux/Mobile |
| [VS Code](https://code.visualstudio.com/) | 开发者友好，插件丰富 | Win/Mac/Linux |
| [Typora](https://typora.io/) | 所见即所得，体验最好（收费） | Win/Mac/Linux |
| [Mark Text](https://github.com/marktext/marktext) | 开源免费，类似 Typora | Win/Mac/Linux |

### LaTeX 环境（可选，用于 PDF 输出）

| 工具 | 特点 |
|------|------|
| TeXWorks | 轻量级，适合初学者 |
| TeX Live | 完整发行版，功能全面 |
| MiKTeX | Windows 友好，按需安装包 |

## 项目结构

```
课件skill-zh/
├── SKILL.md                      # Skill 定义文件（核心）
├── README.md                     # 项目说明
├── LICENSE.txt                   # MIT 许可证
├── test-prompts.json             # 测试用例
└── references/
    ├── example-output.md         # 完整输出示例
    └── latex-style-guide.md      # LaTeX 排版规范
```

## 输出示例

```
Summary - 信号与系统第3章.md      # 默认输出
Summary - 信号与系统第3章.pdf     # 可选（需要 pandoc + LaTeX）
```

## 常见问题

<details>
<summary><strong>PPT 怎么处理？</strong></summary>

用 [Pandoc](https://pandoc.org) 转换为 Markdown，或手动提取内容。

</details>

<details>
<summary><strong>想输出其他格式（如 .docx）？</strong></summary>

安装 [Pandoc](https://pandoc.org)，告诉 agent 你的需求即可。

</details>


## 许可证

[MIT](LICENSE.txt) © 2026 Li Baichuan, Dai Zhengyu

## 相关链接

- [示例输出](references/example-output.md) — 完整的课件总结示例
- [LaTeX 排版规范](references/latex-style-guide.md) — 排版标准和常见问题
