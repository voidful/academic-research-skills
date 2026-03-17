# Experiments 實驗撰寫指南

## 核心原則

Experiments section 的目標是**用數據說服 reviewer 你的方法有效**。每一個 Introduction 中的 claim 都必須在這裡找到對應的實驗支持。遵循四段式結構：Setup → Main Results → Ablation Study → Analysis。

---

## 四段式結構

### 第 1 段：Experimental Setup

#### 必須包含的資訊

```latex
\subsection{Experimental Setup}
\label{sec:setup}

\paragraph{Datasets.}
% 列出所有使用的資料集，每個都要說明：
% - 資料集名稱與引用
% - 規模（圖片數、場景數等）
% - 訓練/驗證/測試分割方式
% - 為什麼選這個資料集
We evaluate on three standard benchmarks:
(1)~\textbf{DTU}~\cite{dtu} (124 scenes, ...),
(2)~\textbf{BlendedMVS}~\cite{blendedmvs} (113 scenes, ...),
and (3)~\textbf{Tanks\&Temples}~\cite{tnt} (21 scenes, ...).
We follow the standard training/test split of [ref].

\paragraph{Baselines.}
% 列出所有比較的 baseline
% - 每個 baseline 的引用
% - 簡述方法類型
% - 結果來源（原論文 or 自己跑的）
We compare against X recent methods spanning two families:
regression-based approaches (PixelNeRF~\cite{pixelnerf},
MVSNeRF~\cite{mvsnerf}, ...) and generative approaches
(SparseFusion~\cite{sparsefusion}, ...).
All baseline results are reproduced using official code
with default hyperparameters, except [X] where we report
numbers from the original paper.

\paragraph{Metrics.}
% 列出所有使用的指標
% - 指標的全名與縮寫
% - 每個指標衡量什麼
We report PSNR, SSIM~\cite{ssim}, and
LPIPS~\cite{lpips} for image quality evaluation.
Higher is better for PSNR and SSIM; lower is better
for LPIPS.

\paragraph{Implementation Details.}
% 可重現性的關鍵
% - 框架（PyTorch版本）
% - 優化器、學習率、排程
% - 訓練 epoch 數
% - batch size
% - 硬體環境
% - 訓練時間
Our method is implemented in PyTorch 2.0. We train for
100K iterations using Adam~\cite{adam} with a learning
rate of $5 \times 10^{-4}$, decayed by 0.5 every 25K
iterations. Training takes approximately 8 hours on a
single NVIDIA A100 GPU. Detailed hyperparameters are
provided in the supplementary material.
```

#### 常見遺漏

| 遺漏項目 | Reviewer 反應 |
|---------|-------------|
| 資料集分割方式 | "How was the data split?" |
| Baseline 結果來源 | "Were baselines re-run or taken from papers?" |
| 訓練超參數 | "Cannot reproduce" |
| 硬體資訊 | "What is the computational cost?" |
| 隨機種子 | "How many runs? What is the variance?" |

### 第 2 段：Main Results

#### 表格設計原則

主結果表格是 Experiments 的核心。設計原則如下：

**格式規範**：
- 使用 `booktabs` 套件（`\toprule`, `\midrule`, `\bottomrule`）
- **最佳結果加粗**（`\textbf{}`）
- **次佳結果加底線**（`\underline{}`）
- 在 caption 中說明加粗和底線的含義
- 方法名稱按年份排列或按類別分組
- 你的方法放在表格最後一行
- 用 `\midrule` 將你的方法與 baseline 分隔

```latex
\begin{table}[t]
  \centering
  \caption{Quantitative comparison on DTU~\cite{dtu} with
    3 input views. \textbf{Bold}: best result.
    \underline{Underline}: second best.
    $\dagger$: results from original papers.}
  \label{tab:main_dtu}
  \begin{tabular}{lccc}
    \toprule
    Method & PSNR$\uparrow$ & SSIM$\uparrow$ & LPIPS$\downarrow$ \\
    \midrule
    PixelNeRF~\cite{pixelnerf} & 19.31 & 0.789 & 0.382 \\
    MVSNeRF~\cite{mvsnerf} & 21.18 & 0.843 & 0.264 \\
    SparseNeRF~\cite{sparsenerf}$^\dagger$ & 22.45 & 0.871 & 0.218 \\
    RegNeRF~\cite{regnerf} & \underline{23.12} & \underline{0.889} & \underline{0.195} \\
    \midrule
    Ours & \textbf{25.41} & \textbf{0.912} & \textbf{0.163} \\
    \bottomrule
  \end{tabular}
\end{table}
```

