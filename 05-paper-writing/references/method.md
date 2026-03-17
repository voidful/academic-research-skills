# Method 方法撰寫指南

## 核心原則

Method section 是論文的技術核心。它必須讓讀者（1）理解你的方法的高層邏輯，（2）掌握每個組件的技術細節，（3）明白每個設計選擇背後的理由。遵循三要素結構：Overview → Details → Justification。

---

## 三要素結構

### 要素 1：Overview（方法概覽）

Method 的第一段（或第一個 subsection）必須提供方法的高層概覽，讓讀者在深入細節前先掌握全貌。

**必須包含**：
- 方法的整體流程
- 輸入和輸出是什麼
- 主要組件有哪些
- 各組件之間的關係

**範例**：
```latex
\section{Method}
\label{sec:method}

Given a set of $K$ input images $\{I_k\}_{k=1}^{K}$ with
known camera poses $\{P_k\}_{k=1}^{K}$, our goal is to
reconstruct a neural scene representation that enables
high-quality novel view synthesis.

\cref{fig:overview} illustrates our framework, which consists
of three stages: (1)~a \textit{geometry estimation} module
that constructs a coarse depth proxy from the input views
(Sec.~\ref{sec:geometry}), (2)~a \textit{feature extraction}
module that computes geometry-aware local features
(Sec.~\ref{sec:features}), and (3)~a \textit{neural rendering}
module that synthesizes novel views conditioned on the
estimated geometry and features (Sec.~\ref{sec:rendering}).
```

**注意事項**：
- 必須引用 overview figure（通常是 Figure 2 或 Figure 1）
- 用括號標註每個組件對應的 subsection
- 使用 `\cref{}` 或 `Sec.~\ref{}` 做交叉引用

### 要素 2：Details（技術細節）

每個組件用一個 subsection 詳細描述。每個 subsection 遵循以下結構：

```
1. 動機（為什麼需要這個組件？）     ← Motivation-First
2. 形式化定義（輸入、輸出、操作）    ← 數學嚴謹
3. 具體實現（網路架構、損失函數等）   ← 可重現
4. 與其他選擇的比較（為什麼選這個？） ← Justification
```

**範例**：
```latex
\subsection{Geometry Estimation}
\label{sec:geometry}

% 1. 動機
Directly optimizing a neural radiance field from sparse
views is ill-posed, as large portions of the scene lack
multi-view supervision. To provide geometric guidance for
unobserved regions, we first estimate a coarse depth map
for each input view.

% 2. 形式化定義
Specifically, for each pair of input views $(I_i, I_j)$,
we construct a cost volume $\mathbf{C}_{ij} \in
\mathbb{R}^{H \times W \times D}$ by computing feature
correlations at $D$ depth hypotheses uniformly sampled
in inverse depth space:
\begin{equation}
  \mathbf{C}_{ij}(u, v, d) = \langle
    \mathbf{F}_i(u, v),\;
    \mathbf{F}_j(\pi(P_j P_i^{-1}, u, v, d))
  \rangle,
  \label{eq:cost_volume}
\end{equation}
where $\mathbf{F}_i$ denotes the feature map of view $i$,
$\pi(\cdot)$ is the projection function, and $\langle
\cdot, \cdot \rangle$ is the inner product.

% 3. 具體實現
The cost volume is regularized by a 3D U-Net with group
normalization, producing a probability volume from which
we extract the depth via soft argmin~\cite{gcnet}.
We aggregate depth estimates from all view pairs using
a confidence-weighted average.

% 4. 與其他選擇的比較
We opt for a cost-volume-based approach over monocular
depth estimation~\cite{midas} because it explicitly
leverages multi-view geometry, providing more reliable
estimates in overlapping regions
(see ablation in \cref{tab:ablation}).
```

### 要素 3：Justification（合理性論證）

每一個非平凡的設計選擇都需要 justification。有三種 justification 方式：

| 方式 | 適用場景 | 範例 |
|------|---------|------|
| 理論 | 有數學推導支持 | "By Theorem 1, this loss is equivalent to..." |
| 實證 | 有 ablation 支持 | "As shown in Table 3, this design improves by 1.2 dB" |
| 直覺 | 合理的設計直覺 | "Since depth discontinuities often align with semantic boundaries, we..." |

**最強的 justification** 結合理論與實證：先用直覺解釋為什麼這樣設計，再用 ablation 驗證。

---

## 如何用圖說明 Pipeline

### Overview Figure 設計原則

Overview figure（通常是 Figure 2）是 Method section 最重要的圖：

1. **從左到右或從上到下的資訊流**：輸入在左/上，輸出在右/下
2. **模組化呈現**：每個組件用一個方框表示，方框內用簡短標籤
3. **標註對應的 subsection**：讓讀者知道去哪裡看細節
4. **使用一致的顏色系統**：
   - 輸入/輸出用一種顏色
   - 可訓練模組用另一種顏色
   - 損失函數用第三種顏色
5. **避免過度複雜**：如果超過 7 個方框，考慮分層呈現

### Caption 寫作

```latex
\caption{Overview of our proposed framework. Given $K$
  sparse input views (left), we first estimate coarse
  geometry through a cost volume (Sec.~\ref{sec:geometry}),
  then extract geometry-aware features
  (Sec.~\ref{sec:features}), and finally render novel
  views through a conditioned neural radiance field
  (Sec.~\ref{sec:rendering}). Trainable components are
  shown in \textcolor{blue}{blue}; frozen modules in gray.}
```

