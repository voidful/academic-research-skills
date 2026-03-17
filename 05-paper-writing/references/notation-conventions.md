# 符號與用語一致性規範

## 數學符號規範

在整篇論文中，符號使用必須完全一致：

| 類型 | 慣例 | 範例 |
|------|------|------|
| 向量 | 小寫粗體 | $\mathbf{x}$, $\mathbf{h}$ |
| 矩陣 | 大寫粗體 | $\mathbf{W}$, $\mathbf{A}$ |
| 純量 | 小寫斜體 | $x$, $\alpha$, $\lambda$ |
| 集合 | 大寫花體 | $\mathcal{X}$, $\mathcal{D}$ |
| 函數 | 小寫斜體或特定符號 | $f(\cdot)$, $\mathcal{L}$ |
| 維度 | 大寫斜體 | $N$, $D$, $T$ |
| 索引 | 小寫斜體 | $i$, $j$, $k$ |

## 時態規範

| 語境 | 時態 | 範例 |
|------|------|------|
| 描述本文方法 | 現在式 | We propose / Our method processes |
| 描述實驗過程 | 過去式 | We trained / We evaluated |
| 描述實驗結果 | 現在式 | Table 1 shows / Our method achieves |
| 描述先前工作 | 過去式 | Smith et al. proposed / Previous work focused on |
| 描述普遍事實 | 現在式 | Transformers are widely used |

## 用詞一致性

全文必須對同一概念使用同一詞彙：

```
❌ 混用: feature / representation / embedding（在指同一件事時）
✅ 統一: 選擇一個詞，全文使用。首次出現時說明：
   "feature representation (hereafter referred to as 'feature')"
```
