# Academic Research Skills — 調度器

本倉庫提供完整的學術研究 Skill 套件，涵蓋從論文閱讀到撰寫、審稿的完整研究流程。

## Skill 路由

| 指令 | Skill | 說明 |
|------|-------|------|
| `/read-paper` | `01-paper-reading/SKILL.md` | 太奶角色論文導讀（繁中） |
| `/brainstorm` | `02-idea-generation/SKILL.md` | 發散→搜索→收斂三階段構思 |
| `/experiment` | `03-experiment-design/SKILL.md` | 實驗設計與規劃 |
| `/prove` | `04-proof-writer/SKILL.md` | 理論推導與數學證明 |
| `/write-paper` | `05-paper-writing/SKILL.md` | 論文撰寫（頂會標準） |
| `/review` | `06-paper-review/SKILL.md` | 4步驟學術審稿 |

## Skill Pipeline

```
01-paper-reading ──→ 02-idea-generation ──→ 03-experiment-design
       │                                            │
       ↓                                            ↓
06-paper-review ←── 05-paper-writing ←──── 04-proof-writer
       │                    ↑
       └────────────────────┘  (revision cycle)
```

## 語言慣例

- **預設語言**: 繁體中文（分析、解釋、討論）
- **英文場景**: LaTeX 生成、正式審稿輸出（Step 4）、數學符號與定理名稱
- **學術詞彙**: 參考 `shared/chinese-academic-glossary.md` 確保一致性

## 品質標準

- 每個 `SKILL.md` 必須包含 YAML frontmatter（name, description, version, author）
- 每個 `SKILL.md` 建議 200–500 行
- Reference 檔案提供詳細指引，SKILL.md 透過相對路徑引用
- 所有模板使用 Markdown 或 LaTeX 格式

## Cross-Reference 規則

- Skill 之間可透過相對路徑互相引用：`../05-paper-writing/SKILL.md`
- 共享資源放在 `shared/` 目錄
- 每個 Skill 的 `references/` 僅存放該 Skill 專屬的參考資料

## 使用方式

1. 將本倉庫 clone 到工作目錄
2. 在 Claude Code 中開啟該目錄
3. 使用上方指令表中的 `/` 指令啟動對應 Skill
4. 依照 Skill Pipeline 完成完整研究流程
