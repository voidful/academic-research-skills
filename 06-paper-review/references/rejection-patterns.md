# 五大退稿模式：詳細說明與範例

本文件詳細說明學術論文審稿中最常見的五大退稿模式，包含常見症狀、範例情境以及如何在審稿中恰當地指出這些問題。

---

## 模式 1：貢獻不足 (Insufficient Contribution)

### 定義

論文所提出的想法或方法缺乏足夠的新穎性或貢獻度，不足以構成一篇獨立的學術論文。

### 常見症狀

1. **增量改進**：只是在已有方法上做了微小的修改（如換一個 loss function、加一個 layer）
2. **Trivial 延伸**：將 A 方法直接搬到 B 問題上，沒有新的技術挑戰
3. **已知結果的簡單組合**：將兩個已有方法拼在一起，沒有新的洞見
4. **工程改進而非研究貢獻**：主要是調參或 tricks 的堆疊
5. **與 concurrent work 高度重疊**：獨立發展但貢獻被搶先

### 範例情境

**情境 A：增量改進**
> 一篇論文聲稱提出了「新的」注意力機制，但仔細一看只是把 dot-product attention 改成 cosine similarity attention，沒有理論解釋也沒有顯著的實驗改進。

**情境 B：簡單搬移**
> 一篇論文把 NLP 中已經很成熟的 pre-training + fine-tuning 範式搬到一個新的小領域，方法完全一樣，只是換了資料集，且沒有遇到任何新的技術挑戰。

**情境 C：結果組合**
> 一篇論文同時使用 data augmentation + knowledge distillation + label smoothing，每個技術都是已知的，組合也是直覺上顯然的，且沒有分析為什麼這個組合特別有效。

### 如何在審稿中指出

**推薦的表述方式：**

- 「The contribution appears to be incremental over [prior work X]. The key differences are [A, B], but these modifications seem straightforward and do not present significant technical challenges.」
- 「While the application domain is new, the methodology closely follows [X] without addressing domain-specific challenges. It would strengthen the paper to identify and tackle unique challenges in this setting.」
- 「The paper combines several known techniques ([A], [B], [C]). While the combination achieves good results, the paper would benefit from a deeper analysis of why this particular combination is effective and when it might fail.」

**避免的表述方式：**

- 「This paper has no contribution.」（過於絕對）
- 「This is just [X] with a minor tweak.」（過於輕蔑）
- 「Anyone could have done this.」（對人不對事）

---

## 模式 2：不清楚 (Lack of Clarity)

### 定義

論文的表達不清楚，導致審稿者（以及預期讀者）無法理解論文的主要貢獻、方法或結果。

### 常見症狀

1. **讀不懂**：多次閱讀後仍不確定論文在說什麼
2. **邏輯跳躍**：從問題到方法的推導有不合理的跳躍
3. **符號混亂**：同一個符號在不同地方代表不同意思，或符號未定義
4. **缺少直覺**：有公式但沒有解釋為什麼這樣設計
5. **結構混亂**：資訊出現的順序不合理，讀者需要反覆翻閱

### 範例情境

**情境 A：符號災難**
> 論文在 Section 3 定義了 $f_\theta$，在 Section 4 用 $f$ 表示同一個東西，然後在 Section 5 又用 $f$ 表示另一個函數。

**情境 B：動機缺失**
> 論文直接跳到方法描述，從未解釋為什麼現有方法不足、為什麼需要新方法、新方法解決了什麼現有方法解決不了的問題。

**情境 C：資訊流混亂**
> 論文在實驗部分引入了方法中未提到的重要設計決定（如特殊的 data preprocessing），而方法部分的某些細節要到附錄才能找到。

### 如何在審稿中指出

**推薦的表述方式：**

- 「The paper is difficult to follow in its current form. In particular, [specific section/paragraph] requires significant clarification. For instance, [specific example of unclear writing].」
- 「The notation is inconsistent — $f_\theta$ in Section 3 appears to refer to a different entity than $f$ in Section 5. I suggest the authors unify the notation throughout.」
- 「The motivation for the proposed approach is not clearly articulated. It would help to explicitly discuss the limitations of existing methods (e.g., [X, Y]) and how the proposed method addresses them.」

