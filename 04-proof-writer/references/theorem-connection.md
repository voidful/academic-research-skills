# 定理連結方法

本文件說明如何從已知定理推導新結果、常用定理清單（按領域分類），以及引用和連結
定理的規範。

---

## 定理連結的基本思路

### 什麼是定理連結？

定理連結是指在證明新結果時，識別並利用已有的定理作為中間步驟或基礎工具。一個好
的證明通常是「站在巨人的肩膀上」——善用已知結果，只推導真正新的部分。

### 連結流程

1. **分解主張**：將要證明的主張分解為多個子問題。
2. **匹配已知結果**：對每個子問題，搜索可用的已知定理。
3. **驗證前提**：確認已知定理的前提條件在當前語境下成立。
4. **填補空隙**：對已知定理無法覆蓋的部分，進行原創推導。
5. **組合結果**：將所有部分組合成完整的證明。

### 連結策略

#### 策略一：直接引用

最簡單的連結方式。當已知定理可以直接應用時：

```latex
By Theorem~\ref{thm:known-result}, we have [conclusion].
```

**前提**：已知定理的所有前提條件在當前語境下都滿足。

#### 策略二：特化 (Specialization)

將一般性定理應用到特殊情況：

```latex
Applying Theorem~\ref{thm:general} with $X = [specific choice]$
and $Y = [specific choice]$, we obtain [specific conclusion].
```

**適用**：當已知定理比需要的更一般時。

#### 策略三：推廣 (Generalization)

證明已知定理的推廣版本。通常需要修改原始證明：

```latex
The proof follows the same strategy as [Reference], with the
following modifications: ...
```

**適用**：當已知定理幾乎但不完全適用時。

#### 策略四：組合 (Combination)

將多個定理的結論組合起來：

```latex
Combining Lemma~\ref{lem:A} and Lemma~\ref{lem:B}, we obtain ...
```

**適用**：當沒有單一定理足以完成證明，但多個定理的結合可以時。

#### 策略五：鏈式推導 (Chaining)

將多個定理串聯成推導鏈：

```latex
By Theorem A, we have [result 1]. Applying Theorem B to [result 1],
we obtain [result 2]. Finally, Theorem C yields [conclusion].
```

**適用**：證明需要經過多個中間步驟時。

---

## 常用定理清單

### 分析 (Analysis)

| 定理 | 陳述摘要 | 常見用途 |
|------|---------|---------|
| Cauchy-Schwarz inequality | $|\langle x, y \rangle| \leq \|x\| \cdot \|y\|$ | 內積估計、上界推導 |
| Triangle inequality | $\|x + y\| \leq \|x\| + \|y\|$ | 距離估計 |
| Jensen's inequality | $f(\mathbb{E}[X]) \leq \mathbb{E}[f(X)]$ for convex $f$ | 凸函數、期望值界 |
| Hölder's inequality | $\|fg\|_1 \leq \|f\|_p \|g\|_q$ where $1/p+1/q=1$ | $L^p$ 空間估計 |
| Minkowski's inequality | $\|f+g\|_p \leq \|f\|_p + \|g\|_p$ | 範數的三角不等式 |
| Mean Value Theorem | $f(b)-f(a) = f'(c)(b-a)$ | 差值估計 |
| Taylor's theorem | $f(x) = \sum_{k=0}^n \frac{f^{(k)}(a)}{k!}(x-a)^k + R_n$ | 近似與誤差界 |
| Dominated Convergence | 控制收斂定理 | 交換極限與積分 |
| Monotone Convergence | 單調收斂定理 | 非負函數序列積分 |

### 機率論 (Probability Theory)

| 定理 | 陳述摘要 | 常見用途 |
|------|---------|---------|
| Markov's inequality | $\Pr[X \geq a] \leq \mathbb{E}[X]/a$ | 基本尾界 |
| Chebyshev's inequality | $\Pr[|X-\mu| \geq k\sigma] \leq 1/k^2$ | 方差尾界 |
| Hoeffding's inequality | 有界隨機變數和的集中不等式 | 有限樣本界 |
| Bernstein's inequality | 考慮方差的集中不等式 | 更緊的集中界 |
| Chernoff bound | 矩生成函數尾界 | 指數型集中 |
| Central Limit Theorem | $\bar{X}_n \xrightarrow{d} N(\mu, \sigma^2/n)$ | 漸近分析 |
| Law of Large Numbers | $\bar{X}_n \xrightarrow{a.s.} \mu$ | 一致性證明 |
| Borel-Cantelli lemma | 事件發生無限次的條件 | 幾乎必然收斂 |
| Union bound | $\Pr[\bigcup A_i] \leq \sum \Pr[A_i]$ | 多事件機率上界 |
| McDiarmid's inequality | 有界差分函數的集中 | 函數集中不等式 |

### 線性代數 (Linear Algebra)