### 補充圖

除了 overview figure，Method section 可能需要：
- **細節圖**：展示某個關鍵組件的內部結構
- **示意圖**：用視覺方式解釋某個抽象概念
- **比較圖**：展示你的方法與 baseline 的結構差異

---

## 符號一致性要求

### 首次出現規則

每個數學符號在首次出現時必須定義：

```latex
% ✅ 首次出現時定義
Given a set of $K$ input images $\{I_k\}_{k=1}^{K}$...

% ❌ 使用未定義的符號
We compute $\mathbf{C}_{ij}(u,v,d)$...
% （讀者不知道 C, u, v, d 分別是什麼）
```

### 符號表（Notation Table）

對於符號眾多的論文，建議在 Method 開頭或附錄中放一個符號表：

```latex
\begin{table}[t]
  \centering
  \caption{Notation summary.}
  \label{tab:notation}
  \begin{tabular}{cl}
    \toprule
    Symbol & Description \\
    \midrule
    $K$ & Number of input views \\
    $I_k$ & The $k$-th input image \\
    $P_k$ & Camera pose of the $k$-th view \\
    $\mathbf{F}_k$ & Feature map of the $k$-th view \\
    $\mathbf{C}_{ij}$ & Cost volume between views $i$ and $j$ \\
    $\hat{D}_k$ & Estimated depth map for view $k$ \\
    \bottomrule
  \end{tabular}
\end{table}
```

### 常見符號不一致問題

| 問題 | 範例 | 修正 |
|------|------|------|
| 同一概念用不同符號 | 有時用 $x$，有時用 $\mathbf{x}$ | 統一為一種 |
| 不同概念用相同符號 | 損失函數和長度都用 $L$ | 損失用 $\mathcal{L}$，長度用 $L$ |
| 上下標不一致 | 有時 $x_i$，有時 $x^{(i)}$ | 統一風格 |
| 缺少定義 | 突然出現 $\lambda$ | 加上 "where $\lambda$ is the balancing weight" |

---

## 損失函數撰寫

損失函數是 Method 的重要部分，需要特別注意寫法：

### 結構

```latex
\subsection{Training Objective}
\label{sec:loss}

% 1. 總損失
Our total training objective combines three terms:
\begin{equation}
  \mathcal{L} = \mathcal{L}_{\text{rgb}}
    + \lambda_d \mathcal{L}_{\text{depth}}
    + \lambda_r \mathcal{L}_{\text{reg}},
  \label{eq:total_loss}
\end{equation}
where $\lambda_d$ and $\lambda_r$ are balancing weights.

% 2. 逐項定義
\paragraph{Reconstruction Loss.}
$\mathcal{L}_{\text{rgb}}$ measures the photometric
error between rendered and ground-truth pixels:
\begin{equation}
  \mathcal{L}_{\text{rgb}} = \frac{1}{|\mathcal{R}|}
    \sum_{\mathbf{r} \in \mathcal{R}}
    \| \hat{C}(\mathbf{r}) - C(\mathbf{r}) \|_2^2,
  \label{eq:rgb_loss}
\end{equation}
where $\mathcal{R}$ is the set of sampled rays...

% 3. 解釋為什麼用這個損失
We use L2 rather than L1 loss as it provides smoother
gradients during early training when the geometry
estimate is coarse.
```

### 注意事項

- 每個損失項都要單獨定義
- 每個超參數（$\lambda$）都要說明如何設定
- 解釋為什麼選擇這個損失函數（而非其他選擇）

---

## 演算法虛擬碼

對於流程複雜的方法，演算法虛擬碼可以幫助讀者理解：

**何時需要**：
- 方法有明確的多步驟流程
- 文字描述容易混淆
- 訓練和推理流程不同

**何時不需要**：
- 方法流程很直覺（一個 forward pass）
- Overview figure 已經足夠清晰

---

## 常見錯誤

### 錯誤 1：缺少 Overview

直接跳入技術細節，讀者迷失在符號和公式中。

**解法**：Method 第一段必須是不帶公式的高層概覽。

### 錯誤 2：缺少 Motivation

```latex
% ❌ 沒有動機
We add a skip connection between layers 3 and 7.

% ✅ 有動機
To preserve fine-grained spatial details that are
often lost through successive downsampling, we
introduce a skip connection between layers 3 and 7.
```

### 錯誤 3：細節不足以重現

```latex
% ❌ 太含糊
We use a CNN to extract features.

% ✅ 可重現
We use a ResNet-50~\cite{resnet} pretrained on ImageNet
as the feature extractor. We extract features from the
output of \texttt{layer3}, yielding feature maps of
dimension $\mathbb{R}^{H/8 \times W/8 \times 1024}$.
```

### 錯誤 4：符號混亂

同一個符號在不同地方表示不同的東西，或者同一概念用了不同符號。

**解法**：全文寫完後，做一次符號一致性檢查。

---

## 自我檢查清單

```
□ 是否有清晰的 Overview（不帶公式）？
□ Overview 是否引用了 figure？
□ 每個組件是否有獨立的 subsection？
□ 每個設計選擇是否有 motivation？
□ 所有符號是否在首次出現時定義？
□ 符號是否全文一致？
□ 損失函數是否逐項定義？
□ 超參數是否說明設定方式？
□ 細節是否足夠讓人重現？
□ 是否需要演算法虛擬碼？
```

---

*回到主文件 → `../SKILL.md`*
