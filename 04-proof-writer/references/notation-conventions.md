# 數學符號慣例

本文件統整數學符號的使用慣例，涵蓋一般數學、機器學習/深度學習領域常用符號，
以及符號一致性原則和常見衝突的解決方法。

---

## 一般數學符號

### 集合與空間

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\mathbb{R}$ | 實數集 | `\mathbb{R}` |
| $\mathbb{R}^n$ | $n$ 維實數空間 | `\mathbb{R}^n` |
| $\mathbb{R}^{m \times n}$ | $m \times n$ 實數矩陣空間 | `\mathbb{R}^{m \times n}` |
| $\mathbb{Z}$ | 整數集 | `\mathbb{Z}` |
| $\mathbb{N}$ | 自然數集 | `\mathbb{N}` |
| $\mathbb{C}$ | 複數集 | `\mathbb{C}` |
| $\mathbb{Q}$ | 有理數集 | `\mathbb{Q}` |
| $\emptyset$ | 空集 | `\emptyset` |
| $\mathcal{X}$ | 輸入空間 | `\mathcal{X}` |
| $\mathcal{Y}$ | 輸出空間 | `\mathcal{Y}` |
| $\mathcal{H}$ | 假設類 / Hilbert space | `\mathcal{H}` |
| $\mathcal{F}$ | 函數類 | `\mathcal{F}` |
| $\mathbb{S}^n$ | $n$ 維球面 | `\mathbb{S}^n` |
| $\Delta_n$ | $n$ 維單純形 | `\Delta_n` |

### 集合運算

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\in$ | 屬於 | `\in` |
| $\notin$ | 不屬於 | `\notin` |
| $\subseteq$ | 子集（含等號） | `\subseteq` |
| $\subset$ | 真子集 | `\subset` |
| $\cup$ | 聯集 | `\cup` |
| $\cap$ | 交集 | `\cap` |
| $\setminus$ | 集合差 | `\setminus` |
| $\times$ | 笛卡爾積 | `\times` |
| $|A|$ | 集合大小 | `|A|` or `\lvert A \rvert` |

### 邏輯符號

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\forall$ | 對所有 | `\forall` |
| $\exists$ | 存在 | `\exists` |
| $\nexists$ | 不存在 | `\nexists` |
| $\Rightarrow$ | 蘊涵 | `\Rightarrow` |
| $\Leftrightarrow$ | 若且唯若 | `\Leftrightarrow` |
| $\neg$ | 否定 | `\neg` |
| $\wedge$ | 且 | `\wedge` |
| $\vee$ | 或 | `\vee` |

### 函數與運算

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $f: A \to B$ | 函數映射 | `f: A \to B` |
| $f \circ g$ | 函數合成 | `f \circ g` |
| $f^{-1}$ | 反函數 | `f^{-1}` |
| $\sup$ | 上確界 | `\sup` |
| $\inf$ | 下確界 | `\inf` |
| $\max$ | 最大值 | `\max` |
| $\min$ | 最小值 | `\min` |
| $\arg\max$ | 取最大值的引數 | `\arg\max` or `\operatorname{argmax}` |
| $\arg\min$ | 取最小值的引數 | `\arg\min` or `\operatorname{argmin}` |
| $\lim$ | 極限 | `\lim` |
| $O(\cdot)$ | 大 O 記號 | `O(\cdot)` |
| $\Omega(\cdot)$ | 大 Omega 記號 | `\Omega(\cdot)` |
| $\Theta(\cdot)$ | 大 Theta 記號 | `\Theta(\cdot)` |
| $o(\cdot)$ | 小 o 記號 | `o(\cdot)` |

---

## 線性代數符號

### 向量與矩陣

| 符號 | 含義 | LaTeX | 備註 |
|------|------|-------|------|
| $\mathbf{x}$, $\boldsymbol{x}$ | 向量 | `\mathbf{x}`, `\boldsymbol{x}` | 粗體小寫 |
| $\mathbf{A}$, $\boldsymbol{A}$ | 矩陣 | `\mathbf{A}`, `\boldsymbol{A}` | 粗體大寫 |
| $\mathbf{I}$ | 單位矩陣 | `\mathbf{I}` | 有時記為 $I_n$ |
| $\mathbf{0}$ | 零向量/矩陣 | `\mathbf{0}` | 由語境判斷 |
| $\mathbf{1}$ | 全一向量 | `\mathbf{1}` | |
| $\mathbf{e}_i$ | 第 $i$ 個標準基向量 | `\mathbf{e}_i` | |