| 定理 | 陳述摘要 | 常見用途 |
|------|---------|---------|
| Spectral theorem | 對稱矩陣的正交分解 | 矩陣分析 |
| Singular Value Decomposition | $A = U\Sigma V^T$ | 矩陣近似、降維 |
| Rank-nullity theorem | $\mathrm{rank}(A) + \mathrm{null}(A) = n$ | 線性系統分析 |
| Perron-Frobenius theorem | 非負矩陣的主特徵值 | 馬可夫鏈 |
| Matrix inversion lemma | $(A + UCV)^{-1}$ 的展開 | 高效計算 |
| Courant-Fischer theorem | 特徵值的 min-max 表示 | 特徵值界 |
| Weyl's inequality | 特徵值擾動界 | 擾動分析 |

### 最佳化 (Optimization)

| 定理 | 陳述摘要 | 常見用途 |
|------|---------|---------|
| KKT conditions | 凸最佳化的最優性條件 | 最優解刻畫 |
| Strong duality | 凸問題的零對偶間隙 | 對偶方法 |
| Gradient descent convergence | 凸且 Lipschitz 梯度下的收斂率 | 演算法分析 |
| Minimax theorem | $\min_x \max_y = \max_y \min_x$ (凸-凹) | 對抗訓練、博弈論 |
| Projection theorem | 閉凸集上的最近點唯一存在 | 凸約束問題 |
| Slater's condition | 強對偶性的充分條件 | 驗證強對偶 |

### 機器學習理論 (Learning Theory)

| 定理 | 陳述摘要 | 常見用途 |
|------|---------|---------|
| VC dimension bound | $\epsilon$-net 與 VC 維的樣本界 | 泛化界 |
| Rademacher complexity bound | 基於 Rademacher 複雜度的泛化界 | 泛化分析 |
| PAC-Bayes bound | 後驗加權假設的泛化界 | 貝式學習 |
| No Free Lunch theorem | 無通用最優演算法 | 理論限制 |
| Bias-variance decomposition | 期望誤差分解 | 模型選擇 |
| Fano's inequality | 互資訊與錯誤率的關係 | minimax 下界 |
| Le Cam's method | 兩假設測試下界 | 估計下界 |
| Assouad's lemma | 多假設測試下界 | 高維估計下界 |

### 資訊論 (Information Theory)

| 定理 | 陳述摘要 | 常見用途 |
|------|---------|---------|
| Shannon's source coding | 無損壓縮的極限為 $H(X)$ | 壓縮界 |
| Channel coding theorem | 通訊率可達 $C = \max I(X;Y)$ | 容量界 |
| Data processing inequality | $I(X;Z) \leq I(X;Y)$ for $X \to Y \to Z$ | 資訊損失 |
| Entropy power inequality | $N(X+Y) \geq N(X) + N(Y)$ | 容量界 |
| Mrs. Gerber's lemma | BSC 組合的熵界 | 二元通道 |
| Pinsker's inequality | TV 距離與 KL 散度的關係 | 分布距離 |
| Gibbs' inequality | $D_{\mathrm{KL}}(P \| Q) \geq 0$ | KL 非負性 |

---

## 引用與連結規範

### 引用格式

#### 引用論文自身的結果

```latex
% 引用同一篇論文中的定理
By Theorem~\ref{thm:our-main-result}, ...
As shown in Lemma~\ref{lem:auxiliary}, ...
From Equation~\eqref{eq:key-bound}, ...
```

#### 引用外部文獻

```latex
% 引用其他論文的結果
By \cite[Theorem~3.2]{author2024paper}, ...
Following the approach of \cite{author2023}, ...
Using the result of \citet{author2022} (specifically, their Theorem~5), ...
```

#### 引用經典結果

```latex
% 眾所周知的結果可不引用具體文獻
By the Cauchy-Schwarz inequality, ...
By Jensen's inequality, ...
% 但較不常見的結果應提供引用
By the Lovász Local Lemma (see, e.g., \cite[Chapter~5]{alon2016book}), ...
```

### 引用的完整性原則

1. **自明結果**：眾所周知的基本定理（如 Cauchy-Schwarz）可不附引用。
2. **標準結果**：領域內廣為人知的結果，附上經典教科書引用。
3. **近期結果**：近年發表的結果，必須附上原始論文引用。
4. **本文結果**：引用本文前面已證明的引理或命題。

### 連結的視覺化

在複雜的證明中，建議在證明開始前提供推導結構的概覽：

```latex
\begin{remark}[Proof outline]
  The proof proceeds in three steps. First, we establish [A]
  using Lemma~\ref{lem:step1}. Then, combining [A] with
  Theorem~\ref{thm:known}, we derive [B]. Finally, we apply
  [B] to obtain the main result.
\end{remark}
```

### 定理依賴圖

對於包含多個引理和定理的論文，維護一個心理上的（或實際的）依賴圖：

```
Lemma 1 ──┐
           ├──→ Theorem 1 ──┐
Lemma 2 ──┘                 │
                             ├──→ Main Theorem
Lemma 3 ──→ Theorem 2 ──────┘
```

確保依賴關係是有向無環的 (DAG)，且陳述順序與依賴順序一致。
