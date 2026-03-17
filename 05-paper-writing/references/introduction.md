# Introduction 引言寫作指南

## 核心原則

Introduction 是論文中最難寫的部分。它決定了 reviewer 是否認為你的工作值得被接收。一個好的 Introduction 必須在 1-1.5 頁內完成一個完整的邏輯論證：這個問題重要→現有方法不夠好→我們有更好的解法→我們的貢獻如下。

---

## 漏斗結構（Funnel Structure）

Introduction 的邏輯必須遵循由寬到窄的漏斗結構：

```
┌─────────────────────────────────────────┐
│         大背景（寬）                       │
│    這個研究領域為什麼重要？                   │
├─────────────────────────────────────────┤
│       具體問題（中）                        │
│    在這個領域中，什麼問題尚未解決？             │
├─────────────────────────────────────────┤
│     現有方法的不足（窄）                     │
│    現有方法為什麼不夠好？                     │
├─────────────────────────────────────────┤
│      我們的方法（核心）                      │
│    我們怎麼解決這個問題？                     │
├─────────────────────────────────────────┤
│       貢獻列表                            │
│    具體列出 3-4 個貢獻                      │
└─────────────────────────────────────────┘
```

### 第 1 段：大背景

- **目標**：建立共識——這個研究領域為什麼重要
- **長度**：3-5 句
- **技巧**：
  - 從應用或現實需求切入
  - 不要太寬泛（"Deep learning has achieved great success..."）
  - 也不要太窄（直接跳到你的具體問題）
  - 引用 2-3 篇高影響力的論文建立可信度

**範例**：
```latex
Understanding and generating 3D scenes from images is a
cornerstone of computer vision, with direct applications
in autonomous driving~\cite{ref1}, robotic
manipulation~\cite{ref2}, and augmented
reality~\cite{ref3}. Recent advances in neural scene
representations~\cite{nerf,instant_ngp} have demonstrated
remarkable quality in novel view synthesis, sparking
widespread interest in learning-based 3D reconstruction.
```

### 第 2 段：具體問題

- **目標**：從大背景聚焦到你要解決的具體問題
- **長度**：3-5 句
- **技巧**：
  - 明確定義問題的邊界
  - 說明這個問題為什麼特別困難
  - 用一句話概括問題的核心挑戰

**範例**：
```latex
Despite this progress, most existing methods require dense
multi-view inputs (typically 50--100 images) to achieve
high-quality reconstruction. In many practical scenarios,
however, only a sparse set of views (e.g., 3--5 images)
is available. Reconstructing from such sparse inputs is
fundamentally ill-posed, as large portions of the scene
remain unobserved.
```

### 第 3 段：現有方法的不足

- **目標**：指出現有方法的具體缺陷，為你的方法建立必要性
- **長度**：4-6 句
- **技巧**：
  - 分類介紹現有方法的主要流派
  - 每個流派指出一個核心缺陷
  - 缺陷必須是客觀的、可驗證的
  - **不要攻擊先前工作**，而是客觀分析其限制

**範例**：
```latex
Prior approaches to sparse-view reconstruction fall into
two categories. Regression-based methods~\cite{pixelnerf,mvsnerf}
directly predict radiance fields from input views but
struggle with unseen regions, producing blurry artifacts.
Generative approaches~\cite{sparsefusion,zero123} leverage
diffusion priors to hallucinate novel views, yet often
generate geometrically inconsistent content. Both families
lack an explicit mechanism to reason about scene geometry
at a global level, limiting their ability to produce
coherent reconstructions.
```

### 第 4 段：我們的方法

- **目標**：介紹你的核心 idea 和方法概覽
- **長度**：4-6 句
- **技巧**：
  - **Motivation-First**：先說為什麼這樣做，再說怎麼做
  - 用一句話概括核心 insight
  - 然後簡要描述方法的主要組件
  - 避免技術細節（留給 Method section）
  - 可以在這裡預覽關鍵結果

**範例**：
```latex
Our key observation is that even a coarse geometric
estimate---such as a rough depth map or voxel grid---provides
sufficient structural guidance to regularize the
reconstruction in unobserved regions. Building on this
insight, we present SparseRecon, a coarse-to-fine framework
that first constructs an approximate geometry proxy from
the available views using a lightweight stereo network,
then progressively refines the scene representation through
a geometry-conditioned neural implicit model. This design
decouples the problem into tractable sub-tasks: global
structure estimation and local detail refinement.
```

### 第 5 段：貢獻列表

- **目標**：以清單形式明確列出 3-4 個貢獻
- **格式**：使用 `\begin{itemize}` 或 `\begin{enumerate}`
- **技巧**：
  - 每個貢獻必須是**具體的、可驗證的**
  - 第一個貢獻通常是方法本身
  - 第二個貢獻通常是某個技術創新點
  - 最後一個貢獻通常是實驗結果
  - 避免說 "We are the first to..."（除非你 100% 確定）

