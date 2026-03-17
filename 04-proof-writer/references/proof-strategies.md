# 證明策略參考

本文件詳細說明八種核心證明策略。每種策略包含定義、適用場景、模板結構、常見錯誤
與範例。

---

## 1. 直接證明 (Direct Proof)

### 定義

從前提條件出發，通過一系列有效的邏輯推導步驟，直接推導出結論。這是最基本也最
常見的證明方法。

### 適用場景

- 等式的建立（如 $A = B$，通過一系列等式變換）
- 不等式的推導（如利用已知不等式逐步放縮）
- 集合包含關係（$A \subseteq B$，取任意 $x \in A$ 證明 $x \in B$）
- 函數性質的驗證（連續性、可微性等）
- 結構較為明確、推導路徑清晰的命題

### 模板結構

```latex
\begin{proof}
  Let $x$ satisfy the given conditions.
  % Step 1: Starting point
  By assumption, we have ...
  % Step 2: Key derivation
  Applying [Theorem/Lemma], it follows that ...
  % Step 3: Intermediate result
  Combining the above, we obtain ...
  % Step 4: Conclusion
  Therefore, the desired result holds. \qed
\end{proof}
```

### 常見錯誤

1. **跳躍推導**：省略了中間步驟，讀者無法理解如何從上一步推到下一步。
   解決方法：每次推導幅度不要超過一個定理的應用。
2. **循環論證**：在推導過程中隱含地使用了結論。
   解決方法：列出推導鏈，確認每一步只依賴前提或之前的結果。
3. **條件不足**：使用了未在前提中聲明的條件。
   解決方法：推導前列出所有可用的前提條件。
4. **方向錯誤**：證明 $A \Rightarrow B$ 時，實際上證明了 $B \Rightarrow A$。
   解決方法：始終明確推導方向。

### 範例

**主張**：若 $a$ 和 $b$ 為正實數，則 $\frac{a+b}{2} \geq \sqrt{ab}$（AM-GM 不等式）。

```latex
\begin{proof}
  Since $a, b > 0$, we have $(\sqrt{a} - \sqrt{b})^2 \geq 0$.
  Expanding, we get $a - 2\sqrt{ab} + b \geq 0$, which implies
  $a + b \geq 2\sqrt{ab}$. Dividing both sides by $2$ yields
  \[
    \frac{a+b}{2} \geq \sqrt{ab}.
  \]
  \qed
\end{proof}
```

---

## 2. 反證法 (Proof by Contradiction)

### 定義

假設結論不成立（即假設結論的否定為真），然後推導出與已知事實或前提條件相矛盾的
結果，從而否定假設，確立結論的正確性。

### 適用場景

- 唯一性證明（假設存在兩個不同的解）
- 不存在性證明（假設存在，推導矛盾）
- 無理數證明（如 $\sqrt{2}$ 的無理性）
- 直接證明路徑不明確時的替代方案
- 結論為否定形式的命題（「不存在」、「不可能」）

### 模板結構

```latex
\begin{proof}
  Suppose, for the sake of contradiction, that [negation of conclusion].
  % Step 1: Derive consequences
  Then, it follows that ...
  % Step 2: Reach contradiction
  However, this contradicts [known fact / assumption].
  % Step 3: Conclude
  Therefore, our assumption is false, and the original
  statement holds. \qed
\end{proof}
```

### 常見錯誤

1. **否定不正確**：未正確取結論的否定。例如 $\forall x, P(x)$ 的否定是
   $\exists x, \neg P(x)$，而非 $\forall x, \neg P(x)$。
   解決方法：仔細處理量詞的否定。
2. **矛盾不成立**：推導出的「矛盾」實際上並不矛盾。
   解決方法：明確指出矛盾的兩個互相否定的命題。
3. **多餘的反證**：本可以直接證明卻使用反證法，增加不必要的複雜度。
   解決方法：先嘗試直接證明，直接證明困難時再考慮反證法。
