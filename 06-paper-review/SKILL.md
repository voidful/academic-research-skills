---
name: paper-review
description: "學術論文審稿技能 — 以結構化四步驟流程完成深度論文審查，涵蓋批判性審查、分數預測、要點精煉與正式審稿產出。當使用者需要 review 一篇論文、模擬 reviewer 反應、評估論文能否被接收、或幫助判斷論文優缺點時，一定要使用此技能。觸發詞包括：review 這篇、幫我審稿、reviewer 會怎麼說、這篇能上嗎、paper review、給分數、找 weakness。適用於任何學術論文的審稿模擬與評估。"
version: 1.0.0
author: weed
---

# 06-paper-review：學術論文審稿技能

## 概述

本技能提供一套系統化的學術論文審稿流程，適用於頂級會議（如 NeurIPS、ICML、ICLR、ACL、CVPR 等）與期刊的同儕審查。整個流程分為四個步驟，前三步以繁體中文進行深度分析，第四步產出符合會議格式的英文正式審稿。

### 核心理念

- **嚴謹但公平**：審稿的目的是提升學術品質，而非打壓作者
- **具體而非模糊**：所有批評都應指向具體段落、公式或實驗
- **建設性導向**：指出問題的同時提供改進方向
- **多維度評估**：不以單一標準論斷，全面考量論文各面向

---

## 四步驟審稿流程

### 總覽

| 步驟 | 名稱 | 語言 | 目的 |
|------|------|------|------|
| Step 1 | 批判性審查 | 繁體中文 | 深入閱讀，找出優缺點 |
| Step 2 | 分數預測 | 繁體中文 | 各維度評分與整體分數預測 |
| Step 3 | 要點精煉 | 繁體中文 | 將發現整理為結構化要點 |
| Step 4 | 正式審稿 | 英文 | 產出符合會議格式的正式 review |

---

### Step 1：批判性審查（繁體中文）

#### 目標

以批判性思維深入閱讀論文，系統性地識別優點與缺點。此步驟為後續所有分析的基礎。

#### 執行方式

1. **第一遍：快速瀏覽（5 分鐘思維）**
   - 閱讀標題、摘要、導論、結論
   - 瀏覽圖表與表格
   - 形成初步印象：這篇論文在做什麼？聲稱了什麼貢獻？

2. **第二遍：仔細閱讀（30 分鐘思維）**
   - 逐節閱讀，標記不清楚的地方
   - 檢查數學推導的正確性
   - 驗證實驗設置的合理性
   - 確認 claims 是否有充分支持

3. **第三遍：批判性分析（15 分鐘思維）**
   - 對照五大審查維度逐一評估
   - 識別是否符合五大退稿模式
   - 思考 missing baselines、missing ablations、missing analysis

#### 輸出格式

```
## Step 1：批判性審查

### 論文基本資訊
- 標題：
- 作者：
- 投稿會議/期刊：
- 領域：

### 初步印象
（一段話總結論文做了什麼、聲稱了什麼）

### 優點列表
1. [S1] （具體描述優點，引用論文段落或頁碼）
2. [S2] ...

### 缺點列表
1. [W1] （具體描述缺點，說明為什麼這是問題）
2. [W2] ...

### 疑問列表
1. [Q1] （需要作者釐清的問題）
2. [Q2] ...

### 初步判斷
（對論文品質的初步判斷，包含是否達到會議門檻的直覺）
```

#### 注意事項

- 優點和缺點都要具體，避免「寫得不錯」「實驗不足」這類空泛評語
- 每個優缺點都應該能對應到論文的具體位置
- 疑問列表要區分「真正的疑問」與「修辭性的批評」
- 初步判斷只是直覺，不要被它錨定——後續步驟可能改變結論

---

### Step 2：分數預測（繁體中文）

#### 目標

基於 Step 1 的分析，對論文的五個維度分別評分，並預測整體分數。

