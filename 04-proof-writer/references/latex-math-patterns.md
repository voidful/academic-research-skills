# LaTeX 數學排版模式

本文件涵蓋 LaTeX 數學排版的常用模式，包括定理環境設定、排版技巧、對齊方式，
以及矩陣等常用結構。

---

## 必要套件

以下為數學證明排版常需的 LaTeX 套件：

```latex
\usepackage{amsmath}    % 數學環境：align, gather, cases 等
\usepackage{amssymb}    % 數學符號：\mathbb, \because 等
\usepackage{amsthm}     % 定理環境：theorem, proof 等
\usepackage{mathtools}  % amsmath 的增強：\coloneqq, \DeclarePairedDelimiter 等
\usepackage{bm}         % 粗體數學符號 \bm{x}
\usepackage{bbm}        % 黑板粗體數字 \mathbbm{1}（指示函數）
\usepackage{thmtools}   % 定理環境的進階管理
```

---

## 定理環境設定

### 基本設定 (amsthm)

```latex
% 定理風格：粗體標題、斜體內文
\theoremstyle{plain}
\newtheorem{theorem}{Theorem}[section]
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem{proposition}[theorem]{Proposition}
\newtheorem{corollary}[theorem]{Corollary}
\newtheorem{conjecture}[theorem]{Conjecture}

% 定義風格：粗體標題、正體內文
\theoremstyle{definition}
\newtheorem{definition}[theorem]{Definition}
\newtheorem{example}[theorem]{Example}
\newtheorem{assumption}[theorem]{Assumption}
\newtheorem{condition}[theorem]{Condition}

% 備註風格：斜體標題、正體內文
\theoremstyle{remark}
\newtheorem{remark}[theorem]{Remark}
\newtheorem{note}[theorem]{Note}
\newtheorem{claim}{Claim}
```

**說明**：

- `[section]` 表示編號按章節重設（如 Theorem 3.1）。
- `[theorem]` 表示與 theorem 共用編號計數器，確保順序編號。
- `claim` 獨立編號，不與其他環境共用計數器。

### 未編號版本

```latex
\newtheorem*{theorem*}{Theorem}
\newtheorem*{lemma*}{Lemma}
\newtheorem*{remark*}{Remark}
```

### 自訂 QED 符號

```latex
% 預設為空心方塊 □
\renewcommand{\qedsymbol}{$\blacksquare$}  % 改為實心方塊
```

---

## Theorem / Lemma / Proof 完整範例

### 基本定理與證明

```latex
\begin{theorem}[Pythagorean Theorem]
\label{thm:pythagoras}
  For a right triangle with legs $a$, $b$ and hypotenuse $c$,
  \[
    a^2 + b^2 = c^2.
  \]
\end{theorem}

\begin{proof}
  Consider the square with side length $a + b$. By arranging
  four copies of the triangle inside the square, we obtain ...
  \qed
\end{proof}
```

### 引理與推論

```latex
\begin{lemma}
\label{lem:helper}
  If $f$ is convex and differentiable, then for all $x, y$,
  \[
    f(y) \geq f(x) + \nabla f(x)^\top (y - x).
  \]
\end{lemma}

\begin{proof}
  By convexity, for $t \in (0, 1]$,
  \[
    f(x + t(y - x)) \leq (1 - t)f(x) + tf(y).
  \]
  Rearranging and taking $t \to 0$ yields the result. \qed
\end{proof}

\begin{corollary}
\label{cor:minimum}
  If $\nabla f(x^*) = 0$ and $f$ is convex, then $x^*$ is a
  global minimizer of $f$.
\end{corollary}

\begin{proof}
  By Lemma~\ref{lem:helper}, $f(y) \geq f(x^*) + 0 = f(x^*)$
  for all $y$. \qed
\end{proof}
```

### 帶名稱的定理

```latex
\begin{theorem}[Jensen's Inequality]
\label{thm:jensen}
  Let $f$ be a convex function and $X$ a random variable with
  $\mathbb{E}[|X|] < \infty$. Then
  \[
    f(\mathbb{E}[X]) \leq \mathbb{E}[f(X)].
  \]
\end{theorem}
```