4. **假設遺失**：反證假設中沒有用到所有必要的前提。
   解決方法：確認反證假設與所有前提條件結合後才能推出矛盾。

### 範例

**主張**：$\sqrt{2}$ is irrational。

```latex
\begin{proof}
  Suppose, for the sake of contradiction, that $\sqrt{2}$ is rational.
  Then there exist integers $p$ and $q$ with $q \neq 0$ and
  $\gcd(p, q) = 1$ such that $\sqrt{2} = p/q$. Squaring both sides,
  we get $2 = p^2 / q^2$, i.e., $p^2 = 2q^2$. This implies $p^2$ is
  even, and hence $p$ is even. Write $p = 2k$ for some integer $k$.
  Then $4k^2 = 2q^2$, so $q^2 = 2k^2$, which implies $q$ is also even.
  But this contradicts $\gcd(p, q) = 1$. Therefore, $\sqrt{2}$ is
  irrational. \qed
\end{proof}
```

---

## 3. 數學歸納法 (Mathematical Induction)

### 定義

證明一個依賴自然數（或可良序化的結構）的命題 $P(n)$ 對所有 $n \geq n_0$ 成立。
需要證明基底步驟 (base case) 和歸納步驟 (inductive step)。

### 變體

- **弱歸納**：假設 $P(k)$ 成立，證明 $P(k+1)$。
- **強歸納**：假設對所有 $n_0 \leq j \leq k$ 都有 $P(j)$ 成立，證明 $P(k+1)$。
- **結構歸納**：對遞迴定義的結構進行歸納（如樹、表達式）。
- **超限歸納**：對任意良序集進行歸納。

### 適用場景

- 遞迴定義的序列性質
- 離散數學中的求和公式
- 數據結構的性質（樹的高度、節點數等）
- 演算法正確性的歸納證明
- 任何與自然數或遞迴結構相關的命題

### 模板結構

```latex
\begin{proof}
  We proceed by induction on $n$.

  \textbf{Base case} ($n = n_0$):
  [Verify P(n_0) holds directly.]

  \textbf{Inductive step}:
  Assume $P(k)$ holds for some $k \geq n_0$ (inductive hypothesis).
  We need to show $P(k+1)$.
  [Derivation using the inductive hypothesis.]
  This establishes $P(k+1)$.

  By the principle of mathematical induction, $P(n)$ holds for
  all $n \geq n_0$. \qed
\end{proof}
```

### 常見錯誤

1. **忘記基底步驟**：直接進入歸納步驟而未驗證基底情況。
   解決方法：始終先寫基底步驟。
2. **歸納假設未使用**：歸納步驟中沒有用到歸納假設，通常表示不需要歸納法。
   解決方法：確認推導中確實使用了 $P(k)$。
3. **基底不正確**：基底步驟的 $n_0$ 選擇不當。
   解決方法：確認命題在最小的 $n$ 上成立。
4. **歸納步驟的方向**：應證明 $P(k) \Rightarrow P(k+1)$，而非反向。
   解決方法：始終從 $P(k)$ 出發推導 $P(k+1)$。

### 範例

**主張**：For all $n \geq 1$, $\sum_{i=1}^{n} i = \frac{n(n+1)}{2}$。

```latex
\begin{proof}
  We proceed by induction on $n$.

  \textbf{Base case} ($n = 1$):
  $\sum_{i=1}^{1} i = 1 = \frac{1 \cdot 2}{2}$. The base case holds.

  \textbf{Inductive step}:
  Assume $\sum_{i=1}^{k} i = \frac{k(k+1)}{2}$ for some $k \geq 1$.
  Then
  \[
    \sum_{i=1}^{k+1} i
    = \left(\sum_{i=1}^{k} i\right) + (k+1)
    = \frac{k(k+1)}{2} + (k+1)
    = \frac{k(k+1) + 2(k+1)}{2}
    = \frac{(k+1)(k+2)}{2}.
  \]
  This is precisely the formula with $n = k+1$.

  By induction, the result holds for all $n \geq 1$. \qed
\end{proof}
```

