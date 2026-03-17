# LaTeX 最佳實踐

## 文件結構範本

```latex
\documentclass{article}
% === Package imports ===
\usepackage{booktabs}       % Professional tables
\usepackage{amsmath,amssymb} % Math
\usepackage{graphicx}       % Figures
\usepackage{hyperref}       % Clickable references
\usepackage{cleveref}       % Smart cross-references
\usepackage{algorithm2e}    % Algorithms
\usepackage{subcaption}     % Sub-figures

% === Custom commands (define once, use everywhere) ===
\newcommand{\method}{OurMethod}  % Method name
\newcommand{\eg}{\textit{e.g.}}
\newcommand{\ie}{\textit{i.e.}}
\newcommand{\etal}{\textit{et al.}}

\begin{document}
\title{[Title]}
\author{Anonymous}
\maketitle
\begin{abstract}
  [4 sentences: problem, method, result, impact]
\end{abstract}
\input{sections/introduction}
\input{sections/related_work}
\input{sections/method}
\input{sections/experiments}
\input{sections/conclusion}
\bibliography{references}
\bibliographystyle{plain}
\appendix
\input{sections/appendix}
\end{document}
```

## 表格範本

```latex
\begin{table}[t]
  \centering
  \caption{Comparison with state-of-the-art methods on
    Dataset-X. \textbf{Bold}: best. \underline{Underline}: second best.}
  \label{tab:main_results}
  \begin{tabular}{lccc}
    \toprule
    Method & Metric-1 & Metric-2 & Metric-3 \\
    \midrule
    Baseline-A~\cite{ref1} & 72.1 & 68.3 & 45.2 \\
    Baseline-B~\cite{ref2} & 74.5 & 70.1 & 47.8 \\
    Baseline-C~\cite{ref3} & \underline{76.2} & \underline{71.5} & \underline{49.3} \\
    \midrule
    Ours & \textbf{78.3} & \textbf{73.8} & \textbf{52.1} \\
    \bottomrule
  \end{tabular}
\end{table}
```

## 圖片範本

```latex
\begin{figure}[t]
  \centering
  \includegraphics[width=\linewidth]{figures/method_overview.pdf}
  \caption{Overview of our proposed method. Given an input $\mathbf{x}$,
    we first extract features using module A (Sec.~\ref{sec:module_a}),
    then refine them through module B (Sec.~\ref{sec:module_b}).
    The final output $\hat{\mathbf{y}}$ is produced by the decoder.}
  \label{fig:overview}
\end{figure}
```

## 演算法範本

```latex
\begin{algorithm}[t]
  \caption{Training procedure of \method{}}
  \label{alg:training}
  \KwIn{Training data $\mathcal{D}$, learning rate $\eta$}
  \KwOut{Trained model parameters $\theta^*$}
  Initialize $\theta$ randomly\;
  \For{epoch $= 1$ \KwTo $E$}{
    \For{mini-batch $(\mathbf{x}, \mathbf{y}) \sim \mathcal{D}$}{
      Compute loss $\mathcal{L}(\theta; \mathbf{x}, \mathbf{y})$\;
      Update $\theta \leftarrow \theta - \eta \nabla_\theta \mathcal{L}$\;
    }
  }
  \Return{$\theta^*$}\;
\end{algorithm}
```

## LaTeX 生成規則

1. 使用 `\section{}`, `\subsection{}` 等標準指令。
2. 數學公式使用 `equation` 或 `align` 環境，每個公式加 `\label{}`。
3. 引用使用 `\cite{}`，交叉引用使用 `\ref{}` 或 `\cref{}`。
4. 表格使用 `booktabs`（`\toprule`, `\midrule`, `\bottomrule`）。
5. 最佳結果加粗：`\textbf{}`，次佳底線：`\underline{}`。
6. 符號在首次出現時使用 inline math 定義。