### 證明草稿 (Proof Sketch)

```latex
\begin{proof}[Proof sketch]
  The main idea is to apply Hoeffding's inequality to each
  hypothesis and then take a union bound over $\mathcal{H}$.
  The full proof is deferred to Appendix~\ref{app:full-proof}.
\end{proof}
```

---

## 等式與公式排版

### 行內公式

```latex
The loss function $\ell(y, \hat{y}) = (y - \hat{y})^2$ is convex.
```

### 展示公式（無編號）

```latex
\[
  f(x) = \sum_{i=1}^n a_i x^i
\]
```

### 展示公式（有編號）

```latex
\begin{equation}
\label{eq:loss}
  \mathcal{L}(\theta) = \frac{1}{n} \sum_{i=1}^n
  \ell(f_\theta(x_i), y_i) + \lambda \|\theta\|_2^2
\end{equation}
```

### 多行對齊 (align)

```latex
\begin{align}
  \mathcal{L}(\theta)
  &= \frac{1}{n} \sum_{i=1}^n \ell(f_\theta(x_i), y_i)
     + \lambda \|\theta\|_2^2 \label{eq:loss-expanded} \\
  &\leq \frac{1}{n} \sum_{i=1}^n \left[
     \ell(f_{\theta^*}(x_i), y_i)
     + \nabla \ell^\top (\theta - \theta^*)
     \right] + \lambda \|\theta\|_2^2 \label{eq:loss-bound} \\
  &= \mathcal{L}(\theta^*) + \text{(remainder terms)}.
     \nonumber
\end{align}
```

**說明**：
- `&` 標記對齊位置（通常放在 `=` 或 `\leq` 前）。
- `\\` 換行。
- `\nonumber` 取消該行的編號。
- 每行可獨立加 `\label`。

### 無編號的多行對齊

```latex
\begin{align*}
  (a + b)^2 &= a^2 + 2ab + b^2 \\
  (a - b)^2 &= a^2 - 2ab + b^2
\end{align*}
```

### 多行等式組 (gather)

適用於多個獨立的等式，不需要對齊：

```latex
\begin{gather}
  x^2 + y^2 = 1 \label{eq:circle} \\
  z = x + iy \label{eq:complex}
\end{gather}
```

### 子等式 (subequations)

```latex
\begin{subequations}
\label{eq:system}
\begin{align}
  \nabla_x L &= 0 \label{eq:system-x} \\
  \nabla_\lambda L &= 0 \label{eq:system-lambda}
\end{align}
\end{subequations}
```

這會產生 (1a)、(1b) 的編號，而 `\ref{eq:system}` 引用整組。

---

## 分情況討論

### cases 環境

```latex
\[
  |x| =
  \begin{cases}
    x  & \text{if } x \geq 0, \\
    -x & \text{if } x < 0.
  \end{cases}
\]
```

### dcases 環境 (mathtools)

`dcases` 使用展示模式大小，而 `cases` 使用行內大小：

```latex
\[
  f(x) =
  \begin{dcases}
    \frac{1}{\sqrt{2\pi}} e^{-x^2/2} & \text{if } x > 0, \\
    0 & \text{otherwise}.
  \end{dcases}
\]
```

---

## 矩陣排版

### 基本矩陣

```latex
% 無括號
\[
  \begin{matrix}
    a & b \\
    c & d
  \end{matrix}
\]

% 圓括號
\[
  \begin{pmatrix}
    a & b \\
    c & d
  \end{pmatrix}
\]

% 方括號
\[
  \begin{bmatrix}
    a & b \\
    c & d
  \end{bmatrix}
\]

% 行列式用的雙直線
\[
  \begin{vmatrix}
    a & b \\
    c & d
  \end{vmatrix}
\]
```

### 大型矩陣（含省略號）

```latex
\[
  \mathbf{A} =
  \begin{bmatrix}
    a_{11} & a_{12} & \cdots & a_{1n} \\
    a_{21} & a_{22} & \cdots & a_{2n} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{m1} & a_{m2} & \cdots & a_{mn}
  \end{bmatrix}
\]
```

