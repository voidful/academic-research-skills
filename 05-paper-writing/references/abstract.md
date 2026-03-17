# Abstract 摘要寫作指南

## 核心原則

摘要是整篇論文的縮影。Reviewer 讀完摘要後，對你的論文已經有了 70% 的判斷。一個好的摘要必須在 150-250 字內回答四個問題。

---

## 4 句話結構

每篇頂級會議論文的摘要都可以拆解為以下四個部分（不一定恰好各一句，但邏輯上必須涵蓋）：

### 第 1 部分：問題（Problem）

- **目標**：告訴讀者你在解決什麼問題，以及為什麼這個問題重要
- **長度**：1-2 句
- **要點**：
  - 問題本身必須是大家認同的、有價值的
  - 避免過於狹窄（"We address the task of predicting X on dataset Y"）
  - 從更高的角度切入（"Understanding 3D scenes from limited observations remains a fundamental challenge in ..."）

**範例**：
```latex
% 好的問題陳述
Reconstructing high-fidelity 3D scenes from sparse observations
is essential for applications in robotics and augmented reality,
yet remains challenging due to the inherent ambiguity of
under-constrained views.

% 壞的問題陳述（太狹窄）
We study the problem of novel view synthesis on the DTU dataset.
```

### 第 2 部分：方法（Approach）

- **目標**：用一句話概括你的核心方法思路
- **長度**：1-2 句
- **要點**：
  - 不要講技術細節，講核心 idea
  - 強調「為什麼你的方法能解決上述問題」
  - 使用 "We propose / We present / We introduce" 開頭

**範例**：
```latex
% 好的方法描述
We present SparseRecon, a coarse-to-fine framework that first
estimates a rough geometry proxy from available views, then
progressively refines it through a learned neural implicit
representation conditioned on local features.

% 壞的方法描述（太含糊）
We propose a novel deep learning method for this task.

% 壞的方法描述（太詳細）
We use a ResNet-50 backbone followed by three transformer layers
with 8 attention heads and a hidden dimension of 512...
```

### 第 3 部分：結果（Results）

- **目標**：用具體數字展示你的方法的效果
- **長度**：1-2 句
- **要點**：
  - 必須有具體數字（百分比、提升幅度）
  - 提及你在哪些 benchmark 上做了實驗
  - 與 SOTA 做明確比較

**範例**：
```latex
% 好的結果描述
Extensive experiments on three standard benchmarks (DTU, BlendedMVS,
and Tanks\&Temples) demonstrate that SparseRecon outperforms
existing methods by 2.3 dB PSNR on average while requiring
only 3 input views, compared to 10+ views for prior approaches.

% 壞的結果描述（沒有數字）
Experiments show that our method achieves superior performance
compared to existing approaches.
```

### 第 4 部分：影響（Impact / Takeaway）

- **目標**：告訴讀者這個工作的更廣泛意義或啟示
- **長度**：1 句
- **要點**：
  - 這部分是可選的，但有的話會讓摘要更完整
  - 可以提到開源計畫、更廣泛的適用性、或揭示的 insight
  - 不要過度宣稱

**範例**：
```latex
% 好的影響描述
Our results suggest that explicit geometric reasoning,
even at a coarse level, provides a strong inductive bias
that significantly reduces the view requirements for
high-quality reconstruction.

% 壞的影響描述（過度宣稱）
Our method will revolutionize the field of 3D reconstruction.
```

---

## 長度建議

| 會議 | 建議字數 | 備註 |
|------|---------|------|
| NeurIPS | 150-200 字 | 簡潔為上 |
| ICLR | 150-250 字 | 可以稍長 |
| CVPR/ECCV | 150-200 字 | 通常較短 |
| ACL | 200-250 字 | NLP 論文摘要稍長 |
| AAAI | 150 字 | 版面限制嚴格 |

**黃金法則**：如果你的摘要超過 250 字，幾乎一定可以刪減。

---

## 常見錯誤

### 錯誤 1：缺少具體數字

```latex
% ❌ 沒有數字的摘要
Our method achieves state-of-the-art performance on multiple
benchmarks, significantly outperforming existing methods.

% ✅ 有數字的摘要
Our method achieves 78.3% mAP on COCO, outperforming the
previous best (75.1%) by 3.2 points, while using 40% fewer
parameters.
```

### 錯誤 2：背景太長

```latex
% ❌ 背景佔了摘要一半
Deep learning has achieved remarkable progress in computer vision.
Convolutional neural networks have been widely adopted for image
classification, object detection, and semantic segmentation.
Recently, transformer architectures have shown promising results...
[然後才開始說自己的方法]

% ✅ 直奔主題
Semantic segmentation in low-resource settings remains challenging
as existing methods require large-scale pixel-level annotations.
We propose...
```

### 錯誤 3：使用禁用詞彙

```latex
% ❌ 花俏詞彙
We propose a novel and groundbreaking framework that dramatically
revolutionizes the field of...

% ✅ 平實描述
We propose a framework that addresses [specific problem] by
[specific technique], achieving [specific result].
```

### 錯誤 4：沒有提到問題的重要性

```latex
% ❌ 直接說方法，不說為什麼
We propose a new method for X. Our method uses A and B.

% ✅ 先說為什麼再說方法
X is critical for [application] but existing methods suffer
from [limitation]. We propose a new method that addresses
this by [approach].
```

### 錯誤 5：過度壓縮方法描述

```latex
% ❌ 方法描述太含糊
We use a learning-based approach.

% ✅ 清楚說明核心 idea
We introduce a two-stage approach: first learning a geometric
prior from synthetic data, then adapting it to real scenes
through a self-supervised refinement module.
```

---

## 完整好範例

```latex
\begin{abstract}
Generating realistic human motions from text descriptions enables
numerous applications in animation, gaming, and virtual reality,
yet remains challenging due to the complexity of human dynamics
and the ambiguity of natural language.  % [問題]
%
We present MotionCraft, a diffusion-based framework that decomposes
the text-to-motion generation into semantic planning and motion
synthesis stages, where the planner first extracts structured
action primitives from text, and the synthesizer generates
temporally coherent motions conditioned on these primitives.  % [方法]
%
On the HumanML3D and KIT-ML benchmarks, MotionCraft achieves
an FID of 0.141 and 0.532 respectively, improving over the
previous state-of-the-art by 18.5\% and 12.3\%, while
producing motions rated 4.2/5.0 in human perceptual studies. % [結果]
%
Our analysis reveals that explicit semantic decomposition not
only improves generation quality but also provides interpretable
control over the generation process.  % [影響]
\end{abstract}
```

---

## 寫作流程建議

1. **最後寫**：摘要應該在全文完成後才寫，這樣你最清楚論文的核心貢獻
2. **先寫長版**：先不管字數限制，把想說的都寫下來
3. **刪減到目標字數**：每一句都問「這句必要嗎？」
4. **請他人閱讀**：找一個不熟悉你工作的人讀摘要，看他們能否理解
5. **對照 4 句話結構**：確認四個部分都有涵蓋

---

*回到主文件 → `../SKILL.md`*