#### 五大審查維度

每個維度以 1-5 分評分。詳細評分標準見 `references/scoring-rubric.md`。

| 維度 | 說明 | 權重參考 |
|------|------|----------|
| 貢獻新穎性 (Novelty & Contribution) | 想法是否新穎？貢獻是否足夠？ | 高 |
| 寫作清晰度 (Clarity & Writing) | 論文是否易讀？邏輯是否清晰？ | 中 |
| 實驗嚴謹性 (Experimental Rigor) | 實驗設計是否嚴謹？結果是否可靠？ | 高 |
| 評估完整性 (Evaluation Completeness) | 評估是否全面？是否有遺漏的比較？ | 中高 |
| 方法健全性 (Soundness of Method) | 方法是否正確？假設是否合理？ | 高 |

詳細的維度說明請參考 `references/review-dimensions.md`。

#### 評分體系

- **Overall Score（整體分數）**：1-10 分，詳見 `references/scoring-rubric.md`
- **Confidence（信心度）**：1-5 分，反映審稿者對自身評估的確信程度
- **各維度分數**：1-5 分

#### 輸出格式

```
## Step 2：分數預測

### 各維度評分

| 維度 | 分數 (1-5) | 簡要理由 |
|------|-----------|----------|
| 貢獻新穎性 | X | （一句話理由） |
| 寫作清晰度 | X | （一句話理由） |
| 實驗嚴謹性 | X | （一句話理由） |
| 評估完整性 | X | （一句話理由） |
| 方法健全性 | X | （一句話理由） |

### 整體分數預測
- **Overall Score**: X / 10
- **Confidence**: X / 5

### 分數推理
（解釋為什麼給這個整體分數，各維度如何影響最終判斷）

### 與接受門檻的比較
（討論這篇論文相對於目標會議的接受門檻如何，是 clear accept、borderline 還是 clear reject）
```

#### 注意事項

- 各維度分數應與 Step 1 的優缺點一致
- 整體分數不是各維度的簡單平均——有些致命缺陷會直接拉低整體分數
- Confidence 要誠實——如果你不熟悉這個子領域，信心度應該較低
- 考慮會議的接受率（如 NeurIPS ~25%、ICML ~25%、workshop ~50%）

---

### Step 3：要點精煉（繁體中文）

#### 目標

將 Step 1 和 Step 2 的分析整理為精煉的結構化要點，作為 Step 4 正式審稿的草稿。

#### 執行方式

1. **合併與去重**：將 Step 1 的優缺點合併，去除重複
2. **排序**：按重要性排序，最重要的放最前面
3. **補充細節**：為每個要點補充具體的論文引用與建議
4. **分類**：區分 major concerns 和 minor concerns
5. **撰寫建議**：為每個缺點提供具體的改進建議

#### 輸出格式

```
## Step 3：要點精煉

### 核心優點（按重要性排序）
1. [Major S1] （精煉描述 + 論文引用）
2. [Major S2] ...

### 重大問題（Major Concerns）
1. [Major W1] （精煉描述 + 為什麼重要 + 建議改進方向）
2. [Major W2] ...

### 次要問題（Minor Concerns）
1. [Minor W1] （精煉描述 + 建議改進方向）
2. [Minor W2] ...

### 必問問題（Questions for Authors）
1. [Q1] （精煉問題 + 為什麼這個答案很重要）
2. [Q2] ...

### 一句話總結
（用一句話總結對這篇論文的評價）
```

#### 注意事項

- Major 和 Minor 的區分要明確——Major 是會影響接受與否的問題
- 每個缺點都應該附帶建議，體現建設性審稿精神
- 問題要有策略性——好的問題能幫助你在 rebuttal 後做出更好的判斷
- 建設性回饋的寫法請參考 `references/constructive-feedback.md`

---

### Step 4：正式審稿（英文）

#### 目標