**箭頭標註**：在指標名稱旁加上 $\uparrow$（越高越好）或 $\downarrow$（越低越好），幫助讀者快速判讀。

#### 文字描述

表格本身只呈現數字，文字需要幫助讀者**解讀**這些數字：

```latex
% ✅ 好的結果描述
\cref{tab:main_dtu} presents the quantitative comparison
on DTU. Our method achieves 25.41 dB PSNR, outperforming
the previous best (RegNeRF, 23.12 dB) by 2.29 dB.
Notably, this improvement is most pronounced in scenes
with large occluded regions (see per-scene breakdown
in supplementary), confirming the effectiveness of our
geometric guidance.

% ❌ 壞的結果描述（只重複表格數字）
As shown in Table 1, our PSNR is 25.41, SSIM is 0.912,
and LPIPS is 0.163. PixelNeRF achieves 19.31, MVSNeRF
achieves 21.18, SparseNeRF achieves 22.45, RegNeRF
achieves 23.12.
```

**要點**：
- 不要逐行重複表格數字
- 聚焦於**趨勢**和**洞察**
- 解釋為什麼你的方法更好（與 Method 的 claim 對應）
- 指出在哪些情境下優勢最明顯

#### 多資料集呈現

如果在多個資料集上實驗：
- 每個資料集一張表格，或合併成一張大表
- 文字描述聚焦於跨資料集的一致趨勢
- 如果某個資料集表現不如預期，誠實說明原因

### 第 3 段：Ablation Study

Ablation study 是 reviewer 最看重的實驗之一。它證明你的方法中**每個組件都是必要的**。

#### 設計原則

```
完整方法（Full model）
  - 去掉組件 A → 驗證 A 的必要性
  - 去掉組件 B → 驗證 B 的必要性
  - 去掉組件 C → 驗證 C 的必要性
  - 替換組件 A 為替代方案 A' → 驗證 A 的設計選擇
  - 改變超參數 → 驗證超參數敏感度
```

#### 表格範例

```latex
\begin{table}[t]
  \centering
  \caption{Ablation study on DTU with 3 input views.
    Each row removes or replaces one component from
    the full model.}
  \label{tab:ablation}
  \begin{tabular}{lccc}
    \toprule
    Configuration & PSNR & SSIM & LPIPS \\
    \midrule
    Full model & \textbf{25.41} & \textbf{0.912} & \textbf{0.163} \\
    \midrule
    w/o geometry proxy & 23.05 & 0.878 & 0.214 \\
    w/o feature conditioning & 24.18 & 0.895 & 0.188 \\
    w/o depth supervision & 24.72 & 0.903 & 0.175 \\
    Replace cost volume $\to$ monocular depth & 24.33 & 0.891 & 0.192 \\
    \bottomrule
  \end{tabular}
\end{table}
```

#### 文字描述

```latex
\cref{tab:ablation} presents the ablation study. Removing
the geometry proxy causes the largest performance drop
($-$2.36 dB), confirming that explicit geometric guidance
is the key ingredient of our framework. Feature conditioning
contributes 1.23 dB, demonstrating the importance of
geometry-aware features. Replacing our cost-volume-based
geometry estimation with monocular depth reduces PSNR by
1.08 dB, validating our choice of leveraging multi-view
geometry.
```

### 第 4 段：Analysis

超越數字的深入分析，展示你對方法的理解：

#### 常見分析類型