### 矩陣運算

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $A^T$ | 轉置 | `A^T` or `A^\top` |
| $A^{-1}$ | 逆矩陣 | `A^{-1}` |
| $A^\dagger$ | 偽逆 | `A^\dagger` |
| $\mathrm{tr}(A)$ | 跡 | `\mathrm{tr}(A)` or `\operatorname{tr}(A)` |
| $\det(A)$ | 行列式 | `\det(A)` |
| $\mathrm{rank}(A)$ | 秩 | `\mathrm{rank}(A)` |
| $\lambda_i(A)$ | 第 $i$ 個特徵值 | `\lambda_i(A)` |
| $\sigma_i(A)$ | 第 $i$ 個奇異值 | `\sigma_i(A)` |
| $A \succeq 0$ | 正半定 | `A \succeq 0` |
| $A \succ 0$ | 正定 | `A \succ 0` |
| $A \otimes B$ | Kronecker 積 | `A \otimes B` |
| $A \odot B$ | Hadamard (逐元素) 積 | `A \odot B` |

### 範數

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\|x\|$ | 範數（預設為 $\ell_2$） | `\|x\|` or `\lVert x \rVert` |
| $\|x\|_p$ | $\ell_p$ 範數 | `\|x\|_p` |
| $\|x\|_1$ | $\ell_1$ 範數 | `\|x\|_1` |
| $\|x\|_\infty$ | $\ell_\infty$ 範數 | `\|x\|_\infty` |
| $\|A\|_F$ | Frobenius 範數 | `\|A\|_F` |
| $\|A\|_{\mathrm{op}}$ | 運算元範數 | `\|A\|_{\mathrm{op}}` |
| $\|A\|_*$ | 核範數 | `\|A\|_*` |

### 內積

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\langle x, y \rangle$ | 內積 | `\langle x, y \rangle` |
| $x^T y$ | 向量點積 | `x^T y` |
| $x \cdot y$ | 點積（較少用） | `x \cdot y` |

---

## 機率與統計符號

### 基本機率

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\Pr[\cdot]$ | 機率 | `\Pr[\cdot]` |
| $\mathbb{E}[\cdot]$ | 期望值 | `\mathbb{E}[\cdot]` |
| $\mathrm{Var}[\cdot]$ | 變異數 | `\mathrm{Var}[\cdot]` |
| $\mathrm{Cov}[\cdot]$ | 共變異數 | `\mathrm{Cov}[\cdot]` |
| $X \sim P$ | $X$ 服從分布 $P$ | `X \sim P` |
| $X \perp Y$ | $X$ 與 $Y$ 獨立 | `X \perp Y` |
| $X \mid Y$ | 條件於 $Y$ | `X \mid Y` |
| $\mathbb{E}[X \mid Y]$ | 條件期望 | `\mathbb{E}[X \mid Y]` |
| $p(x)$ | 機率密度/質量函數 | `p(x)` |
| $F(x)$ | 累積分布函數 | `F(x)` |
| $X_1, \ldots, X_n \overset{\text{i.i.d.}}{\sim} P$ | 獨立同分布 | `\overset{\text{i.i.d.}}{\sim}` |

### 常見分布

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\mathcal{N}(\mu, \sigma^2)$ | 常態分布 | `\mathcal{N}(\mu, \sigma^2)` |
| $\mathrm{Bernoulli}(p)$ | 伯努利分布 | `\mathrm{Bernoulli}(p)` |
| $\mathrm{Uniform}(a, b)$ | 均勻分布 | `\mathrm{Uniform}(a, b)` |
| $\mathrm{Binomial}(n, p)$ | 二項分布 | `\mathrm{Binomial}(n, p)` |
| $\mathrm{Poisson}(\lambda)$ | 泊松分布 | `\mathrm{Poisson}(\lambda)` |
| $\mathrm{Exp}(\lambda)$ | 指數分布 | `\mathrm{Exp}(\lambda)` |

### 收斂記號

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $\xrightarrow{d}$ | 分布收斂 | `\xrightarrow{d}` |
| $\xrightarrow{p}$ | 機率收斂 | `\xrightarrow{p}` |
| $\xrightarrow{a.s.}$ | 幾乎必然收斂 | `\xrightarrow{a.s.}` |
| $\xrightarrow{L^p}$ | $L^p$ 收斂 | `\xrightarrow{L^p}` |

---

## ML/DL 領域常用符號

### 監督學習

