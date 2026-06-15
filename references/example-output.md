# 课件总结示例

> 本文件展示一个完整的课件总结输出示例，供参考和对照。

## 示例场景

- **源文件**：信号与系统第3章 - 傅里叶变换.pdf（共 45 页）
- **输出格式**：LaTeX + PDF
- **语言风格**：中文为主，术语附英文

---

## 期望输出结构

```latex
\documentclass[11pt,a4paper]{article}
\usepackage[UTF8]{ctex}
\usepackage{amsmath,amssymb}
\usepackage{geometry}
\usepackage{enumitem}
\usepackage{tikz}
\usepackage{pgfplots}

\geometry{margin=2.5cm}
\setlength{\parindent}{0pt}
\setlength{\parskip}{6pt}

\title{信号与系统 · 第3章 傅里叶变换}
\author{课件总结}
\date{2026-06-15}

\begin{document}
\maketitle

\section{核心概念}

\subsection{傅里叶级数 (Fourier Series)}

\textbf{定义}：周期信号分解为正弦/余弦分量的叠加

\textbf{公式}：
\begin{equation}
x(t) = \frac{a_0}{2} + \sum_{n=1}^{\infty} [a_n \cos(n\omega_0 t) + b_n \sin(n\omega_0 t)]
\end{equation}

\textbf{系数计算}：
\begin{align}
a_n &= \frac{2}{T} \int_{T} x(t) \cos(n\omega_0 t) dt \\
b_n &= \frac{2}{T} \int_{T} x(t) \sin(n\omega_0 t) dt
\end{align}

\textbf{物理意义}：任意周期信号可以用不同频率的正弦波叠加表示

\textbf{典型例题}：求方波信号的傅里叶级数展开

\textbf{易错点}：
\begin{itemize}
  \item 积分区间选择：通常取 $[-T/2, T/2]$ 或 $[0, T]$
  \item 奇偶函数简化：奇函数 $a_n=0$，偶函数 $b_n=0$
\end{itemize}

\subsection{傅里叶变换 (Fourier Transform)}

\textbf{定义}：非周期信号的频域表示

\textbf{公式}：
\begin{equation}
X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} dt
\end{equation}

\textbf{逆变换}：
\begin{equation}
x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(\omega) e^{j\omega t} d\omega
\end{equation}

\textbf{物理意义}：信号在频域的密度分布

\section{重要性质}

\begin{enumerate}
  \item \textbf{线性性}：$\mathcal{F}[ax_1(t) + bx_2(t)] = aX_1(\omega) + bX_2(\omega)$
  \item \textbf{时移性}：$\mathcal{F}[x(t-t_0)] = e^{-j\omega t_0} X(\omega)$
  \item \textbf{频移性}：$\mathcal{F}[e^{j\omega_0 t} x(t)] = X(\omega - \omega_0)$
  \item \textbf{尺度变换}：$\mathcal{F}[x(at)] = \frac{1}{|a|} X(\frac{\omega}{a})$
  \item \textbf{卷积定理}：$\mathcal{F}[x_1(t) * x_2(t)] = X_1(\omega) \cdot X_2(\omega)$
\end{enumerate}

\section{常用变换对}

\begin{center}
\begin{tabular}{|l|l|}
\hline
\textbf{时域信号} & \textbf{频域表示} \\
\hline
$\delta(t)$ & $1$ \\
\hline
$1$ & $2\pi\delta(\omega)$ \\
\hline
$e^{j\omega_0 t}$ & $2\pi\delta(\omega - \omega_0)$ \\
\hline
$\cos(\omega_0 t)$ & $\pi[\delta(\omega - \omega_0) + \delta(\omega + \omega_0)]$ \\
\hline
$e^{-at}u(t)$, $a>0$ & $\frac{1}{a + j\omega}$ \\
\hline
$u(t)$ & $\pi\delta(\omega) + \frac{1}{j\omega}$ \\
\hline
\end{tabular}
\end{center}

\section{典型例题}

\subsection{例题1：求矩形脉冲的傅里叶变换}

\textbf{题目}：求 $x(t) = \text{rect}(t/\tau)$ 的傅里叶变换

\textbf{解法}：
\begin{align}
X(\omega) &= \int_{-\tau/2}^{\tau/2} e^{-j\omega t} dt \\
&= \frac{e^{-j\omega t}}{-j\omega} \Big|_{-\tau/2}^{\tau/2} \\
&= \frac{2\sin(\omega\tau/2)}{\omega} \\
&= \tau \cdot \text{Sa}(\omega\tau/2)
\end{align}

\textbf{技巧}：利用 Sa 函数（抽样函数）简化表达式

\subsection{例题2：利用卷积定理求响应}

\textbf{题目}：已知系统冲激响应 $h(t) = e^{-t}u(t)$，求输入 $x(t) = u(t)$ 的响应

\textbf{解法}：
\begin{enumerate}
  \item 求变换：$H(\omega) = \frac{1}{1+j\omega}$，$X(\omega) = \pi\delta(\omega) + \frac{1}{j\omega}$
  \item 频域相乘：$Y(\omega) = H(\omega) \cdot X(\omega)$
  \item 求逆变换得 $y(t)$
\end{enumerate}

\section{易错点汇总}

\begin{itemize}
  \item 傅里叶变换存在条件：$\int_{-\infty}^{\infty} |x(t)| dt < \infty$
  \item 不要混淆 $\omega$（角频率）和 $f$（频率）：$\omega = 2\pi f$
  \item 卷积定理应用时注意归一化系数
  \item 离散傅里叶变换（DFT）与连续傅里叶变换的区别
\end{itemize}

\section{考试重点}

\begin{enumerate}
  \item 傅里叶级数系数的计算（必考）
  \item 常用信号的傅里叶变换（必须熟记）
  \item 卷积定理的应用（高频考点）
  \item 信号的带宽概念和计算
\end{enumerate}

\end{document}
```

---

## 输出质量检查清单

- [ ] 包含核心概念定义
- [ ] 公式完整且正确
- [ ] 有物理意义解释
- [ ] 有典型例题
- [ ] 有易错点标注
- [ ] 有考试重点提示
- [ ] 术语中英对照
- [ ] 页码引用准确
- [ ] LaTeX 语法正确
- [ ] 排版清晰可读

---

## 常见问题

### Q: 公式太长怎么办？
A: 使用 `align` 环境分行，每行不超过 80 字符

### Q: 图表怎么处理？
A: 用 tikz/pgfplots 绘制，不要用截图

### Q: 内容太多怎么精简？
A: 只保留核心公式和典型例题，细节删除

### Q: 不确定的内容怎么标注？
A: 标注「原文未明确」或「待确认」