---

## 4. 構造性證明 (Constructive Proof)

### 定義

通過明確構造出滿足條件的對象，來證明該對象的存在性。與純存在性證明不同，
構造性證明提供了一個具體的例子或演算法。

### 適用場景

- 存在性命題（$\exists x$ such that $P(x)$）
- 演算法設計與正確性（構造出解並驗證其正確）
- 具體界的建立（構造出達到界的例子）
- 反例構造（證明某性質不普遍成立）
- 編碼理論中的編碼方案設計

### 模板結構

```latex
\begin{proof}
  We construct the desired object explicitly.
  % Step 1: Construction
  Define $x = $ [explicit construction].
  % Step 2: Verification
  We now verify that $x$ satisfies all required properties.
  [Property 1]: ...
  [Property 2]: ...
  % Step 3: Conclude
  Therefore, such an $x$ exists. \qed
\end{proof}
```

### 常見錯誤

1. **構造不明確**：構造過程含糊不清，讀者無法重現。
   解決方法：提供精確的定義，避免模糊的描述。
2. **驗證不完整**：只驗證了部分性質。
   解決方法：列出所有需要驗證的性質，逐一檢查。
3. **構造依賴未證明的存在性**：構造過程中使用了另一個未證明存在的對象。
   解決方法：確保構造過程只使用已知的運算和對象。
4. **非良定義**：構造的對象可能在某些情況下未定義。
   解決方法：驗證構造在所有情況下都是良定義的。

### 範例

**主張**：There exists a surjective function from $\mathbb{N}$ to $\mathbb{Z}$。

```latex
\begin{proof}
  Define $f: \mathbb{N} \to \mathbb{Z}$ by
  \[
    f(n) =
    \begin{cases}
      n/2 & \text{if } n \text{ is even}, \\
      -(n+1)/2 & \text{if } n \text{ is odd}.
    \end{cases}
  \]
  We verify surjectivity. Let $z \in \mathbb{Z}$ be arbitrary.
  If $z \geq 0$, then $f(2z) = z$. If $z < 0$, then $f(-2z - 1) = z$.
  In both cases, there exists $n \in \mathbb{N}$ with $f(n) = z$.
  Therefore, $f$ is surjective. \qed
\end{proof}
```

---

## 5. 歸約法 (Proof by Reduction)

### 定義

將要證明的問題轉化為一個已知已解決（或已知性質）的問題。通過建立兩個問題之間
的對應關係，將已知結果「搬運」到新問題上。

### 適用場景

- 計算複雜度下界（如 NP-hardness 證明）
- 不可判定性證明（歸約到停機問題）
- 問題等價性的建立
- 利用已知的最佳化問題結果
- 密碼學中的安全性歸約

### 模板結構

```latex
\begin{proof}
  We prove the result by reduction from [Known Problem].
  % Step 1: Describe the reduction
  Given an instance $I$ of [Known Problem], we construct
  an instance $I'$ of [Target Problem] as follows: ...
  % Step 2: Correctness (forward direction)
  If $I$ is a YES-instance, then ... , so $I'$ is also
  a YES-instance.
  % Step 3: Correctness (backward direction)
  Conversely, if $I'$ is a YES-instance, then ... , so $I$
  is also a YES-instance.
  % Step 4: Conclude
  Since [Known Problem] is [hard/undecidable], it follows that
  [Target Problem] is also [hard/undecidable]. \qed
\end{proof}
```

### 常見錯誤

1. **歸約方向錯誤**：證明 NP-hardness 時應從已知 NP-hard 問題歸約到目標問題，
   而非反向。
   解決方法：明確標記歸約的方向。
2. **歸約不保持結構**：轉化過程改變了問題的本質性質。
   解決方法：驗證雙向的正確性。