**避免的表述方式：**

- 「This paper is poorly written.」（太籠統，不指出具體問題）
- 「I cannot understand anything.」（可能是審稿者的問題而非論文的問題）

---

## 模式 3：效果弱 (Weak Results)

### 定義

論文聲稱的改進不顯著、不可靠，或實驗結果不足以支持論文的核心 claims。

### 常見症狀

1. **改進不顯著**：相對於 baselines 只有微小的改進，可能在誤差範圍內
2. **Cherry-picked results**：只展示方法表現好的情況，隱藏表現差的
3. **缺乏統計測試**：沒有報告標準差或統計顯著性
4. **與 claims 不匹配**：論文聲稱大幅改進，但數字顯示改進很小
5. **不一致的結果**：在某些資料集上好，在另一些上不好，且沒有解釋

### 範例情境

**情境 A：統計不顯著**
> 論文聲稱在三個資料集上都取得了 SOTA，但改進幅度分別為 0.1%、0.3%、0.2%，且沒有報告標準差或 p-value。

**情境 B：選擇性報告**
> 論文在 6 個資料集中的 4 個上取得改進，但隻字未提在另外 2 個上表現更差。審稿者從附錄的表格中發現了這一點。

**情境 C：Claims 過度**
> 摘要聲稱「significantly outperforms all existing methods」，但主表格顯示只在特定設定下略好，在其他設定下與 baselines 持平或更差。

### 如何在審稿中指出

**推薦的表述方式：**

- 「The improvements over [baseline X] are marginal (e.g., 0.2% on Dataset A). Without statistical significance tests (e.g., paired t-test, bootstrap), it is unclear whether these improvements are meaningful.」
- 「I notice that the results on Datasets E and F (Appendix Table X) show degraded performance compared to the baseline. It would be important to discuss these cases and analyze when the method underperforms.」
- 「The claim in the abstract that the method 'significantly outperforms all existing methods' does not appear to be fully supported by the experimental results, particularly on [specific benchmarks].」

**避免的表述方式：**

- 「The results are not impressive.」（主觀且不具體）
- 「The authors are cherry-picking.」（指控動機，而非指出事實）

---

## 模式 4：評估不全 (Incomplete Evaluation)

### 定義

論文的實驗評估不夠全面，缺少驗證其 claims 所必需的關鍵實驗、比較或分析。

### 常見症狀

1. **缺少重要 baselines**：遺漏了該領域最新或最相關的對比方法
2. **資料集太少**：只在一兩個資料集上實驗，無法驗證泛化性
3. **沒有 ablation study**：方法有多個組件但不知道每個組件的貢獻
4. **缺少分析**：只有數字沒有洞見，不知道方法為什麼有效或何時失效
5. **遺漏的評估指標**：只報告對自己有利的指標

### 範例情境

**情境 A：缺少 SOTA baseline**
> 一篇 2026 年的論文比較的最新 baseline 是 2023 年的方法，忽略了 2024-2025 年間發表的多個更強的方法。

**情境 B：缺少 ablation**
> 論文提出了一個包含三個新組件的方法（新 loss、新 architecture、新 training strategy），但只報告了完整方法的結果，沒有分析每個組件的貢獻。

**情境 C：單一資料集**
> 論文聲稱方法具有廣泛的適用性，但只在一個資料集上進行了實驗。

**情境 D：遺漏指標**
> 一篇生成模型的論文只報告 FID score，沒有報告 diversity metrics（如 recall、coverage），而論文的方法可能犧牲了多樣性來換取品質。

### 如何在審稿中指出

**推薦的表述方式：**

- 「Several important baselines are missing from the comparison, notably [X] (ICML 2025) and [Y] (NeurIPS 2025), which are directly relevant and have shown strong performance on the same benchmarks.」
- 「The paper would be significantly strengthened by an ablation study that isolates the contribution of each proposed component (the new loss, the architectural modification, and the training strategy).」
- 「Given the claim of broad applicability, evaluating on additional datasets from different domains (e.g., [specific suggestions]) would be necessary to support this claim.」
- 「Reporting only [metric A] may give an incomplete picture. I would suggest also reporting [metric B] and [metric C], which capture [aspect] that [metric A] does not.」

