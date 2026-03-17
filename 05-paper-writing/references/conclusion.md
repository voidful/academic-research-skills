# Conclusion 結論寫作指南

## 核心原則

結論是讀者（和 reviewer）閱讀的最後一個部分。它的功能不是重複前文，而是提煉出最核心的 takeaway，並誠實地討論限制和展望。好的結論讓 reviewer 帶著正面印象結束閱讀；壞的結論讓人覺得虎頭蛇尾。

---

## 三段式結構

### 第 1 段：總結貢獻（Summary）

用 3-5 句話回顧論文的核心內容。注意：是**提煉重點**，不是**逐章複述**。

```latex
\section{Conclusion}
\label{sec:conclusion}

We presented SparseRecon, a coarse-to-fine framework for
high-quality 3D reconstruction from sparse input views.
Our key insight is that an explicit, even coarse, geometric
proxy provides strong structural guidance that enables
neural implicit representations to produce coherent results
in unobserved regions. Through a geometry-conditioned
refinement module, our method adaptively focuses
representational capacity on geometrically complex areas.
Experiments on three benchmarks demonstrate consistent
improvements over existing methods, with an average gain
of 2.3~dB PSNR using only 3 input views.
```

**要點**：
- 第一句重述方法名稱和核心任務
- 第二句回顧核心 insight（不是技術細節）
- 最後一句用數字總結最重要的結果
- 不要引入任何新資訊

### 第 2 段：Limitations（限制）

**為什麼要寫 Limitations？**

1. **誠實性**：reviewer 會更尊重誠實面對限制的作者
2. **預防質疑**：主動承認限制比被 reviewer 指出要好得多
3. **頂會要求**：NeurIPS 2021 起明確要求 broader impact 和 limitations

```latex
\paragraph{Limitations.}
Our method has several limitations.
First, the cost-volume-based geometry estimation assumes
approximate Lambertian reflectance, leading to degraded
performance on highly specular surfaces such as glass and
metal (\cref{fig:failure}a).
Second, our depth sampling strategy uses a fixed number
of hypotheses ($D = 128$), which may be insufficient for
scenes with large depth ranges.
Third, while our method is significantly faster than
per-scene optimization approaches, the stereo network
adds approximately 30\% overhead compared to direct
neural rendering methods.
```

**注意事項**：
- 限制必須是**真實的、具體的**
- 不要故意寫「假限制」來顯示你有想過
- 不要寫你已經解決的問題（"A limitation is X, but we address it by..."）
- 每個限制最好附帶一個可能的解決方向

### 第 3 段：Future Work（未來工作）

**好的 future work** 從 limitations 自然延伸出來：

```latex
\paragraph{Future Work.}
Several promising directions emerge from this work.
Integrating material-aware rendering~\cite{ref} could
address the specular surface limitation.
Adaptive depth sampling strategies~\cite{ref2} may
improve efficiency and quality for scenes with varying
depth complexity.
Beyond reconstruction, our coarse-to-fine geometric
reasoning framework may benefit other sparse-view tasks
such as semantic segmentation and object detection,
which we plan to explore in future work.
```

**注意事項**：
- 要具體，不要寫 "We will improve our method in the future"
- 每個方向最好引用一篇相關論文，表示可行性
- 2-3 個方向即可，不要列太多
- 至少有一個方向超越當前問題，展示更廣泛的影響

---

## 不要引入新資訊

結論中最常見的錯誤是引入前文沒有的新資訊：

```latex
% ❌ 引入了新的實驗結果
In conclusion, our method also works well on
indoor scenes (achieving 28.1 dB on ScanNet).

% ❌ 引入了新的方法細節
We note that adding a discriminator loss further
improves the visual quality.

% ❌ 引入了新的 claim
Our framework can be easily extended to video
reconstruction, achieving real-time performance.

% ✅ 只總結前文已有的內容
Our experiments demonstrate consistent improvements
across three benchmarks, validating the effectiveness
of explicit geometric guidance for sparse-view
reconstruction.
```

**黃金法則**：結論中的每一句話都應該能在前文找到對應的內容。

---

## 長度建議

| 會議 | 結論建議長度 | 備註 |
|------|-----------|------|
| NeurIPS/ICML/ICLR | 0.3-0.5 頁 | 簡潔為上 |
| CVPR/ECCV | 0.3-0.5 頁 | 可以稍短 |
| ACL/EMNLP | 0.3-0.5 頁 | 通常包含 ethical considerations |
| AAAI | 0.25-0.3 頁 | 版面緊張，盡量精簡 |

**通用建議**：結論不應超過半頁。如果你寫了超過半頁，幾乎一定包含了不必要的重複或新資訊。

---

## Broader Impact（社會影響）

部分會議（如 NeurIPS）要求或鼓勵討論 broader impact：

```latex
\paragraph{Broader Impact.}
Our work on sparse-view 3D reconstruction has potential
applications in reducing the data acquisition cost for
3D content creation, making 3D capture more accessible.
However, improved reconstruction technology could also
be misused for unauthorized 3D scanning of private
spaces or for creating deepfake 3D content. We encourage
the community to develop appropriate safeguards alongside
technical advances.
```

**位置**：通常放在 Conclusion 最後，或作為獨立的 section。

---

## 完整範例

```latex
\section{Conclusion}
\label{sec:conclusion}

We presented SparseRecon, a coarse-to-fine framework for
3D reconstruction from sparse input views. By introducing
an explicit geometry proxy as structural guidance, our
method overcomes the ill-posed nature of sparse-view
reconstruction, producing coherent and detailed results
in both observed and unobserved regions. Extensive
experiments on DTU, BlendedMVS, and Tanks\&Temples
demonstrate that SparseRecon consistently outperforms
existing methods, achieving an average improvement of
2.3~dB PSNR while using only 3 input views.

\paragraph{Limitations.}
Our method assumes approximately Lambertian surfaces and
may produce artifacts on highly specular objects. The
fixed depth sampling resolution ($D = 128$) can be
suboptimal for scenes with extreme depth variation.
Additionally, our approach requires known camera poses,
limiting its applicability in fully uncalibrated settings.

\paragraph{Future Work.}
Promising extensions include integrating material-aware
rendering to handle non-Lambertian surfaces, adopting
adaptive depth sampling for improved efficiency, and
jointly estimating camera poses to remove the calibration
requirement. We also plan to explore the application of
our geometric reasoning framework to downstream tasks
such as sparse-view semantic understanding.
```

---

## 自我檢查清單

```
□ 是否用 3-5 句話總結了核心貢獻？
□ 是否提到了最重要的數字結果？
□ 是否列出了 2-3 個真實的 limitations？
□ Limitations 是否具體而非籠統？
□ 是否列出了 2-3 個 future work 方向？
□ Future work 是否從 limitations 自然延伸？
□ 是否沒有引入新資訊？
□ 總長度是否控制在半頁以內？
□ 是否需要 broader impact 段落？
```

---

*回到主文件 → `../SKILL.md`*
