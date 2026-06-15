# LaTeX 课件总结排版规范

> 本文件定义课件总结 LaTeX 输出的排版标准和常见问题解决方案。

---

## 文档结构

### 标准 preamble

```latex
\documentclass[11pt,a4paper]{article}
\usepackage[UTF8]{ctex}          % 中文支持
\usepackage{amsmath,amssymb}     % 数学公式
\usepackage{geometry}            % 页面设置
\usepackage{enumitem}            % 列表定制
\usepackage{tikz}                % 绘图
\usepackage{pgfplots}            % 数据图表
\usepackage{xcolor}              % 颜色支持
\usepackage{hyperref}            % 超链接

\geometry{margin=2.5cm}
\setlength{\parindent}{0pt}
\setlength{\parskip}{6pt}
```

### 文档结构

```latex
\title{课程名 · 章节名}
\author{课件总结}
\date{\today}

\begin{document}
\maketitle
\tableofcontents  % 可选，长文档建议加

\section{核心概念}
\subsection{概念1}
% 内容...

\section{重要性质}
% 内容...

\section{典型例题}
% 内容...

\section{易错点}
% 内容...

\section{考试重点}
% 内容...

\end{document}
```

---

## 排版规范

### 1. 标题层级

- `\section{}` - 一级标题（核心概念、重要性质、典型例题等）
- `\subsection{}` - 二级标题（具体知识点）
- `\subsubsection{}` - 三级标题（很少用，避免过度嵌套）

### 2. 公式排版

**行内公式**：用 `$...$`
```latex
信号 $x(t)$ 的傅里叶变换为 $X(\omega)$
```

**独立公式**：用 `equation` 或 `align`
```latex
\begin{equation}
X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} dt
\end{equation}
```

**多行对齐**：用 `align`
```latex
\begin{align}
a_n &= \frac{2}{T} \int_{T} x(t) \cos(n\omega_0 t) dt \\
b_n &= \frac{2}{T} \int_{T} x(t) \sin(n\omega_0 t) dt
\end{align}
```

### 3. 列表排版

**无序列表**：
```latex
\begin{itemize}
  \item 第一点
  \item 第二点
\end{itemize}
```

**有序列表**：
```latex
\begin{enumerate}
  \item 第一步
  \item 第二步
\end{enumerate}
```

**紧凑列表**（节省空间）：
```latex
\begin{itemize}[noitemsep,topsep=0pt]
  \item 第一点
  \item 第二点
\end{itemize}
```

### 4. 表格排版

**标准表格**：
```latex
\begin{center}
\begin{tabular}{|l|c|r|}
\hline
\textbf{信号} & \textbf{公式} & \textbf{说明} \\
\hline
$\delta(t)$ & $1$ & 单位冲激 \\
\hline
$u(t)$ & $\frac{1}{j\omega}$ & 单位阶跃 \\
\hline
\end{tabular}
\end{center}
```

### 5. 强调与标注

**重点标注**：
```latex
\textbf{重要}：这个公式必须记住

\textcolor{red}{易错}：积分区间不要选错

\textcolor{blue}{技巧}：利用奇偶性简化计算
```

**定义框**：
```latex
\begin{center}
\fbox{\parbox{0.8\textwidth}{
\textbf{定义}：傅里叶变换是将时域信号转换为频域表示的数学工具
}}
\end{center}
```

---

## 常见问题解决

### 问题1：中文显示乱码

**原因**：缺少中文支持包

**解决**：
```latex
\usepackage[UTF8]{ctex}
```

### 问题2：公式编号混乱

**原因**：使用了 `equation*` 或手动去掉了编号

**解决**：
- 需要编号：用 `equation`
- 不需要编号：用 `equation*`

### 问题3：图片位置不听话

**原因**：LaTeX 浮动体机制

**解决**：
```latex
\begin{figure}[htbp]  % h=here, t=top, b=bottom, p=page
\centering
% 图片内容
\caption{图片说明}
\end{figure}
```

### 问题4：表格太宽超出页面

**原因**：表格内容太多