### 分塊矩陣

```latex
\[
  \mathbf{M} =
  \left[
  \begin{array}{c|c}
    \mathbf{A} & \mathbf{B} \\
    \hline
    \mathbf{C} & \mathbf{D}
  \end{array}
  \right]
\]
```

### 行內小矩陣

```latex
The matrix $\bigl(\begin{smallmatrix} a & b \\ c & d
\end{smallmatrix}\bigr)$ is invertible.
```

---

## 括號與定界符

### 自動調整大小

```latex
\left( \frac{a}{b} \right)
\left[ \sum_{i=1}^n x_i \right]
\left\{ x \in \mathbb{R} : x > 0 \right\}
\left\| \mathbf{x} \right\|
\left\langle \mathbf{x}, \mathbf{y} \right\rangle
```

### 手動調整大小

```latex
\big( \Big( \bigg( \Bigg(
\big) \Big) \bigg) \Bigg)
```

**建議**：多數情況使用 `\left...\right`，但在多行公式中（跨行的括號），
需要手動使用 `\big` 系列或 `\left.\right.` 搭配不可見定界符。

### 跨行括號

```latex
\begin{align}
  f(x) &= \biggl( \sum_{i=1}^n a_i x^i \biggr)
           \cdot \biggl( \sum_{j=1}^m b_j x^j \biggr)
\end{align}
```

---

## 常用排版技巧

### 文字在公式中

```latex
\[
  x \in S \quad \text{if and only if} \quad f(x) > 0
\]

\[
  \sum_{i=1}^n x_i \qquad \text{where } x_i \geq 0
\]
```

### 間距控制

| 命令 | 寬度 | 用途 |
|------|------|------|
| `\,` | 薄間距 | 微分符號前 $\int f(x)\,dx$ |
| `\:` | 中間距 | |
| `\;` | 厚間距 | |
| `\quad` | 1em | 公式間分隔 |
| `\qquad` | 2em | 更大的分隔 |
| `\!` | 負薄間距 | 緊縮間距 |

### 數學運算元

```latex
% 預設運算元（正體）
\sin, \cos, \tan, \log, \ln, \exp, \det, \dim, \ker, \lim,
\max, \min, \sup, \inf, \gcd

% 自定義運算元
\DeclareMathOperator{\tr}{tr}
\DeclareMathOperator{\diag}{diag}
\DeclareMathOperator{\sign}{sign}
\DeclareMathOperator{\softmax}{softmax}
\DeclareMathOperator*{\argmax}{argmax}  % * 使下標在展示模式置於正下方
\DeclareMathOperator*{\argmin}{argmin}
```

### 上下標與裝飾

```latex
% 上方裝飾
\hat{x}        % 估計量
\tilde{x}      % 近似
\bar{x}        % 平均
\overline{AB}  % 長上劃線
\widehat{ABC}  % 寬帽子
\widetilde{f}  % 寬波浪

% 向量箭頭
\vec{x}        % 小箭頭
\overrightarrow{AB}  % 長箭頭

% 上下括號
\overbrace{a + b + c}^{\text{sum}}
\underbrace{x_1 + \cdots + x_n}_{n \text{ terms}}
```

### 省略號

```latex
$x_1, x_2, \ldots, x_n$     % 低省略號（逗號列舉）
$x_1 + x_2 + \cdots + x_n$  % 中省略號（運算符間）
$\vdots$                      % 垂直省略號
$\ddots$                      % 對角省略號
```

---

## 常見證明結構的排版

### 分步驟證明

```latex
\begin{proof}
  We prove the claim in two steps.

  \textbf{Step 1.}
  We first show that $A$ holds. [Derivation of A.]

  \textbf{Step 2.}
  Using Step~1, we now prove $B$. [Derivation of B using A.]

  Combining Steps~1 and~2, the result follows. \qed
\end{proof}
```

### 歸納法證明