基於前三步的繁中分析，產出符合會議格式的英文正式 review。

#### 執行方式

1. 使用 `templates/review-form.md` 中的模板
2. 將 Step 3 的要點翻譯並潤飾為學術英文
3. 確保語氣專業、客觀、建設性
4. 檢查是否遺漏了重要的優缺點

#### 正式審稿結構

```
## Summary
（2-4 句話總結論文的主要貢獻與方法）

## Strengths
1. [S1] ...
2. [S2] ...

## Weaknesses
1. [W1] ...
2. [W2] ...

## Questions for Authors
1. [Q1] ...
2. [Q2] ...

## Suggestions for Improvement
1. ...
2. ...

## Minor Issues
- （格式、typo、文法等小問題）

## Rating
- Overall: X/10
- Confidence: X/5

## Justification
（簡短解釋你的評分理由）
```

#### 語氣指引

- **避免**：「This paper is bad.」「The authors clearly don't understand...」
- **推薦**：「The paper would benefit from...」「It is unclear how...」「A potential concern is...」
- 使用學術審稿的慣用語（參考 `references/constructive-feedback.md`）
- 批評要對事不對人——評論論文，不評論作者

#### 注意事項

- Summary 要準確反映論文內容，讓作者知道你確實讀了論文
- Strengths 要真誠——即使你要拒稿，也要承認論文的優點
- Weaknesses 要具體——指出具體的段落、公式、實驗
- Questions 要有策略性——能幫助你在 rebuttal 後做決定
- 退稿模式的參考請見 `references/rejection-patterns.md`

---

## 五大審查維度（詳細版）

以下為五大審查維度的摘要。完整說明請參考 `references/review-dimensions.md`。

### 1. 貢獻新穎性 (Novelty & Contribution)

- 這個想法之前有人做過嗎？
- 貢獻的量和質是否足以支撐一篇完整論文？
- 相對於 prior work，增量有多大？
- 是技術新穎、應用新穎，還是視角新穎？

### 2. 寫作清晰度 (Clarity & Writing)

- 非專家能否理解論文的主要貢獻？
- 動機是否清晰？為什麼這個問題重要？
- 符號和術語是否一致？
- 圖表是否清晰且有助理解？

### 3. 實驗嚴謹性 (Experimental Rigor)

- 實驗設計是否足以驗證 claims？
- 是否有適當的 baselines？
- 是否報告了統計顯著性或誤差範圍？
- 超參數選擇是否合理？是否進行了公平比較？

### 4. 評估完整性 (Evaluation Completeness)

- 資料集是否足夠多樣？
- 是否有 ablation study？
- 是否有分析（error analysis、case study）？
- 是否討論了局限性？

### 5. 方法健全性 (Soundness of Method)

- 數學推導是否正確？
- 假設是否合理且被明確陳述？
- 方法是否能如聲稱般運作？
- 是否有理論保證或直覺性解釋？

---

## 五大退稿模式

以下為五大退稿模式的摘要。完整說明與範例請參考 `references/rejection-patterns.md`。

### 模式 1：貢獻不足 (Insufficient Contribution)

- 症狀：增量改進、trivial extension、已知結果的簡單組合
- 典型觸發語：「This is a straightforward extension of [X].」

### 模式 2：不清楚 (Lack of Clarity)

- 症狀：讀不懂、邏輯跳躍、符號混亂、缺少直覺
- 典型觸發語：「The paper is difficult to follow.」

### 模式 3：效果弱 (Weak Results)

- 症狀：改進不顯著、cherry-picked results、缺乏統計測試
- 典型觸發語：「The improvements are marginal and may not be statistically significant.」

### 模式 4：評估不全 (Incomplete Evaluation)

- 症狀：缺少重要 baselines、資料集太少、沒有 ablation
- 典型觸發語：「Key baselines such as [X] are missing.」

### 模式 5：方法有缺 (Flawed Methodology)