3. **效率問題**：歸約的轉化過程本身計算複雜度過高。
   解決方法：確認歸約在要求的複雜度範圍內（如多項式時間）。
4. **特殊情況遺漏**：歸約在某些邊界情況下不成立。
   解決方法：列舉並處理所有邊界情況。

### 範例

**主張**：Vertex Cover is NP-hard。

```latex
\begin{proof}
  We reduce from Independent Set, which is known to be NP-hard.
  Given a graph $G = (V, E)$ and integer $k$, the Independent Set
  instance asks whether $G$ has an independent set of size $\geq k$.
  We construct a Vertex Cover instance: the same graph $G$ with
  parameter $|V| - k$.

  If $G$ has an independent set $S$ of size $\geq k$, then $V
  \setminus S$ is a vertex cover of size $\leq |V| - k$, since
  every edge has at least one endpoint in $V \setminus S$.

  Conversely, if $G$ has a vertex cover $C$ of size $\leq |V| - k$,
  then $V \setminus C$ is an independent set of size $\geq k$.

  The reduction runs in polynomial time. Since Independent Set is
  NP-hard, Vertex Cover is also NP-hard. \qed
\end{proof}
```

---

## 6. 機率法 (Probabilistic Method)

### 定義

通過證明隨機選擇的對象滿足特定性質的機率大於零，來證明滿足該性質的對象一定
存在。此方法不需要明確構造出該對象。

### 適用場景

- 組合數學中的存在性問題（如 Ramsey 理論）
- 圖論中的極值問題
- 隨機化演算法的期望值分析
- 編碼理論中的好碼存在性
- 學習理論中的隨機抽樣分析

### 模板結構

```latex
\begin{proof}
  Consider a random object $X$ drawn from [distribution/construction].
  % Step 1: Compute probability or expectation
  We compute $\mathbb{E}[f(X)]$ (or $\Pr[\text{event}]$):
  [calculation]
  % Step 2: Existence argument
  Since $\mathbb{E}[f(X)] < t$ (or $\Pr[\text{event}] > 0$),
  there must exist a realization $x$ of $X$ such that $f(x) < t$
  (or the event occurs).
  % Step 3: Conclude
  Therefore, the desired object exists. \qed
\end{proof}
```

### 關鍵工具

- **期望值論證**：若 $\mathbb{E}[X] < c$，則存在 $\omega$ 使得 $X(\omega) < c$。
- **Lovász Local Lemma**：當壞事件有有限的依賴關係時。
- **第一動差法** (First Moment Method)。
- **第二動差法** (Second Moment Method)。
- **Alteration method**：先隨機構造，再修復不滿足的部分。

### 常見錯誤

1. **機率計算錯誤**：錯誤估計了機率或期望值。
   解決方法：仔細檢查機率計算，特別是獨立性假設。
2. **依賴關係忽略**：假設了不成立的獨立性。
   解決方法：使用 union bound 或 Lovász Local Lemma。
3. **存在性與構造混淆**：機率法僅證明存在性，不提供構造。
   解決方法：明確說明證明是非構造性的。
4. **分布選擇不當**：隨機分布的選擇使得分析困難。
   解決方法：嘗試均勻分布或其他自然的分布。

### 範例

**主張**：For any graph $G$ with $n$ vertices and $m$ edges, there exists a
cut of size at least $m/2$。

```latex
\begin{proof}
  Assign each vertex independently and uniformly at random to one of
  two sets $S$ and $\bar{S}$. For each edge $e = (u,v)$, let $X_e$
  be the indicator that $e$ crosses the cut, i.e., one endpoint is
  in $S$ and the other in $\bar{S}$. Then $\Pr[X_e = 1] = 1/2$.
  The expected number of crossing edges is
  \[
    \mathbb{E}\left[\sum_{e \in E} X_e\right]
    = \sum_{e \in E} \Pr[X_e = 1]
    = \frac{m}{2}.
  \]
  Since the expected cut size is $m/2$, there exists a partition
  $(S, \bar{S})$ with at least $m/2$ crossing edges. \qed
\end{proof}
```