**範例**：
```latex
In summary, our contributions are as follows:
\begin{itemize}
  \item We propose SparseRecon, a coarse-to-fine framework
    for sparse-view 3D reconstruction that explicitly
    leverages geometric priors to guide neural scene
    representations.
  \item We introduce a geometry-conditioned refinement
    module that adaptively allocates representational
    capacity based on the local geometric complexity,
    enabling detailed reconstruction in complex regions
    while maintaining efficiency.
  \item Extensive experiments on three benchmarks (DTU,
    BlendedMVS, Tanks\&Temples) demonstrate that SparseRecon
    outperforms existing methods by 2.3~dB PSNR on average
    using only 3 input views, while running 5$\times$ faster
    than the nearest competitor.
\end{itemize}
```

---

## 貢獻列表寫作要訣

### 好的貢獻 vs 壞的貢獻

```latex
% ❌ 太含糊、不可驗證
\item We propose a novel method for 3D reconstruction.

% ❌ 過度宣稱
\item We are the first to solve sparse-view reconstruction.

% ❌ 只是實作細節
\item We implement our method in PyTorch.

% ✅ 具體、可驗證
\item We propose a coarse-to-fine framework that decouples
  sparse-view reconstruction into geometry estimation and
  appearance refinement, reducing the problem complexity.

% ✅ 有數字支撐
\item Extensive experiments demonstrate state-of-the-art
  performance on three benchmarks, with 2.3 dB improvement
  in PSNR using 3$\times$ fewer input views.
```

### 貢獻的數量

- **最佳**：3 個貢獻
- **可接受**：2-4 個貢獻
- **過多**：5 個以上（會讓 reviewer 覺得你在灌水）
- **過少**：1 個（會讓 reviewer 覺得貢獻不夠）

### 貢獻的類型組合

推薦的組合方式：

| 貢獻 1 | 貢獻 2 | 貢獻 3 |
|--------|--------|--------|
| 方法/框架 | 技術創新 | 實驗結果 |
| 問題定義 | 解法 | 理論分析 + 實驗 |
| 新觀點/insight | 基於 insight 的方法 | 大規模實驗驗證 |

---

## 常見錯誤

### 錯誤 1：背景太長

```latex
% ❌ 整整一段都在講 deep learning 的歷史
Deep learning has achieved remarkable progress in the past
decade. Starting from AlexNet in 2012, convolutional neural
networks have dominated...

% ✅ 直接切入相關背景
3D scene understanding from images is fundamental to
robotics and AR applications.
```

### 錯誤 2：漏斗結構斷裂

問題描述和方法之間沒有邏輯銜接——reader 不知道為什麼你的方法能解決前面提到的問題。

**解法**：在描述方法前，用一句 "key observation" 或 "key insight" 連接問題和解法。

### 錯誤 3：貢獻列表與正文不符

Introduction 宣稱的貢獻在後文找不到對應的章節或實驗。

**解法**：寫完全文後回來對照，確保每個貢獻都有實驗驗證。

### 錯誤 4：攻擊先前工作

```latex
% ❌ 攻擊性語言
Previous methods are fundamentally flawed because...
The naive approach of [Author] fails to...

% ✅ 客觀分析
While effective in dense-view settings, these methods
face challenges when the number of input views is
limited, as the lack of multi-view correspondence
leads to ambiguous reconstructions.
```

### 錯誤 5：Figure 1 與文字脫節

Introduction 通常包含一張 Figure 1（方法概覽或問題示意圖）。這張圖必須與 Introduction 的文字緊密配合。

**建議**：在 Introduction 中至少引用 Figure 1 一次，並用文字解釋圖中展示的核心觀點。

---

## 段落銜接範本

以下是各段之間的銜接句型：

### 大背景 → 具體問題
- "Despite this progress, ..."
- "However, a critical limitation remains: ..."
- "While promising, these advances rely on ..."

### 具體問題 → 現有方法不足
- "To address this challenge, prior work has explored ..."
- "Existing approaches to this problem can be categorized into ..."

### 現有方法不足 → 我們的方法
- "In this work, we take a different approach."
- "Our key insight is that ..."
- "Motivated by [observation], we propose ..."

### 我們的方法 → 貢獻列表
- "In summary, our contributions are as follows:"
- "Our main contributions include:"
- "To summarize, we make the following contributions:"

---

## 自我檢查清單

寫完 Introduction 後，回答以下問題：

```
□ 讀完第一段，讀者能理解這個領域嗎？
□ 讀完第二段，讀者能理解具體問題嗎？
□ 讀完第三段，讀者能理解為什麼需要新方法嗎？
□ 讀完第四段，讀者能理解你的核心 idea 嗎？
□ 貢獻列表的每一條都是具體的、可驗證的嗎？
□ Figure 1 是否被引用並解釋？
□ 段落之間的邏輯銜接是否自然？
□ 是否避免了攻擊性語言？
□ 總長度是否控制在 1-1.5 頁？
```

---

*回到主文件 → `../SKILL.md`*
