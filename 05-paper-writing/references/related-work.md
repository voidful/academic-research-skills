# Related Work 相關工作寫作指南

## 核心原則

Related Work 不是文獻列表。它的目的是幫助讀者理解你的工作在研究版圖中的位置，以及你與先前工作的本質差異。寫得好的 Related Work 會讓 reviewer 覺得你對領域有深刻理解；寫得差的會讓他們覺得你只是在湊引用。

---

## 組織方式

### 方式 A：按主題分組（推薦）

將相關工作按照**技術主題**或**方法類別**分組，每組一個 subsection 或一個段落。

**優點**：
- 結構清晰，讀者容易找到感興趣的部分
- 自然引出你的方法與每組方法的差異
- 便於 reviewer 檢查你是否遺漏重要引用

**組織範例**：

```
3.1 Neural Implicit Representations
    [討論 NeRF 系列工作]

3.2 Sparse-View Reconstruction
    [討論稀疏視角重建工作]

3.3 Geometric Priors for 3D Reconstruction
    [討論幾何先驗工作]
```

**每個分組的結構**：

```latex
% 分組標題
\paragraph{Neural Implicit Representations.}
% 1. 簡述這個方向的起源和核心思想（1-2句）
Neural radiance fields (NeRF)~\cite{nerf} represent scenes
as continuous functions mapping 3D coordinates to color
and density, enabling photorealistic novel view synthesis.
% 2. 介紹主要進展（2-3句，引用關鍵論文）
Subsequent works have improved training
efficiency~\cite{instant_ngp,plenoxels}, generalization to
new scenes~\cite{pixelnerf,ibrnet}, and quality through
better regularization~\cite{mipnerf,regnerf}.
% 3. 指出與你的方法的關聯和差異（1-2句）★關鍵★
While these methods have advanced dense-view reconstruction,
they require substantial multi-view overlap. Our work builds
on the implicit representation framework but introduces
explicit geometric guidance to enable reconstruction from
as few as three views.
```

### 方式 B：按時間線（不推薦，但某些情況可用）

按時間順序介紹相關工作的發展脈絡。

**適用情境**：
- 綜述型論文
- 你的方法是某個研究脈絡的自然延伸
- 需要展示領域演進歷程

**風險**：容易寫成流水帳，缺乏深度分析。

### 方式 C：按問題維度（適用於多面向問題）

如果你的問題涉及多個面向，可以按面向分組。

**範例**（文字生成運動）：
```
3.1 Text Understanding for Motion
3.2 Motion Generation Models
3.3 Motion Quality Evaluation
```

---

## 差異化比較

Related Work 的核心價值在於差異化比較。每組相關工作的結尾必須說明你的方法與它們的**本質差異**。

### 差異化句型

```latex
% 強調不同的出發點
Unlike [方向A] which addresses X from the perspective of Y,
our work approaches it through Z.

% 強調不同的假設
While [方法A] assumes [假設], our method relaxes this
constraint by [做法].

% 強調不同的技術路線
In contrast to [方法A] that relies on [技術],
we leverage [不同技術] to achieve [效果].

% 強調互補關係
Our work is complementary to [方向A]; while they focus
on [面向], we address the orthogonal challenge of [面向].

% 強調改進
Building upon [方法A], our approach further improves
[面向] by introducing [新元素].
```

### 好的差異化 vs 壞的差異化

```latex
% ❌ 沒有實質差異化（空洞）
Our method is different from previous methods.

% ❌ 只是說「我們更好」
Our method outperforms all previous methods.

% ❌ 攻擊性語言
Previous methods are naive and ineffective.

% ✅ 具體的技術差異
Unlike PixelNeRF~\cite{pixelnerf} which predicts features
independently for each view, our method explicitly models
inter-view geometric consistency through a cost volume,
enabling more coherent reconstruction in overlapping regions.

% ✅ 互補角度
Our work is most related to RegNeRF~\cite{regnerf}, which
also addresses sparse-view reconstruction. While RegNeRF
regularizes geometry through rendered patch supervision,
our approach provides direct geometric guidance through
an estimated depth proxy. These strategies are complementary,
and we show in Sec.~\ref{sec:ablation} that combining them
yields further improvements.
```

---

## 避免變成文獻列表

### 文獻列表 vs 有分析的 Related Work

```latex
% ❌ 文獻列表（每篇論文一句話，沒有分析）
[A]~\cite{a} proposed X. [B]~\cite{b} introduced Y.
[C]~\cite{c} presented Z. [D]~\cite{d} developed W.

% ✅ 有分析的 Related Work（有歸納、有比較）
A family of methods~\cite{a,b,c} addresses X through the
shared strategy of Y. Among them, [A]~\cite{a} focuses on
[面向1], while [B]~\cite{b} extends this to [面向2].
A notable limitation of this approach is [限制], which
[D]~\cite{d} partially addresses through [方法] but at the
cost of [代價]. Our method avoids this trade-off entirely
by [做法].
```

### 分析的維度

對每組相關工作，可以從以下維度進行分析：

| 維度 | 問題 |
|------|------|
| 假設 | 這組方法做了什麼假設？這些假設合理嗎？ |
| 能力 | 這組方法能做什麼？不能做什麼？ |
| 代價 | 達成效果的代價是什麼？（計算量、資料需求等） |
| 限制 | 在什麼場景下會失效？ |
| 與本文關係 | 本文的方法如何克服這些限制？ |

---

## 引用數量建議

| 會議 | 建議引用數 | Related Work 長度 |
|------|----------|-----------------|
| NeurIPS/ICML | 30-50 | 0.5-1 頁 |
| ICLR | 30-50 | 0.5-1 頁 |
| CVPR/ECCV | 40-60 | 0.5-1 頁 |
| ACL/EMNLP | 30-50 | 0.75-1 頁 |

### 引用策略

- **必須引用**：直接相關的工作（方法類似或問題相同）
- **應該引用**：同一方向的重要里程碑論文
- **可以引用**：相關但不同方向的背景知識
- **避免引用**：與你的工作完全無關的論文（灌引用會被 reviewer 看出來）

### Reviewer 常見的引用相關質疑

- "The authors missed important related work: [X]" → 確保覆蓋所有主要方向
- "The comparison with [X] is missing" → 在 Related Work 和 Experiments 中都要有
- "The distinction from [X] is unclear" → 每組相關工作結尾必須有差異化

---

## 位置選擇

Related Work 的位置有兩種常見選擇：

### 選項 1：Introduction 之後（Section 2）

- **適用**：Related Work 為後續 Method 提供必要背景知識
- **優點**：讀者有足夠背景理解你的方法
- **常見於**：大多數論文

### 選項 2：Experiments 之後

- **適用**：Method 不需要太多背景知識就能理解
- **優點**：讀者更快看到你的技術貢獻
- **常見於**：NeurIPS 部分論文、方法非常直覺的論文

**建議**：除非有特殊理由，預設放在 Introduction 之後。

---

## 自我檢查清單

```
□ 是否按主題分組而非逐篇列舉？
□ 每個分組是否有 2 句以上的分析（而非只是列舉）？
□ 每個分組結尾是否說明了與本文的差異？
□ 是否覆蓋了所有 reviewer 可能想到的相關方向？
□ 是否引用了最新的相關論文（近 1-2 年）？
□ 是否避免了攻擊性語言？
□ 總長度是否控制在 0.5-1 頁？
□ 引用格式是否統一且正確？
```

---

*回到主文件 → `../SKILL.md`*