| 符號 | 含義 | 備註 |
|------|------|------|
| $\mathcal{D}$ | 數據分布 | |
| $S = \{(x_i, y_i)\}_{i=1}^n$ | 訓練集 | $n$ 個樣本 |
| $f_\theta$ 或 $h_\theta$ | 參數化模型 | $\theta$ 為參數 |
| $\ell(\hat{y}, y)$ | 損失函數 | |
| $\mathcal{L}(\theta)$ | 經驗損失 | $\frac{1}{n}\sum_i \ell(f_\theta(x_i), y_i)$ |
| $R(f)$ | 真實風險 | $\mathbb{E}_{(x,y)\sim\mathcal{D}}[\ell(f(x), y)]$ |
| $\hat{R}_n(f)$ | 經驗風險 | |
| $\lambda$ | 正則化參數 | |
| $\Omega(\theta)$ | 正則化項 | |

### 深度學習

| 符號 | 含義 | 備註 |
|------|------|------|
| $W^{(l)}$ | 第 $l$ 層的權重矩陣 | |
| $b^{(l)}$ | 第 $l$ 層的偏差向量 | |
| $a^{(l)}$ | 第 $l$ 層的激活值 | |
| $\sigma(\cdot)$ | 激活函數 | ReLU, sigmoid 等 |
| $\nabla_\theta \mathcal{L}$ | 損失對參數的梯度 | |
| $\eta$ | 學習率 | |
| $B$ | batch size | |
| $T$ | 總訓練步數或時間步 | |
| $L$ | 網路層數 | |
| $d$ | 特徵維度 | |
| $d_{\mathrm{model}}$ | 模型維度 (Transformer) | |
| $d_k$, $d_v$ | key/value 維度 | |
| $h$ | 注意力頭數 | |

### 最佳化

| 符號 | 含義 | 備註 |
|------|------|------|
| $\nabla f$ | 梯度 | |
| $\nabla^2 f$ | Hessian 矩陣 | |
| $\theta_{t+1} = \theta_t - \eta \nabla \mathcal{L}(\theta_t)$ | 梯度下降更新 | |
| $\beta_1, \beta_2$ | Adam 的動量參數 | |
| $\epsilon$ | 數值穩定性常數 | Adam 中 |
| $L$ | Lipschitz 常數 | 梯度 Lipschitz |
| $\mu$ | 強凸參數 | |
| $\kappa = L/\mu$ | 條件數 | |

### 資訊論 (ML 語境)

| 符號 | 含義 | LaTeX |
|------|------|-------|
| $H(X)$ | Shannon 熵 | `H(X)` |
| $H(X \mid Y)$ | 條件熵 | `H(X \mid Y)` |
| $I(X; Y)$ | 互資訊 | `I(X; Y)` |
| $D_{\mathrm{KL}}(P \| Q)$ | KL 散度 | `D_{\mathrm{KL}}(P \| Q)` |
| $h(X)$ | 微分熵 | `h(X)` |
| $\|P - Q\|_{\mathrm{TV}}$ | 全變差距離 | `\|P - Q\|_{\mathrm{TV}}` |

### 生成模型

| 符號 | 含義 | 備註 |
|------|------|------|
| $p_\theta(x)$ | 模型分布 | |
| $p_{\mathrm{data}}(x)$ | 真實數據分布 | |
| $q_\phi(z \mid x)$ | 編碼器 (VAE) | |
| $p_\theta(x \mid z)$ | 解碼器 (VAE) | |
| $z$ | 潛在變數 | |
| $\mathrm{ELBO}$ | 證據下界 | |
| $G$, $D$ | 生成器、判別器 (GAN) | |

---

## 符號一致性原則

### 原則一：全文一致

同一符號在整篇論文中必須代表同一含義。不同的概念必須使用不同的符號。

**錯誤範例**：在第 3 節用 $n$ 表示樣本數，在第 5 節用 $n$ 表示維度。

**正確做法**：用 $n$ 表示樣本數，$d$ 表示維度。

### 原則二：先定義後使用

每個符號在首次使用時必須明確定義。定義應出現在使用之前。

```latex
Let $n$ denote the number of training samples and $d$ denote the
input dimension. We consider a dataset
$S = \{(\mathbf{x}_i, y_i)\}_{i=1}^n$ where
$\mathbf{x}_i \in \mathbb{R}^d$.
```

### 原則三：遵循領域慣例

優先使用領域內約定俗成的符號。偏離慣例的選擇會增加讀者的認知負擔。