---

## 7. 凸性論證 (Convexity Arguments)

### 定義

利用凸函數或凸集的性質來建立不等式或最佳化結論。凸性是最佳化和機器學習理論中
最常用的結構性假設之一。

### 適用場景

- 不等式的推導（利用 Jensen's inequality）
- 最佳化問題的全域最優性保證
- 機器學習中的損失函數分析
- 凸鬆弛 (convex relaxation) 的近似界
- 資訊幾何和統計推論

### 關鍵工具

- **Jensen's inequality**：若 $f$ 為凸函數，則
  $f(\mathbb{E}[X]) \leq \mathbb{E}[f(X)]$。
- **凸函數的一階條件**：$f(y) \geq f(x) + \nabla f(x)^T (y - x)$。
- **凸函數的二階條件**：$\nabla^2 f(x) \succeq 0$。
- **Fenchel 對偶**：$f^*(y) = \sup_x \{ \langle y, x \rangle - f(x) \}$。
- **KKT 條件**：凸最佳化問題的最優性必要充分條件。

### 模板結構

```latex
\begin{proof}
  % Step 1: Establish convexity
  We first verify that $f$ is convex. [Show Hessian is PSD /
  show definition holds.]
  % Step 2: Apply convexity tool
  By Jensen's inequality (or first-order condition), we have ...
  % Step 3: Derive desired bound
  It follows that ...
  % Step 4: Conclude
  This establishes the claimed inequality. \qed
\end{proof}
```

### 常見錯誤

1. **凸性未驗證**：假設函數為凸但未證明。
   解決方法：明確驗證凸性（計算 Hessian 或使用定義）。
2. **Jensen 方向錯誤**：凸函數和凹函數的 Jensen 不等式方向相反。
   解決方法：明確標記函數是凸還是凹。
3. **定義域問題**：函數僅在部分定義域上為凸。
   解決方法：確認所有相關點都在凸性成立的定義域內。
4. **嚴格凸與凸混淆**：嚴格凸保證唯一最小值，普通凸不保證。
   解決方法：根據需要區分嚴格凸與凸。

### 範例

**主張**：For a convex function $f$ and i.i.d. random variables $X_1, \ldots, X_n$,
$f\!\left(\frac{1}{n}\sum_{i=1}^n X_i\right) \leq \frac{1}{n}\sum_{i=1}^n f(X_i)$。

```latex
\begin{proof}
  Since $f$ is convex, Jensen's inequality gives
  \[
    f\!\left(\mathbb{E}\!\left[\frac{1}{n}\sum_{i=1}^n X_i
    \,\middle|\, X_1, \ldots, X_n\right]\right)
    \leq \mathbb{E}\!\left[f\!\left(\frac{1}{n}\sum_{i=1}^n X_i\right)
    \,\middle|\, X_1, \ldots, X_n\right].
  \]
  Applying Jensen's inequality directly to the deterministic
  quantities $X_1, \ldots, X_n$ (viewed as a uniform mixture):
  \[
    f\!\left(\frac{1}{n}\sum_{i=1}^n X_i\right)
    \leq \frac{1}{n}\sum_{i=1}^n f(X_i),
  \]
  which is the desired result. \qed
\end{proof}
```

---

## 8. 資訊論方法 (Information-theoretic Methods)

### 定義

使用熵 (entropy)、互資訊 (mutual information)、KL 散度 (KL divergence) 等
資訊論工具進行推導。特別適用於建立下界和不可能性結果。

### 適用場景

- 通訊系統的容量界
- 學習理論中的 minimax 下界
- 差分隱私的分析
- 數據壓縮的極限
- 統計估計的 Cramér-Rao 下界

### 關鍵工具