**解决**：
```latex
\begin{table}[htbp]
\centering
\resizebox{\textwidth}{!}{  % 自动缩放
\begin{tabular}{...}
% 表格内容
\end{tabular}
}
\end{table}
```

### 问题5：公式太长换行

**原因**：单行公式超出页面宽度

**解决**：
```latex
\begin{multline}
x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(\omega) e^{j\omega t} d\omega \\
+ \sum_{n=1}^{\infty} [a_n \cos(n\omega_0 t) + b_n \sin(n\omega_0 t)]
\end{multline}
```

### 问题6：编译错误 "Undefined control sequence"

**原因**：缺少宏包

**解决**：检查是否引入了所需宏包，常见缺失：
- `\usepackage{amsmath}` - 数学公式
- `\usepackage{graphicx}` - 图片
- `\usepackage{hyperref}` - 超链接

### 问题7：PDF 中文字体缺失

**原因**：系统没有中文字体

**解决**：
```latex
\usepackage[UTF8,fontset=windows]{ctex}  % Windows 系统
\usepackage[UTF8,fontset=mac]{ctex}      % Mac 系统
```

---

## 代码规范

### 1. 缩进

- 环境内缩进 2 空格
- 嵌套环境继续缩进

```latex
\begin{itemize}
  \item 第一点
    \begin{itemize}
      \item 子项1
      \item 子项2
    \end{itemize}
  \item 第二点
\end{itemize}
```

### 2. 空行

- 环境前后各空一行
- 段落之间空一行
- 不要连续多个空行

### 3. 注释

```latex
% 这是注释
% 用于解释复杂公式或特殊处理
```

### 4. 命名规范

- 标签用英文小写+连字符：`\label{eq:fourier-transform}`
- 前缀标识类型：`eq:`, `fig:`, `tab:`, `sec:`

---

## 图表规范

### 1. 函数图像

```latex
\begin{tikzpicture}
\begin{axis}[
    xlabel={$\omega$},
    ylabel={$|X(\omega)|$},
    grid=major,
    width=10cm,
    height=6cm
]
\addplot[blue,thick] {exp(-x^2)};
\end{axis}
\end{tikzpicture}
```

### 2. 框图

```latex
\begin{tikzpicture}[
    block/.style={rectangle, draw, fill=blue!20, 
        text width=5em, text centered, minimum height=3em}
]
\node[block] (input) {输入};
\node[block, right=2cm of input] (system) {系统};
\node[block, right=2cm of system] (output) {输出};

\draw[->] (input) -- (system);
\draw[->] (system) -- (output);
\end{tikzpicture}
```

### 3. 信号波形

```latex
\begin{tikzpicture}
\begin{axis}[
    xlabel={t},
    ylabel={x(t)},
    domain=-2*pi:2*pi,
    samples=100,
    grid=major
]
\addplot[blue,thick] {sin(deg(x))};
\addplot[red,dashed] {0};
\end{axis}
\end{tikzpicture}
```

---

## 编译检查清单

编译前检查：

- [ ] 所有 `\begin{...}` 都有对应的 `\end{...}`
- [ ] 所有 `$` 都成对出现
- [ ] 所有 `{` 都有对应的 `}`
- [ ] 特殊字符已转义：`&`, `%`, `$`, `#`, `_`, `{`, `}`, `~`, `^`
- [ ] 中文字符在正确环境中
- [ ] 图片路径正确
- [ ] 引用的标签都存在

编译后检查：

- [ ] PDF 生成成功
- [ ] 中文正常显示
- [ ] 公式编号正确
- [ ] 图表位置合理
- [ ] 页面布局美观
- [ ] 没有溢出警告

---

## 性能优化

### 1. 编译速度

- 使用 `\includeonly{}` 只编译需要的章节
- 图片用 `\includegraphics` 而非内嵌 tikz（复杂图）

### 2. 文件大小

- 图片压缩后再引入
- 避免重复的宏包引入
- 使用 `\pdfcompresslevel=9` 压缩 PDF

### 3. 兼容性

- 使用标准宏包，避免冷门宏包
- 测试不同 LaTeX 发行版（TeXLive, MiKTeX）
- 保留 `.tex` 源文件，便于后续修改