| 分析類型 | 內容 | 呈現方式 |
|---------|------|---------|
| 定性比較 | 視覺結果對比 | Figure（並排對比圖） |
| 失敗案例 | 方法失效的場景 | Figure + 分析文字 |
| 效率分析 | 推理時間、參數量、FLOPs | Table |
| Scaling 分析 | 隨視角數/資料量/模型大小的變化 | Line chart |
| 泛化性分析 | 在新資料集/新場景上的表現 | Table / Figure |
| 超參數敏感度 | 關鍵超參數的影響 | Line chart / Table |

#### 定性比較範例

```latex
\paragraph{Qualitative Comparison.}
\cref{fig:qualitative} presents visual comparisons on
challenging scenes from DTU. Our method produces sharper
textures and more coherent geometry in occluded regions
(highlighted in red boxes), whereas PixelNeRF generates
blurry results and RegNeRF exhibits floating artifacts.
```

#### 失敗案例分析

```latex
\paragraph{Failure Cases.}
\cref{fig:failure} shows representative failure cases.
Our method struggles with (1)~highly specular surfaces
where the Lambertian assumption of our cost volume
breaks down, and (2)~extremely thin structures that
fall between depth sampling planes. Addressing these
limitations is an important direction for future work.
```

---

## 超參數描述

### 在正文中

只提及最關鍵的超參數（影響方法設計的）：

```latex
We set the number of depth hypotheses to $D = 128$,
uniformly sampled in inverse depth space between the
near and far planes. The loss weights are set to
$\lambda_d = 0.1$ and $\lambda_r = 0.01$ based on
validation performance.
```

### 在附錄/補充材料中

提供完整的超參數表格：

```latex
\begin{table}[h]
  \centering
  \caption{Complete hyperparameter settings.}
  \begin{tabular}{lc}
    \toprule
    Hyperparameter & Value \\
    \midrule
    Learning rate & $5 \times 10^{-4}$ \\
    Batch size & 4 \\
    Optimizer & Adam ($\beta_1 = 0.9$, $\beta_2 = 0.999$) \\
    LR schedule & Step decay ($\times 0.5$ every 25K) \\
    Total iterations & 100K \\
    Depth hypotheses $D$ & 128 \\
    $\lambda_d$ & 0.1 \\
    $\lambda_r$ & 0.01 \\
    \bottomrule
  \end{tabular}
\end{table}
```

---

## 公平比較原則

Reviewer 非常在意比較的公平性：

1. **相同資料分割**：所有方法使用完全相同的訓練/測試集
2. **相同輸入**：相同的輸入圖片、相同的視角
3. **相同評估方式**：相同的指標計算方式（resolution、cropping 等）
4. **最佳設定**：baseline 使用其論文中推薦的最佳設定
5. **版本說明**：如果使用官方程式碼，說明版本；如果自己實現，說明依據

```latex
% 公平性聲明
For fair comparison, all methods are evaluated at
$800 \times 600$ resolution. We use the official
implementations of all baselines with their recommended
hyperparameters. For methods that do not provide pretrained
models on our evaluation datasets, we retrain them
following the original training protocols.
```

---

## 統計顯著性

對於結果差異較小的比較，建議報告統計顯著性：

```latex
We run each experiment 3 times with different random
seeds and report the mean and standard deviation.
Our method achieves $25.41 \pm 0.12$ dB PSNR,
compared to $23.12 \pm 0.08$ dB for RegNeRF.
The improvement is statistically significant
($p < 0.01$, paired $t$-test).
```

---

## 自我檢查清單

```
□ Experimental Setup 是否包含資料集、baseline、指標、實現細節？
□ 是否所有 Introduction 中的 claim 都有對應實驗？
□ 主結果表格是否加粗最佳、底線次佳？
□ 文字是否解讀趨勢（而非重複數字）？
□ Ablation study 是否驗證每個組件的必要性？
□ 是否有定性比較（視覺結果）？
□ 是否有失敗案例分析？
□ 是否有效率比較？
□ 比較是否公平（相同設定）？
□ 超參數是否有完整記錄？
□ 是否報告多次實驗的方差？
```

---

*回到主文件 → `../SKILL.md`*
