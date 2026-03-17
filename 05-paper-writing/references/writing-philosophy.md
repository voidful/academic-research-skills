# Writing Philosophy 寫作鐵律與禁忌

## 核心信念

學術論文不是文學作品，也不是行銷文案。它的唯一目的是**精確、高效地傳遞資訊**。每一個字都必須服務於這個目的。多餘的字不是裝飾，是噪音。

---

## 30 秒法則

### 原理

學術 reviewer 每年審數十篇到上百篇論文。他們沒有時間仔細讀每一個字。研究顯示，reviewer 在前 30 秒內就會形成對論文的初步印象，而這個印象對最終評分有巨大影響。

### 30 秒內 reviewer 看的東西

按優先順序排列：

1. **標題**（5 秒）
   - 能否立即理解這篇論文在做什麼？
   - 是否有新穎的關鍵詞吸引注意？

2. **摘要**（10 秒）
   - 前兩句能否理解問題和方法？
   - 最後一句有沒有數字結果？

3. **Figure 1**（10 秒）
   - 能否直覺理解方法的核心？
   - 圖的品質是否專業？

4. **Table 1 / 主結果**（5 秒）
   - 有沒有加粗的最佳結果？
   - 改進幅度明顯嗎？

### 實踐方法

#### 標題優化

```
❌ 模糊標題
A Deep Learning Approach for 3D Reconstruction

❌ 太長的標題
A Novel Coarse-to-Fine Neural Implicit Representation
Framework with Geometric Guidance for High-Quality
Sparse-View 3D Scene Reconstruction

✅ 清晰、適中的標題
SparseRecon: Geometry-Guided Neural Reconstruction
from Sparse Views
```

**標題公式**：[方法名稱]: [核心技術] for [目標任務]

#### 摘要前兩句優化

```
❌ 前兩句還在講背景
Deep learning has revolutionized computer vision.
3D reconstruction is an important task.

✅ 前兩句直奔主題
Reconstructing 3D scenes from sparse views remains
challenging due to insufficient multi-view overlap.
We present SparseRecon, a coarse-to-fine framework
that leverages explicit geometric priors to guide
neural reconstruction.
```

#### Figure 1 優化

- 必須是**自解釋的**——不看正文也能理解
- 字體要足夠大（列印後仍可讀）
- 標註要清楚（輸入→處理→輸出的流向）
- 如果是結果對比圖，要有明顯的視覺差異

#### Table 1 優化

- 最佳結果加粗，一眼可見
- 你的方法在最後一行，用 `\midrule` 分隔
- 改進幅度最好 > 1%（否則 reviewer 不會印象深刻）

---

## 禁用詞彙完整清單

### 絕對禁止

這些詞在任何情況下都不應該出現在學術論文中：

| 禁用詞 | 問題 | 替代 |
|--------|------|------|
| novel | 過度使用，已失去意義 | we propose / we introduce / we present |
| groundbreaking | 誇大 | effective / promising / competitive |
| revolutionize | 誇大 | improve / advance / enable |
| dramatically | 誇大 | significantly / substantially / by X% |
| obviously | 傲慢 | (直接陳述事實) |
| clearly | 可能不 clear | As shown in Fig. X / Table X shows |
| very / really | 空洞 | (用具體數字代替) |
| of course | 傲慢 | (直接陳述事實) |
| trivially | 對讀者不友善 | straightforwardly / directly |
| interestingly | 主觀 | notably / we observe that |
| unfortunately | 不必要的情感 | however / a limitation is |
| believe | 主觀 | hypothesize / expect / observe |

### 謹慎使用

以下詞彙不是完全禁止，但需要明確的支持證據：

| 詞彙 | 使用條件 |
|------|---------|
| state-of-the-art | 只在你確實超越所有現有方法時 |
| significant | 只在有統計檢驗支持時 |
| outperform | 只在有具體數字時 |
| superior | 只在有多個指標支持時 |
| robust | 只在有跨條件實驗支持時 |
| efficient | 只在有效率數據（FLOPs、時間）支持時 |
| generalize | 只在有跨資料集實驗支持時 |
| scalable | 只在有 scaling 實驗支持時 |

### 推薦的學術用語

| 場景 | 推薦用語 |
|------|---------|
| 提出方法 | We propose / present / introduce |
| 描述結果 | achieves / attains / yields |
| 比較優勢 | improves over / outperforms ... by X |
| 觀察現象 | We observe that / We find that |
| 分析原因 | This is because / We attribute this to |
| 假設 | We hypothesize that / We conjecture that |
| 承認限制 | A limitation of our approach is / Our method may struggle with |