```latex
\begin{proof}
  We proceed by (strong) induction on $n$.

  \textit{Base case} ($n = 1$).
  [Verification for n = 1.]

  \textit{Inductive step}.
  Suppose the claim holds for all $1 \leq j \leq k$.
  We show it for $k + 1$.
  [Derivation using inductive hypothesis.]

  By induction, the result holds for all $n \geq 1$. \qed
\end{proof}
```

### 反證法證明

```latex
\begin{proof}
  Suppose, for the sake of contradiction, that [negation].
  [Derivation leading to contradiction.]
  This contradicts [known fact], completing the proof. \qed
\end{proof}
```

### 充要條件證明

```latex
\begin{proof}
  ($\Rightarrow$)
  Assume $A$ holds. [Derivation showing $B$.]

  ($\Leftarrow$)
  Assume $B$ holds. [Derivation showing $A$.] \qed
\end{proof}
```

---

## 交叉引用

### 基本引用

```latex
By Theorem~\ref{thm:main}, ...
As shown in Equation~\eqref{eq:bound}, ...
See Lemma~\ref{lem:aux} and Corollary~\ref{cor:result}.
```

**注意**：
- 定理等環境用 `\ref`。
- 等式用 `\eqref`（自動加括號）。
- `~` 為不可斷行空格，防止引用編號與前文斷行。

### cleveref 套件（推薦）

```latex
\usepackage{cleveref}

% 自動判斷引用類型
\cref{thm:main}         % → Theorem 1
\Cref{thm:main}         % → Theorem 1 (句首大寫)
\cref{eq:bound}          % → (1)
\cref{lem:a,lem:b,lem:c} % → Lemmas 1, 2 and 3
```

---

## 附錄中的定理環境

論文附錄中的定理通常需要不同的編號格式：

```latex
\appendix

% 方法一：重設計數器
\setcounter{theorem}{0}
\renewcommand{\thetheorem}{\Alph{section}.\arabic{theorem}}

% 方法二：使用 restatable 環境 (thmtools)
% 在正文中：
\begin{restatable}{theorem}{maintheorem}
\label{thm:main}
  Statement of the main theorem.
\end{restatable}

% 在附錄中重新陳述：
\maintheorem*
\begin{proof}
  Full proof here. \qed
\end{proof}
```

---

## 常見排版問題與解決

### 問題一：括號大小不匹配

```latex
% 錯誤：\left \right 跨行
\begin{align}
  f(x) &= \left( \sum_{i=1}^n x_i \right. \\  % 報錯！
       &\quad \left. + y \right)
\end{align}

% 正確：使用 \bigl \bigr 或不可見定界符
\begin{align}
  f(x) &= \biggl( \sum_{i=1}^n x_i \nonumber \\
       &\quad + y \biggr)
\end{align}
```

### 問題二：長公式斷行

```latex
% 使用 multline 環境
\begin{multline}
  \mathcal{L}(\theta) = \frac{1}{n} \sum_{i=1}^n
  \ell(f_\theta(x_i), y_i) \\
  + \lambda_1 \|\theta\|_1 + \lambda_2 \|\theta\|_2^2
  + \gamma \sum_{j} R_j(\theta)
\end{multline}

% 或使用 split 在 equation 內
\begin{equation}
\begin{split}
  \mathcal{L}(\theta) &= \frac{1}{n} \sum_{i=1}^n
  \ell(f_\theta(x_i), y_i) \\
  &\quad + \lambda_1 \|\theta\|_1
  + \lambda_2 \|\theta\|_2^2
\end{split}
\end{equation}
```

### 問題三：條件機率中的 | 大小

```latex
% 錯誤：| 太短
p(y | x)

% 正確方案
p(y \mid x)                          % \mid 有適當間距
p\left(y \,\middle|\, x\right)      % 自動調整大小
p(y \given x)                        % 自定義命令（見下）

% 自定義命令
\newcommand{\given}{\,\middle|\,}
```

### 問題四：積分的排版

```latex
% 推薦風格：微分符號前加薄間距
\int_0^\infty f(x) \, dx

% 多重積分
\iint_D f(x, y) \, dx \, dy
\iiint_V f(x, y, z) \, dx \, dy \, dz

% 正體 d（某些風格指南要求）
\newcommand{\dd}{\mathrm{d}}
\int_0^\infty f(x) \, \dd x
```

