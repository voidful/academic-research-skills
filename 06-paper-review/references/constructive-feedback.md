# 建設性回饋寫法指南

本文件提供撰寫建設性學術審稿回饋的指南，包含如何批評而不傷人、具體與模糊回饋的對比，以及建議修改方向的模板。

---

## 核心原則

### 1. 對事不對人

審稿評論的對象是論文，而非作者。

| 對人（避免） | 對事（推薦） |
|-------------|-------------|
| 「The authors failed to...」 | 「The paper does not address...」 |
| 「The authors clearly don't understand...」 | 「The connection to [X] is not discussed...」 |
| 「The authors are lazy about...」 | 「Additional experiments on [X] would strengthen...」 |
| 「The authors made a mistake in...」 | 「There appears to be an issue with Eq. (3)...」 |

### 2. 指出問題的同時提供方向

每個 weakness 都應附帶改進建議，即使只是方向性的。

**只指出問題（不完整）：**
> The paper lacks ablation studies.

**指出問題並提供方向（完整）：**
> The paper would benefit from ablation studies that isolate the contribution of each component. Specifically, comparing (1) the full model, (2) without the attention module, and (3) without the contrastive loss would help readers understand the importance of each design choice.

### 3. 使用緩和語氣

學術審稿有一套約定俗成的緩和語氣（hedging language）。

| 直接（可能顯得攻擊性） | 緩和（專業而友善） |
|----------------------|-------------------|
| 「This is wrong.」 | 「I believe there may be an issue with...」 |
| 「This doesn't work.」 | 「It is unclear whether this approach would generalize to...」 |
| 「This is trivial.」 | 「The contribution relative to [prior work] appears to be incremental.」 |
| 「The experiments are bad.」 | 「The experimental evaluation could be strengthened by...」 |

### 4. 承認不確定性

如果你不確定某個批評是否正確，要明確表達。

**好的做法：**
> I may be missing something, but it seems that Eq. (5) assumes independence between X and Y, which may not hold in practice. If this assumption is indeed required, it would be helpful to discuss its implications.

**不好的做法：**
> Eq. (5) is wrong because X and Y are not independent.

---

## 具體 vs 模糊回饋的對比

### 貢獻相關

| 模糊（避免） | 具體（推薦） |
|-------------|-------------|
| 「The novelty is limited.」 | 「The main difference from [X] appears to be the use of [specific technique]. It would help to clarify why this modification is non-trivial and what challenges it addresses.」 |
| 「The contribution is not enough.」 | 「The paper presents [A] as a contribution, but [similar work Y] has explored a very similar idea. The paper would benefit from a detailed comparison with [Y] to highlight the unique aspects.」 |

### 寫作相關

| 模糊（避免） | 具體（推薦） |
|-------------|-------------|
| 「The writing needs improvement.」 | 「Section 3.2 is difficult to follow. Specifically, the transition from Eq. (3) to Eq. (4) requires additional explanation of why [specific step] is valid.」 |
| 「The paper is hard to read.」 | 「The notation is inconsistent: $h$ denotes hidden states in Section 3 but is overloaded to mean hypothesis in Section 4. Using distinct symbols would improve readability.」 |

### 實驗相關

| 模糊（避免） | 具體（推薦） |
|-------------|-------------|
| 「More experiments are needed.」 | 「Evaluating on [specific dataset] would test the method under [specific condition] and strengthen the generalization claim.」 |
| 「The baselines are outdated.」 | 「Recent methods such as [X] (ICML 2025) and [Y] (NeurIPS 2025) have achieved strong results on the same benchmarks and should be included for a fair comparison.」 |

### 方法相關

| 模糊（避免） | 具體（推薦） |
|-------------|-------------|
| 「The method has issues.」 | 「The optimization objective in Eq. (7) is non-convex, and the paper does not discuss convergence guarantees. Empirically demonstrating convergence (e.g., plotting the loss curve) would address this concern.」 |
| 「The assumptions are unrealistic.」 | 「Assumption 2 requires [specific condition], which is typically violated in [specific practical scenario]. Relaxing this assumption or empirically testing performance under violation would strengthen the work.」 |

---

## 審稿常用句型模板

### 表達優點