---

## 段落結構規則

### 規則 1：Topic Sentence 開頭

每個段落的第一句必須是 topic sentence，概括本段的核心訊息：

```latex
% ✅ 清晰的 topic sentence
The geometry estimation module is the cornerstone of
our framework. [接下來解釋為什麼...]

% ❌ 沒有 topic sentence
We first extract features using a CNN. Then we compute
a cost volume. After that, we apply regularization...
% [讀者不知道這段在說什麼]
```

### 規則 2：一段一訊息

每個段落只傳遞一個核心訊息。檢驗方法：如果你能用一句話概括這個段落，就是好的；如果需要兩句以上，就要拆分。

```
❌ 一段包含兩個訊息
Our geometry module estimates depth maps. [細節...]
Additionally, we found that data augmentation significantly
improves generalization. [細節...]

✅ 拆成兩段
[段落 1] Our geometry module estimates depth maps. [細節...]

[段落 2] To improve generalization, we apply data
augmentation during training. [細節...]
```

### 規則 3：段落長度

- **最佳**：4-8 句
- **可接受**：3-10 句
- **太短**：1-2 句（通常可以合併到相鄰段落）
- **太長**：超過 10 句（必須拆分）

### 規則 4：段落間轉換

相鄰段落之間必須有邏輯銜接。常用的轉換方式：

| 轉換類型 | 範例 |
|---------|------|
| 因果 | Therefore / As a result / Consequently |
| 對比 | However / In contrast / On the other hand |
| 遞進 | Furthermore / Moreover / In addition |
| 具體化 | Specifically / In particular / More concretely |
| 總結 | In summary / Overall / To summarize |
| 時間 | First / Then / Finally |

---

## 句子層面的寫作原則

### 原則 1：主動語態優先

```latex
% ❌ 被動（弱）
The features are extracted by the encoder.

% ✅ 主動（強）
The encoder extracts features from the input image.
```

例外：描述普遍做法時可以用被動（"X is widely used in ..."）

### 原則 2：避免長句

如果一個句子超過 30 個字，考慮拆分：

```latex
% ❌ 太長
We propose a method that first estimates coarse geometry
using a cost volume constructed from multi-view feature
correlations and then refines the reconstruction through
a neural implicit representation conditioned on the
geometry-aware features extracted from the input views.

% ✅ 拆分
We first estimate coarse geometry using a cost volume
built from multi-view feature correlations. We then
refine the reconstruction through a neural implicit
representation, conditioned on geometry-aware features
from the input views.
```

### 原則 3：平行結構

列舉時保持語法結構一致：

```latex
% ❌ 不平行
Our method (1) estimates geometry, (2) extraction of
features, and (3) rendering novel views.

% ✅ 平行
Our method (1) estimates geometry, (2) extracts features,
and (3) renders novel views.
```

### 原則 4：避免模糊指代

```latex
% ❌ 模糊的 "this"
We compute the cost volume and regularize it. This
improves the result significantly.
% [讀者不知道 "This" 指什麼：計算、正則化、還是兩者？]

% ✅ 明確指代
We compute the cost volume and regularize it. This
regularization step improves reconstruction quality
by 1.5 dB.
```

---

## 常見語法錯誤

| 錯誤 | 範例 | 修正 |
|------|------|------|
| 冠詞缺失 | "We use network to..." | "We use **a** network to..." |
| 主詞動詞不一致 | "The results shows..." | "The results show..." |
| 懸吊修飾 | "Using our method, the results improved." | "Using our method, **we** improved the results." |
| 逗號拼接 | "We train the model, it converges in 10 epochs." | "We train the model**;** it converges in 10 epochs." |
| that/which 混用 | 限定用 which | 限定用 **that**，非限定用 **which** |

---

## 自我編輯流程

寫完每個段落後，依序問自己：

```
1. 這段的 topic sentence 是什麼？
2. 每一句都服務於這個 topic 嗎？
3. 有沒有句子可以刪除而不影響理解？
4. 有沒有使用禁用詞彙？
5. 有沒有超過 30 字的長句？
6. 與上下段的銜接是否自然？
```

如果答案有任何一個「否」，就需要修改。

---

*回到主文件 → `../SKILL.md`*
