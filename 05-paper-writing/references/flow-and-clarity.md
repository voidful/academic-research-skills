# Flow and Clarity 段落邏輯與文章流暢度

## 核心原則

一篇好論文讀起來像在聽一個流暢的故事：每一段自然地引出下一段，讀者永遠不會問「為什麼突然在講這個？」。好的 flow 是看不見的——讀者只會覺得「很好懂」而不會意識到你在刻意銜接。壞的 flow 則會讓 reviewer 寫下 "The paper is hard to follow" 或 "The presentation needs improvement"。

---

## 段落邏輯驗證方法

### 方法 1：Topic Sentence 串讀法

將每個段落的第一句（topic sentence）單獨抽出來，按順序排列。如果只讀這些 topic sentence 就能理解整篇論文的邏輯脈絡，說明結構是合理的。

**操作步驟**：

1. 在每段的第一句旁標記 [T1], [T2], [T3]...
2. 將所有 topic sentence 列出來
3. 檢查：
   - 相鄰的 topic sentence 之間有邏輯關係嗎？
   - 整體是否構成一個完整的論述？
   - 有沒有邏輯跳躍？

**範例**：

```
[T1] 3D reconstruction from sparse views is important
     for robotics applications.
[T2] However, existing methods require dense input views.
[T3] Prior approaches fall into two categories.
[T4] Regression-based methods struggle with unseen regions.
[T5] Generative approaches produce geometrically
     inconsistent results.
[T6] We observe that coarse geometry provides sufficient
     guidance.
[T7] We propose SparseRecon, a coarse-to-fine framework.
[T8] Our contributions are as follows.
```

上面的 topic sentence 串起來構成了一個完整的 Introduction 邏輯。

### 方法 2：因果鏈驗證法

對每對相鄰段落，問一個問題：「為什麼讀者讀完上一段之後，會想讀下一段？」

可能的回答（邏輯關係）：

| 關係 | 說明 | 連接詞 |
|------|------|--------|
| 因果 | 上段引出問題，下段回答 | Therefore / Thus |
| 轉折 | 上段說了一面，下段說另一面 | However / Despite |
| 遞進 | 下段深化上段的論點 | Furthermore / Moreover |
| 具體化 | 下段是上段的具體實現 | Specifically / In particular |
| 分支 | 上段提出多面向，下段處理其中一個 | First / Regarding |

如果找不到邏輯關係，說明兩段之間存在**邏輯斷裂**。

### 方法 3：問答檢驗法

在每段結尾想像讀者會問什麼問題，下一段必須回答這個問題：

```
段落 1：3D reconstruction from sparse views is challenging.
         → 讀者問：「現有方法怎麼做的？」

段落 2：Existing methods fall into regression and generation.
         → 讀者問：「這些方法有什麼問題？」

段落 3：Both families lack explicit geometric reasoning.
         → 讀者問：「那你怎麼解決？」

段落 4：Our key insight is that coarse geometry suffices.
         → 讀者問：「具體怎麼做？」

段落 5：We propose SparseRecon, a coarse-to-fine framework.
         → 讀者問：「你的貢獻是什麼？」

段落 6：Our contributions are: (1)... (2)... (3)...
```

如果某一段沒有回答上一段引出的問題，就是邏輯斷裂。

---

## Topic Sentence → Support → Transition

每個段落都遵循三部分結構：

### Topic Sentence（主題句）

段落的第一句，宣告本段的核心訊息。

**好的 topic sentence 特徵**：
- 可以獨立成為一個完整的 claim
- 後續句子都在支撐或展開這個 claim
- 讀者讀完就知道這段在說什麼

```latex
% ✅ 好的 topic sentence
The cost volume provides a robust geometric prior
even under severe occlusion.

% ❌ 壞的 topic sentence（太含糊）
We describe our method in this section.

% ❌ 壞的 topic sentence（太細節）
We set the number of depth hypotheses to 128.
```

### Support（支撐句）

提供證據、解釋、或例子來支撐 topic sentence：

| 支撐類型 | 作用 | 範例 |
|---------|------|------|
| 解釋 | 說明為什麼 topic sentence 是對的 | "This is because the cost volume aggregates information across all view pairs, providing redundancy against single-view failures." |
| 證據 | 用數據支撐 | "As shown in Table 3, removing the cost volume reduces PSNR by 2.4 dB." |
| 例子 | 用具體案例說明 | "For instance, in scene X where 60% of the target view is occluded, ..." |
| 對比 | 與替代方案比較 | "In contrast, monocular depth estimates lack multi-view consistency, leading to artifacts at view boundaries." |

**順序建議**：解釋 → 證據 → 例子 → 對比

### Transition（轉換）

段落結尾或下一段開頭的銜接，引導讀者進入下一個話題：

**轉換的位置**：

```
選項 A：在當前段落結尾（段尾轉換）
[Topic] [Support] [Support] [Transition → 預告下段]

選項 B：在下一段落開頭（段首轉換）
[Transition ← 回顧上段] [Topic] [Support] [Support]
```

**段尾轉換範例**：
```latex
...the cost volume provides a robust geometric prior.
However, this coarse geometry alone is insufficient for
high-quality rendering, motivating our refinement module
described next.
```

**段首轉換範例**：
```latex
While the geometry estimation module provides a strong
structural foundation, the resulting depth maps are too
coarse for photo-realistic rendering. To address this,
we introduce a geometry-conditioned refinement module.
```

---

## 前後文連貫性檢查

### 檢查 1：術語一致性

全文對同一概念必須使用同一術語：