- 「A strength of this paper is [X], which [why it's good].」
- 「The paper makes a valuable contribution by [X].」
- 「I appreciate the thoroughness of [specific aspect].」
- 「The experimental setup is well-designed, particularly [specific aspect].」
- 「The writing is clear and the paper is easy to follow.」
- 「The problem addressed is important and timely.」

### 表達缺點（建設性）

- 「A concern is [X]. This could be addressed by [suggestion].」
- 「The paper would benefit from [X] to strengthen the [specific claim].」
- 「It is unclear [what/why/how]. Additional clarification would help.」
- 「One potential issue is [X]. It would be helpful to [suggestion].」
- 「While the approach is interesting, [X] raises a concern about [Y].」

### 提出問題

- 「Could the authors clarify [specific point]?」
- 「How does the method perform when [specific condition]?」
- 「What happens if [assumption] is violated?」
- 「Is there a reason why [specific baseline/dataset/metric] was not included?」
- 「How sensitive is the method to [specific hyperparameter]?」

### 提供建議

- 「I would suggest [specific action] to address this concern.」
- 「One way to strengthen this section would be to [specific suggestion].」
- 「Including [specific experiment/analysis] would help validate [specific claim].」
- 「The paper could be improved by [specific writing suggestion].」

### 表達不確定性

- 「I may be mistaken, but it appears that...」
- 「Unless I am missing something, [observation]...」
- 「If I understand correctly, [interpretation]. If so, [concern].」
- 「This is outside my core expertise, but [observation].」

---

## 不同情境的回饋策略

### 情境 1：你要拒稿但論文有可取之處

**策略**：先真誠地肯定優點，再具體說明問題，最後提供改進方向。

**範例：**
> The paper addresses an important problem and proposes an interesting approach. The idea of [X] is creative and the theoretical framework is well-motivated.
>
> However, I have several concerns that prevent me from recommending acceptance at this time:
>
> 1. [Major concern 1 + suggestion]
> 2. [Major concern 2 + suggestion]
>
> I believe this work has potential, and I encourage the authors to address these issues and resubmit.

### 情境 2：你要接受但論文有瑕疵

**策略**：清楚標註哪些是必須修改的，哪些是建議性的。

**範例：**
> Overall, this is a solid paper with a clear contribution. I recommend acceptance with the following revisions:
>
> **Required revisions (for camera-ready):**
> 1. [Issue that must be fixed]
>
> **Suggested improvements (optional but recommended):**
> 1. [Improvement that would make the paper stronger]

### 情境 3：你不確定方法是否正確

**策略**：描述你的理解，指出你疑惑的地方，用問句而非斷言。

**範例：**
> If I understand correctly, the proof of Theorem 2 relies on the assumption that [X]. However, in the experimental setting described in Section 5, it seems that [Y] might not hold. Could the authors clarify whether the theorem still applies in this case? If not, how does this affect the practical guarantees?

### 情境 4：論文品質很差

**策略**：即使論文品質不佳，也保持專業和尊重。指出最核心的幾個問題，不需要列出所有小問題。

**範例：**
> The paper attempts to address [problem], which is a relevant topic. However, there are several fundamental issues that need to be addressed before the paper is ready for publication:
>
> 1. [Most critical issue + why it matters + suggestion]
> 2. [Second critical issue + suggestion]
>
> I recommend the authors focus on addressing these core issues. Once the fundamental concerns are resolved, additional refinements in [writing/experiments] would also be beneficial.

---

## 回饋的結構化原則

### STAR 框架

對每個重要的回饋點，考慮使用以下結構：

- **S**ituation（情境）：指出論文中的具體位置
- **T**opic（主題）：說明你要評論什麼
- **A**ssessment（評估）：你的判斷是什麼
- **R**ecommendation（建議）：你建議怎麼改

**範例：**
> In Section 4.2 (Situation), the paper claims that the method achieves real-time performance (Topic). However, the reported inference time of 200ms per frame suggests this may not meet the common real-time threshold of 30 FPS (Assessment). I would suggest either adjusting the claim or providing optimization strategies that could bring the latency below 33ms (Recommendation).

### 優先級標記

在正式 review 中，區分不同重要性的回饋：

- **[Major]**：影響接受與否的重大問題
- **[Minor]**：不影響接受但建議改進的問題
- **[Nit]**：格式、typo 等極小的問題
- **[Question]**：需要作者回答的問題

---

## 審稿者常犯的錯誤

### 1. 只批評不肯定

即使是要被拒的論文，也值得被承認其優點。如果你找不到任何優點，可能是你沒有認真讀。

### 2. 要求作者做不可能的事

如「please compare with all existing methods」或「please prove that the method works in all cases」。要求應該是合理且具體的。

### 3. 把自己的研究方向強加於作者

「The paper should also consider [my favorite topic]」——除非真的相關，否則不要把自己的研究偏好當成論文的缺點。

### 4. 字數太少

「Reject. The paper is not good enough.」——這種 review 對作者毫無幫助，也不配被當作拒稿理由。

### 5. 前後矛盾

文字評論全是缺點但給了高分，或者文字評論很正面但給了低分。評分應與文字一致。

---

## 文化敏感度提醒

- 不要根據作者的英文寫作品質推測其國籍或能力
- 不要因為論文使用了非標準的術語就認為作者不專業——可能是不同社群的用法
- 對於英文非母語的作者，區分「語言問題」和「邏輯問題」——前者可以修正，後者才是核心問題
- 保持客觀，不要因為作者來自知名機構就給予優待，也不要因為來自不知名機構就更嚴格