- 症狀：數學錯誤、不合理的假設、data leakage、不公平比較
- 典型觸發語：「There appears to be an error in the derivation of Eq. (X).」

---

## 評分體系速查

### Overall Score (1-10)

| 分數 | 含義 | 建議 |
|------|------|------|
| 10 | 頂級論文，可直接接受 | Strong Accept |
| 8-9 | 優秀論文，明顯高於門檻 | Accept |
| 6-7 | 好論文，略高於或在門檻附近 | Weak Accept / Borderline |
| 5 | 在門檻上，有明顯的優缺點 | Borderline |
| 3-4 | 低於門檻，有重大問題 | Weak Reject / Reject |
| 1-2 | 明顯不合格 | Strong Reject |

### Confidence (1-5)

| 分數 | 含義 |
|------|------|
| 5 | 非常確信——我是這個子領域的專家 |
| 4 | 確信——我熟悉這個領域 |
| 3 | 中等——我了解主要概念但非專家 |
| 2 | 不太確信——部分內容超出我的專業 |
| 1 | 不確信——這不是我的領域 |

完整評分標準請參考 `references/scoring-rubric.md`。

---

## 參考資料與模板

### 參考資料
- `references/review-dimensions.md` — 五大審查維度的完整說明
- `references/scoring-rubric.md` — 完整評分標準
- `references/rejection-patterns.md` — 五大退稿模式的詳細說明與範例
- `references/constructive-feedback.md` — 建設性回饋的寫法指南

### 模板
- `templates/review-form.md` — 標準審稿表模板
- `templates/meta-review-form.md` — AC meta-review 模板

### 相關技能
- **paper-writing** skill — 論文寫作技能，可搭配使用進行修改循環（revision cycle）

---

## 使用方式

### 基本使用

```
請幫我審查這篇論文：[貼上論文內容或提供 PDF 路徑]
```

依序執行四個步驟，最終產出英文正式審稿。

### 指定步驟

```
請只執行 Step 1（批判性審查）
請從 Step 3 開始（我已經有前兩步的分析）
```

### 指定會議

```
請以 NeurIPS 2026 的標準審查這篇論文
請以 ACL 2026 的標準審查，特別注意 reproducibility
```

### Meta-review

```
以下是三位 reviewer 的意見，請幫我撰寫 meta-review：
[貼上三份 review]
```

使用 `templates/meta-review-form.md` 模板。

---

## 審稿倫理提醒

1. **保密性**：審稿內容不得洩漏給第三方
2. **利益衝突**：如果你認識作者或與論文有利益關係，應主動迴避
3. **尊重**：即使論文品質不佳，也應以尊重的態度撰寫 review
4. **時效性**：在截止日期前完成審稿是審稿者的責任
5. **一致性**：你的評分應與你的文字評論一致——不要給高分卻寫滿缺點
6. **建設性**：審稿的最終目的是幫助作者改進論文，而非炫耀自己的知識

---

## 常見問題

### Q：如果我不確定某個缺點是否正確怎麼辦？

寫在 Questions for Authors 中，讓作者在 rebuttal 中回應。不確定的批評不應作為拒稿的主要理由。

### Q：如何處理 borderline 的論文？

仔細衡量優缺點的相對權重。如果優點明確且重大，而缺點可以在 camera-ready 中修復，傾向接受。如果核心方法有問題，傾向拒稿。

### Q：meta-review 和 individual review 有什麼不同？

Meta-review 需要綜合所有 reviewer 的意見，找出共識與分歧，並做出最終建議。AC 需要判斷哪些 reviewer 的意見更有價值，以及 rebuttal 是否有效回應了主要問題。

### Q：如何與 paper-writing 技能搭配使用？

在完成審稿後，可以將 review 中的建議傳遞給 **paper-writing** skill，指導作者進行修改。這形成了一個「審稿 -> 修改 -> 再審」的循環。