```
❌ 混用（讀者會困惑這是否是不同的東西）
- 段落 1 用 "feature representation"
- 段落 3 用 "feature embedding"
- 段落 5 用 "latent code"

✅ 統一
- 全文統一用 "feature representation"
- 首次出現時定義："feature representation
  (i.e., the output of the encoder)"
```

**檢查方法**：搜尋論文中所有指代同一概念的詞彙，確保一致。

### 檢查 2：邏輯前後不矛盾

```
❌ 矛盾
- Introduction: "Our method requires no additional
  supervision beyond RGB images."
- Method: "We use ground-truth depth for training the
  geometry module."

✅ 一致
- Introduction: "Our method leverages only RGB images
  and coarse depth estimates at training time."
- Method: "During training, we use pseudo ground-truth
  depth from a pretrained stereo model."
```

**檢查方法**：列出所有 claim，逐一對照實驗和方法的描述。

### 檢查 3：數字一致

```
❌ 數字不一致
- Abstract: "improves by 2.3 dB"
- Experiments: Table 1 顯示改進了 2.29 dB
- Conclusion: "gains of 2.5 dB"

✅ 一致
- 全文統一使用 "2.3 dB"（可以在表格中顯示精確值 2.29）
```

### 檢查 4：引用前後呼應

在 Introduction 中提到的問題/方法，必須在後文中有對應：

| Introduction 提到 | 必須在後文出現 |
|------------------|--------------|
| 問題 X 很重要 | Experiments 中解決 X 的實驗 |
| 現有方法的缺陷 Y | Method 中描述如何克服 Y |
| 貢獻 Z | Method 中 Z 的詳細描述 + Experiments 中 Z 的實驗驗證 |

---

## 常見邏輯斷裂模式

### 模式 1：跳躍式論述

```
段落 1：我們的方法使用 cost volume 估計幾何。
段落 2：表 3 顯示我們的方法在 DTU 上達到 25.4 dB。

問題：從方法描述直接跳到結果，沒有過渡。

修正：在兩段之間加入「實驗設定」或「我們驗證 cost volume
的有效性」的過渡段落。
```

### 模式 2：無頭段落

```
段落：Additionally, we apply batch normalization after
each convolutional layer. The kernel size is set to 3.
We use ReLU activation.

問題：這段沒有 topic sentence，讀者不知道為什麼要
讀這些細節。

修正：加入 topic sentence —— "To stabilize training and
improve convergence, we adopt standard architectural
design choices for the feature extractor:"
```

### 模式 3：回力鏢

```
段落 1：介紹方法 A
段落 2：介紹方法 B
段落 3：又回來補充方法 A 的細節

問題：讀者讀到段落 3 時已經在想方法 B 了，
突然被拉回方法 A 會很困惑。

修正：把方法 A 的所有內容集中在一起。
```

### 模式 4：假設讀者有超能力

```
"As discussed earlier, ..."（但之前沒有討論過）
"It is well known that ..."（對你來說 well known，
對讀者不一定）
"Following standard practice, ..."（什麼 standard？引用？）

修正：加入具體引用或回指（"As shown in Eq. (3), ..."
或 "Following the protocol of [ref], ..."）
```

### 模式 5：不對稱的結構

```
3.1 Module A（2 頁詳細描述）
3.2 Module B（3 行帶過）
3.3 Module C（1.5 頁詳細描述）

問題：如果 Module B 很重要，描述太短讓人懷疑完整性。
如果不重要，為什麼要單獨一個 subsection？

修正：要嘛擴充 Module B 的描述，要嘛將其合併到
其他 subsection 中。
```

---

## Section 間的邏輯流

### Introduction → Related Work

Introduction 末尾的貢獻列表自然引出 "在描述方法細節前，我們先回顧相關工作"：

```latex
% Introduction 結尾
...our contributions are: (1)... (2)... (3)...

% Related Work 開頭
Before describing our approach in detail, we review
the most relevant prior work in three areas: ...
```

### Related Work → Method

Related Work 末尾指出 gap，Method 開頭填補這個 gap：

```latex
% Related Work 結尾
...existing methods either [限制A] or [限制B]. Our
approach addresses both limitations through a unified
framework.

% Method 開頭
We now describe our proposed framework that overcomes
the limitations outlined above.
```

### Method → Experiments

Method 末尾可以預告實驗，Experiments 開頭回顧要驗證什麼：

```latex
% Method 結尾
[損失函數描述]... The training procedure is summarized
in Algorithm 1.

% Experiments 開頭
We evaluate our method on three benchmarks to answer
the following questions: (1) Does SparseRecon outperform
existing sparse-view methods? (2) How important is each
component? (3) How does performance scale with the
number of input views?
```

### Experiments → Conclusion

Experiments 末尾的分析自然引出結論中的總結和限制討論。

---

## 實用工具

### 連貫性自檢表

在完成論文初稿後，逐項檢查：

```
□ 所有 topic sentence 串讀起來構成完整論述？
□ 相鄰段落之間都有明確的邏輯關係？
□ 沒有邏輯跳躍（每一步都有鋪陳）？
□ 沒有回力鏢（同一主題的內容集中在一起）？
□ 術語全文一致？
□ 數字全文一致？
□ 所有 claim 都有前後呼應（提出→論證→驗證）？
□ Section 之間的銜接自然？
□ 沒有假設讀者有超能力的地方？
□ 結構對稱（類似組件用類似篇幅描述）？
```

### 快速修復策略

| 問題 | 快速修復 |
|------|---------|
| 邏輯跳躍 | 加一個銜接句或一個短段落 |
| 無頭段落 | 加 topic sentence |
| 回力鏢 | 重新組織段落順序 |
| 術語不一致 | 全文搜尋替換 |
| 結構不對稱 | 擴充短的 or 精簡長的 |

---

*回到主文件 → `../SKILL.md`*