### 問題五：最佳化問題的排版

```latex
\[
  \min_{\theta \in \Theta} \quad
  \frac{1}{n} \sum_{i=1}^n \ell(f_\theta(x_i), y_i)
  \quad \text{s.t.} \quad \|\theta\| \leq B
\]

% 更正式的排版
\[
  \begin{aligned}
    \minimize_{\theta} \quad
    & \frac{1}{n} \sum_{i=1}^n \ell(f_\theta(x_i), y_i) \\
    \text{subject to} \quad
    & \|\theta\|_2 \leq B, \\
    & \theta_j \geq 0, \quad j = 1, \ldots, d.
  \end{aligned}
\]

% 所需的自定義命令
\DeclareMathOperator{\minimize}{minimize}
\DeclareMathOperator{\maximize}{maximize}
```

---

## 完整證明排版範例

以下是一個完整的定理及其證明的排版範例：

```latex
\begin{theorem}[Generalization Bound for Finite Hypothesis Classes]
\label{thm:finite-gen-bound}
  Let $\mathcal{H}$ be a finite hypothesis class and let
  $S = \{(x_i, y_i)\}_{i=1}^n$ be drawn i.i.d.\ from a
  distribution $\mathcal{D}$. Assume the loss function $\ell$
  is bounded in $[0, 1]$. Then, for any $\delta > 0$, with
  probability at least $1 - \delta$ over the draw of $S$,
  for all $h \in \mathcal{H}$:
  \begin{equation}
  \label{eq:gen-bound}
    \left| R(h) - \hat{R}_n(h) \right|
    \leq \sqrt{\frac{\ln|\mathcal{H}| + \ln(2/\delta)}{2n}},
  \end{equation}
  where $R(h) = \mathbb{E}_{(x,y) \sim \mathcal{D}}[\ell(h(x), y)]$
  and $\hat{R}_n(h) = \frac{1}{n}\sum_{i=1}^n \ell(h(x_i), y_i)$.
\end{theorem}

\begin{proof}
  Fix any $h \in \mathcal{H}$. Define $Z_i = \ell(h(x_i), y_i)$
  for $i = 1, \ldots, n$. Since $\ell$ is bounded in $[0, 1]$,
  the $Z_i$ are i.i.d.\ random variables in $[0, 1]$ with mean
  $\mu = R(h)$.

  \textbf{Step 1} (Concentration for a single hypothesis).
  By Hoeffding's inequality,
  \begin{equation}
  \label{eq:hoeffding-single}
    \Pr\!\left[\left|\hat{R}_n(h) - R(h)\right| > \epsilon\right]
    \leq 2\exp(-2n\epsilon^2).
  \end{equation}

  \textbf{Step 2} (Union bound over $\mathcal{H}$).
  Applying the union bound over all $h \in \mathcal{H}$:
  \begin{align}
    \Pr\!\left[\exists\, h \in \mathcal{H}:
      \left|\hat{R}_n(h) - R(h)\right| > \epsilon\right]
    &\leq \sum_{h \in \mathcal{H}}
      \Pr\!\left[\left|\hat{R}_n(h) - R(h)\right|
      > \epsilon\right] \nonumber \\
    &\leq |\mathcal{H}| \cdot 2\exp(-2n\epsilon^2).
      \label{eq:union-bound}
  \end{align}

  \textbf{Step 3} (Solving for $\epsilon$).
  Setting the right-hand side of~\eqref{eq:union-bound} equal
  to $\delta$ and solving for $\epsilon$:
  \[
    2|\mathcal{H}|\exp(-2n\epsilon^2) = \delta
    \quad \Longrightarrow \quad
    \epsilon = \sqrt{\frac{\ln|\mathcal{H}| + \ln(2/\delta)}{2n}}.
  \]

  Substituting back, with probability at least $1 - \delta$,
  for all $h \in \mathcal{H}$,
  $|R(h) - \hat{R}_n(h)| \leq \epsilon$. This
  establishes~\eqref{eq:gen-bound}. \qed
\end{proof}
```