- **Shannon entropy**：$H(X) = -\sum_x p(x) \log p(x)$
- **Mutual information**：$I(X; Y) = H(X) - H(X | Y)$
- **KL divergence**：$D_{\mathrm{KL}}(P \| Q) = \sum_x P(x) \log \frac{P(x)}{Q(x)}$
- **Data processing inequality**：若 $X \to Y \to Z$ 為 Markov chain，
  則 $I(X; Z) \leq I(X; Y)$
- **Fano's inequality**：$H(X | Y) \leq h_b(P_e) + P_e \log(|\mathcal{X}| - 1)$
- **Pinsker's inequality**：$\|P - Q\|_{\mathrm{TV}} \leq \sqrt{\frac{1}{2} D_{\mathrm{KL}}(P \| Q)}$

### 模板結構

```latex
\begin{proof}
  % Step 1: Set up information-theoretic quantities
  Consider the mutual information $I(X; Y)$ where ...
  % Step 2: Upper bound via data processing or other tools
  By the data processing inequality, $I(X; Y) \leq ...$
  % Step 3: Lower bound via Fano's inequality or other tools
  By Fano's inequality, $I(X; Y) \geq ...$
  % Step 4: Combine bounds
  Combining the upper and lower bounds, we obtain ...
  % Step 5: Conclude
  Therefore, ... \qed
\end{proof}
```

### 常見錯誤

1. **對數底數不一致**：混用 $\log_2$ 和 $\ln$。
   解決方法：在證明開頭明確宣告對數底數。
2. **Markov chain 條件不滿足**：錯誤地應用 data processing inequality。
   解決方法：驗證變數之間的 Markov 關係。
3. **連續與離散混用**：離散熵和微分熵的性質不完全相同。
   解決方法：區分使用 $H(X)$ 和 $h(X)$。
4. **KL 散度的不對稱性**：$D_{\mathrm{KL}}(P \| Q) \neq D_{\mathrm{KL}}(Q \| P)$。
   解決方法：注意 KL 散度的方向。

### 範例

**主張**：For binary hypothesis testing between $P$ and $Q$, the error probability
satisfies $P_e \geq \frac{1}{2} \exp(-D_{\mathrm{KL}}(P \| Q))$。

```latex
\begin{proof}
  Let $\phi$ be any test. The sum of Type I and Type II errors is
  \[
    P(\phi = 1) + Q(\phi = 0)
    = 1 - \|P - Q\|_{\mathrm{TV}} \cdot [\text{optimal test gain}].
  \]
  By Pinsker's inequality,
  $\|P - Q\|_{\mathrm{TV}} \leq \sqrt{\frac{1}{2} D_{\mathrm{KL}}(P \| Q)}$.
  Using the inequality $1 - x \geq e^{-2x}$ for $x \in [0, 1/2]$,
  we obtain
  \[
    P_e \geq \frac{1}{2}\left(1 - \|P - Q\|_{\mathrm{TV}}\right)
    \geq \frac{1}{2} \exp\!\left(-D_{\mathrm{KL}}(P \| Q)\right).
  \]
  \qed
\end{proof}
```

---

## 策略選擇摘要表

| 策略 | 最適合情境 | 難度 | 常見於 |
|------|-----------|------|--------|
| 直接證明 | 路徑明確的推導 | 低-中 | 各領域 |
| 反證法 | 否定形式、唯一性 | 中 | 分析、代數 |
| 數學歸納法 | 遞迴結構、序列 | 低-中 | 離散數學、CS |
| 構造性證明 | 存在性、演算法 | 中-高 | CS、代數 |
| 歸約法 | 複雜度下界 | 中-高 | CS、密碼學 |
| 機率法 | 組合存在性 | 中-高 | 組合、圖論 |
| 凸性論證 | 最佳化、界 | 中 | ML、最佳化 |
| 資訊論方法 | 下界、不可能性 | 高 | 通訊、學習理論 |