### 原則四：減少符號重載

同一字母不應在不同語境下表示不同的概念，除非語境完全不同且不會混淆。

### 原則五：下標與上標的使用規範

- **下標**：用於索引（$x_i$）、類型標記（$\theta_{\mathrm{init}}$）
- **上標**：用於冪次（$x^2$）、層次（$W^{(l)}$）、迭代（$\theta^{(t)}$）
- 括號區分：層次用 $W^{(l)}$，冪次用 $x^2$（無括號）

---

## 常見符號衝突與解決

### 衝突一：$\sigma$ 的多重含義

- $\sigma$：激活函數（sigmoid）
- $\sigma$：標準差
- $\sigma$：奇異值
- $\sigma$：置換 (permutation)

**解決方法**：
- 激活函數使用具體名稱：$\mathrm{sigmoid}(\cdot)$、$\mathrm{ReLU}(\cdot)$
- 標準差：保留 $\sigma$，或在需要區分時使用 $\mathrm{std}$
- 奇異值：使用 $\sigma_i(A)$ 搭配矩陣引數
- 置換：使用 $\pi$ 代替

### 衝突二：$\lambda$ 的多重含義

- $\lambda$：特徵值
- $\lambda$：正則化參數
- $\lambda$：速率參數（Poisson 分布）

**解決方法**：
- 特徵值：使用 $\lambda_i(A)$ 搭配矩陣引數
- 正則化：使用 $\lambda_{\mathrm{reg}}$ 或直接使用 $\lambda$（根據語境）
- 速率參數：使用 $\mu$ 或希臘字母替代

### 衝突三：$p$ 的多重含義

- $p$：機率 / 機率密度函數
- $p$：範數中的指數（$\ell_p$ 範數）
- $p$：維度或特徵數

**解決方法**：
- 機率：保留 $p(\cdot)$ 或 $P(\cdot)$
- 範數指數：保持在下標位置 $\|\cdot\|_p$
- 維度：使用 $d$ 代替

### 衝突四：$H$ 的多重含義

- $H$：熵
- $H$：假設類
- $H$：Hessian 矩陣

**解決方法**：
- 熵：使用 $H(X)$ 帶引數
- 假設類：使用 $\mathcal{H}$
- Hessian：使用 $\nabla^2 f$ 或 $\mathbf{H}$（粗體）

### 衝突五：$L$ 的多重含義

- $L$：損失函數
- $L$：Lipschitz 常數
- $L$：網路層數

**解決方法**：
- 損失函數：使用 $\mathcal{L}$ 或 $\ell$
- Lipschitz 常數：保留 $L$
- 網路層數：根據語境使用 $L$ 或 $D$（depth）

---

## 排版建議

### 粗體與花體的區分

| 風格 | 用途 | 範例 |
|------|------|------|
| 粗體小寫 $\mathbf{x}$ | 向量 | `\mathbf{x}` |
| 粗體大寫 $\mathbf{A}$ | 矩陣 | `\mathbf{A}` |
| 花體 $\mathcal{X}$ | 集合、空間、類 | `\mathcal{X}` |
| 黑板粗體 $\mathbb{R}$ | 數系 | `\mathbb{R}` |
| 正體 $\mathrm{tr}$ | 運算元名稱 | `\mathrm{tr}` |

### 自定義命令建議

在論文的 preamble 中定義常用符號，保持一致性並方便修改：

```latex
% 常用集合
\newcommand{\R}{\mathbb{R}}
\newcommand{\N}{\mathbb{N}}
\newcommand{\Z}{\mathbb{Z}}

% 機率與期望
\newcommand{\E}{\mathbb{E}}
\newcommand{\Var}{\mathrm{Var}}
\newcommand{\Cov}{\mathrm{Cov}}
\DeclareMathOperator*{\argmax}{argmax}
\DeclareMathOperator*{\argmin}{argmin}

% 範數與內積
\newcommand{\norm}[1]{\left\lVert #1 \right\rVert}
\newcommand{\abs}[1]{\left\lvert #1 \right\rvert}
\newcommand{\inner}[2]{\left\langle #1, #2 \right\rangle}

% 資訊論
\newcommand{\KL}[2]{D_{\mathrm{KL}}\left(#1 \| #2\right)}
\newcommand{\MI}[2]{I\left(#1; #2\right)}

% 向量與矩陣
\renewcommand{\vec}[1]{\mathbf{#1}}
\newcommand{\mat}[1]{\mathbf{#1}}
```
