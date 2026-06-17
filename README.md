# 📚 kejian-skill-zh

> **课件总结 Skill** — 将课件/讲义/PPT/Slides 转换为考试导向的复习资料、考点速查表或 Cheat Sheet

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE.txt) [![Skill](https://img.shields.io/badge/Claude-Skill-purple)](SKILL.md)

中文 | **[English](README.en.md)**

---

## 这是什么？

`kejian-skill-zh` 是一个面向 AI Agent（Claude Code 等）的 Skill，专为**备考复习**场景设计。输入一份课件（Markdown、PDF、纯文本），自动产出：

- **`Summary - <文件名>.md`** — 结构化的 Markdown 复习文档（默认）
- **`Summary - <文件名>.pdf`** — 编译后的 PDF（可选，需 LaTeX）

输出内容聚焦**考点**而非泛泛的章节摘要：核心概念、公式、典型例题、解题技巧、易错点，每一项都附带**指向源文件精确行的可点击链接**。

---

## 核心特性

| 特性 | 说明 |
|------|------|
| **精确行号跳转** | 每个知识点链接到源文件对应行号（`[pp. 1468](源文件.md#L256)`），点击直接定位 |
| **自动分段处理** | 长文档智能按课时/主题拆分，逐段并行阅读，最后全局合并 |
| **独立验证机制** | 合并后运行全新验证器检查覆盖率、页码引用、双语术语、考试实用性 |
| **中英双语术语** | 中文为主，重要概念在括号中附英文原名（如 "指令集架构 (Instruction Set Architecture, ISA)"） |
| **数学公式保留** | 使用 LaTeX 语法（`$...$` / `$$...$$`），在支持渲染的阅读器中正确显示 |
| **多格式输入** | Markdown（推荐）、纯文本、PDF（支持直接读取或通过 Marker/Markitdown/Surya 转换） |
| **图表按需保留** | 仅保留对理解有实质帮助的图表（框图、波形图、零极点图等），不堆砌装饰 |
| **考试导向** | 输出包含考试重点优先级（🔴必考 / ⚡重点 / 📌理解）、典型例题模式和解题技巧 |

---

## 输出结构预览

```markdown
# 课程名 · 章节名

## 核心概念

### CPU 时间公式 [pp. 1468-1534](源文件.md#L256-L420)

**定义**：CPU 时间 = 指令数 × CPI × 时钟周期 [pp. 1468](源文件.md#L256)

**公式**：
$$CPU\ Time = IC \times CPI \times T_c$$
*来源：[pp. 1470](源文件.md#L280)*

**典型例题**：已知 IC=10⁶, CPI=2.5, f=2GHz，求 CPU 时间 [pp. 1500](源文件.md#L350)

**易错点**：
- CPI 与时钟频率无关 [pp. 1520](源文件.md#L400)

---

## 考试重点

| 优先级 | 知识点 | 页码（点击跳转到源文件对应行） |
|--------|--------|------|
| 🔴 **必考** | CPU 时间公式及综合计算 | [pp. 1468-1534](源文件.md#L256-L420) |
| ⚡ **重点** | CPI 的含义、影响因素、优化方向 | [pp. 1476-1518](源文件.md#L435-L510) |
| 📌 **理解** | 指令执行周期（取指→译码→…→写回） | [pp. 754-782](源文件.md#L180-L245) |
```

> **点击任意 `pp.` 链接，直接跳转到源文件对应内容的起始行。** 不在几百行的文件中手动翻找。

---

## 工作流（Controller → Readers → Validator）

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│ 接收输入  │───▶│ 全局阅读  │───▶│ 按课时分段 │───▶│ 逐段阅读  │
│ MD/TXT/PDF│    │ 建立地图  │    │ 划分主题块 │    │并行/顺序  │
└──────────┘    └──────────┘    └──────────┘    └─────┬────┘
                                                       │
┌──────────┐    ┌──────────┐    ┌──────────┐          │
│ 输出文件  │◀───│ 写入磁盘  │◀───│ 全新验证  │◀─────────┘
│ .md/.pdf  │    │ 最终检查  │    │ 覆盖率/链接│  合并草稿
└──────────┘    └──────────┘    └──────────┘
```

### 关键角色

- **控制器（Controller）** — 全局阅读、分段决策、合并草稿、样式规范化、最终报告
- **段落阅读器（Section Reader）** — 每个独立课时/主题段一个，返回结构化笔记（考点、公式、**行号**、英文术语）
- **验证器（Validator）** — 全新上下文，独立检查覆盖率、页码链接可点击性、行号锚点正确性、考试实用性。不通过则退回修改

---

## 安装

### 方式一：通过 npx 安装

```bash
npx skills add Arc-univer/kejian-skill-zh --skill kejian-skill-zh
```

### 方式二：手动安装

```bash
# CLAUDE CODE
git clone https://github.com/Arc-univer/kejian-skill-zh.git ~/.claude/skills/kejian-skill-zh

# CODEX
git clone https://github.com/Arc-univer/kejian-skill-zh.git ~/.agent/skills/kejian-skill-zh
```

---

## 快速开始

### 路径 1：完整环境（推荐）

```
用户：总结一下 "计算机系统概论"，我只要考点
      ↓
Skill 自动：全局阅读 → 分段 → 逐段提取考点+行号 → 合并 → 验证 → 写入文件
      ↓
产出：Summary - 计算机系统概论.md（每个考点链到源文件对应行）
```

### 路径 2：没有任何转换工具

1. 将非 Markdown 课件丢给网页 AI 转换成 Markdown
2. 保存为 `.md` 文件，按路径 1 处理

### 路径 3：没有 Agent 环境

1. 下载 [SKILL.md](SKILL.md)
2. 将课件 + SKILL.md 一起发给网页 AI（Claude / ChatGPT / Gemini）
3. 获得文字版总结（无行号跳转功能，但结构相同）

---

## 推荐配套工具

### 输入转换（PDF → Markdown）

| 工具 | 用途 | 质量 | 速度 |
|------|------|------|------|
| [Marker](https://github.com/VikParuchuri/marker) | PDF → Markdown | ⭐⭐⭐ 最佳 | 较慢 |
| [Markitdown](https://github.com/microsoft/markitdown) | 多格式 → Markdown | ⭐⭐ 良好 | 快 |
| [Surya](https://github.com/VikParuchuri/surya) | 通用 OCR | ⭐⭐ 良好 | 中等 |
| [Pandoc](https://pandoc.org) | 格式转换 | ⭐⭐ 良好 | 快 |

> **推荐组合**：用 Marker 转换学术 PDF → 用本 Skill 生成复习文档

### Markdown 阅读器（查看 `.md` 输出）

| 阅读器 | 数学公式 | 链接跳转 | 平台 | 推荐 |
|--------|----------|----------|------|------|
| [Obsidian](https://obsidian.md/) | ✅ | ✅ | 全平台 | ⭐ 推荐 |
| [VS Code](https://code.visualstudio.com/) | ✅ (插件) | ✅ | 全平台 | 开发者首选 |
| [Typora](https://typora.io/) | ✅ | ✅ | 全平台 | 所见即所得（收费） |
| [Mark Text](https://github.com/marktext/marktext) | ✅ | ✅ | 全平台 | 开源免费 |

> **Obsidian 和 VS Code 原生支持 `#L<行号>` 锚点跳转**，点击页码链接直接定位到源文件对应行。

### LaTeX 环境（可选，仅 PDF 输出需要）

| 工具 | 特点 |
|------|------|
| [TeXWorks](https://www.tug.org/texworks/) | 轻量级，适合初学者 |
| [TeX Live](https://www.tug.org/texlive/) | 完整发行版 |
| [MiKTeX](https://miktex.org/) | Windows 友好，按需安装包 |

---

## 项目结构

```
kejian-skill-zh/
├── SKILL.md                      # Skill 定义文件（核心逻辑）
├── README.md                     # 项目说明（中文）
├── README.en.md                  # 项目说明（英文）
├── LICENSE.txt                   # MIT 许可证
├── .gitignore
├── test-prompts.json             # 测试用例
└── references/
    ├── example-output.md         # 完整输出示例（LaTeX 版）
    └── latex-style-guide.md      # LaTeX 排版规范与常见问题
```

---

## 常见问题

<details>
<summary><strong>PPT/PPTX 文件怎么处理？</strong></summary>

1. PPTX 文件：
  - 安装 [Pandoc](https://pandoc.org) 或 [Markitdown](https://github.com/microsoft/markitdown) 转换为 Markdown（skill 会自动检测处理），然后按正常流程处理。如果上述工具不可用，手动提取文本内容存入 `.md` 文件。
2. PPT 文件：
  - [Pandoc](https://pandoc.org) 不支持旧版的格式，推荐安装 [Markitdown](https://github.com/microsoft/markitdown) 转换。或者喂给网页 AI，手动放入 .md 文件

</details>

<details>
<summary><strong>扫描版 PDF（图片型）能处理吗？</strong></summary>

需要先 OCR。推荐安装 [Marker](https://github.com/VikParuchuri/marker)（学术文档优化）或 [Surya](https://github.com/VikParuchuri/surya)（通用 OCR）将 PDF 转为 Markdown（skill 会自动检测处理）。直接读取扫描版 PDF 识别质量差，公式和符号可能丢失。

</details>

<details>
<summary><strong>想输出 PDF 但不想装 LaTeX？</strong></summary>

有几种替代方案：
1. 在 Obsidian 中打开 `.md` 文件，用插件导出 PDF
2. 用 VS Code + Markdown PDF 插件导出

</details>

<details>
<summary><strong>能输出 .docx 吗？</strong></summary>

可以。安装 Pandoc 后，告诉 Agent "输出 docx" 即可：`pandoc Summary-xxx.md -o Summary-xxx.docx`

</details>

<details>
<summary><strong>总结几百页的课件会不会丢内容？</strong></summary>

不会。Skill 内置强制分段机制：长文档必须先按课时/主题拆分为独立段落，逐段阅读提取，再全局合并验证。验证器会检查分段地图中的每段是否都在最终草稿中有体现，缺一段都会标记为不通过。

</details>

<details>
<summary><strong>和直接让 AI "总结一下这个课件" 有什么区别？</strong></summary>

| 直接让 AI 总结 | 使用本 Skill |
|----------------|-------------|
| 一次性通读，后半截容易偏移 | 强制分段 + 独立验证 |
| 页码引用可能丢失或不准 | 每个知识点带精确行号链接 |
| 可能输出泛泛的散文摘要 | 结构化考点 + 优先级 + 易错点 |
| 英文术语可能遗漏 | 双语术语是核心交付物 |
| 一次对话即结束 | 多轮验证直到通过才写入文件 |

</details>

---

## 设计原则

1. **不可跳过的验证** — 合并草稿后必须经过全新验证器检查，不通过不回退
2. **页码引用是链接，不是装饰** — 必须可点击、必须能跳转到精确行号
3. **中文 + 英文双语标注** — 重要概念首次出现时必须附英文原名
4. **长文档强制分段** — 禁止一次性总结几百页的课件
5. **图表按需保留** — 只在概念确实需要图示时才包含，不堆砌

---

## 许可证

[MIT](LICENSE.txt) © 2026 Li Baichuan, Dai Zhengyu

---

## 相关链接

- [SKILL.md](SKILL.md) — Skill 完整定义和执行规则
- [示例输出](references/example-output.md) — LaTeX 版课件总结示例
- [LaTeX 排版规范](references/latex-style-guide.md) — 排版标准、常见问题与解决方案
- [测试用例](test-prompts.json) — 用于评估 Skill 效果的测试提示词