**避免的表述方式：**

- 「The experiments are insufficient.」（不指出缺少什麼）
- 「The authors should run more experiments.」（不具體說明哪些實驗）

---

## 模式 5：方法有缺 (Flawed Methodology)

### 定義

論文所提出的方法在技術層面有錯誤、不合理的假設，或存在根本性的方法論問題。

### 常見症狀

1. **數學錯誤**：推導中有計算錯誤或邏輯錯誤
2. **不合理的假設**：方法依賴於在實際場景中不成立的假設
3. **Data leakage**：測試集的資訊洩漏到了訓練過程中
4. **不公平比較**：自己的方法使用了 baselines 沒有使用的額外資訊或資源
5. **忽略了已知的限制**：使用了已被證明在某些條件下失效的技術而未討論

### 範例情境

**情境 A：數學錯誤**
> 論文在推導 Theorem 1 時，第三步的不等式方向反了。將 $\leq$ 改為 $\geq$ 後，整個定理的結論都需要改變。

**情境 B：Data leakage**
> 論文在 feature engineering 階段使用了整個資料集（包括測試集）的統計資訊來做 normalization，導致測試集的資訊洩漏到了模型中。

**情境 C：不公平比較**
> 論文的方法使用了額外的未標記資料進行 pre-training，但所有 baselines 都只使用標記資料。在不考慮這個差異的情況下直接比較數字是不公平的。

**情境 D：隱含假設**
> 論文的方法假設資料是 i.i.d. 的，但實際應用場景（如時間序列或社交網路）明顯違反了這個假設，論文未討論此問題。

### 如何在審稿中指出

**推薦的表述方式：**

- 「I believe there may be an error in the derivation of Theorem 1. Specifically, in Eq. (5), the inequality should be reversed because [reason]. This would affect the main conclusion.」
- 「There appears to be a potential data leakage issue: the normalization in Section 3.2 uses statistics computed over the entire dataset including the test set. This could inflate the reported performance.」
- 「The comparison may not be entirely fair, as the proposed method uses additional unlabeled data for pre-training (Section 3.1) while the baselines do not. I would suggest either (a) providing baselines with the same pre-training data, or (b) clearly discussing this advantage.」
- 「The i.i.d. assumption (stated in Section 2) may not hold in the target application. It would be valuable to discuss the implications of violating this assumption and to test the method under non-i.i.d. conditions.」

**避免的表述方式：**

- 「The math is wrong.」（不具體指出哪裡錯了）
- 「The authors cheated by using test data.」（指控意圖而非陳述觀察）
- 「This method cannot work.」（過於絕對且不提供理由）

---

## 退稿模式的組合

一篇論文通常不會只觸發一個退稿模式。常見的組合包括：

### 致命組合

- **貢獻不足 + 效果弱**：沒什麼新意，結果也不好 -> 幾乎確定被拒
- **方法有缺 + 效果弱**：方法有問題且結果不佳 -> 強烈拒稿
- **不清楚 + 方法有缺**：看不懂，而且看懂的部分有錯 -> 強烈拒稿

### 可救組合

- **貢獻好但寫不清楚**：核心想法有價值但需要重寫 -> borderline，視 rebuttal 而定
- **方法健全但評估不全**：技術上正確但需要更多實驗 -> borderline，可以補做實驗
- **效果好但貢獻定位不清**：結果不錯但沒有解釋清楚為什麼 -> 可以在 rebuttal 中改善

### 審稿時的考量

- 觸發一個致命模式（如方法有根本性錯誤）通常就足以構成拒稿理由
- 觸發兩個以上的非致命模式（如貢獻不足 + 評估不全）加起來也可能構成拒稿
- 即使觸發了某個模式，如果論文在其他維度極其出色，仍需綜合考量
