# Academic Research Skills for Claude Code

一套完整的學術研究 Skill 套件庫，供 Claude Code 使用。涵蓋從論文閱讀到撰寫、審稿的完整研究流程。

## 功能總覽

| # | Skill | 指令 | 說明 |
|---|-------|------|------|
| 01 | Paper Reading | `/read-paper` | 太奶角色論文導讀，繁中敘事風格 |
| 02 | Idea Generation | `/brainstorm` | 發散→搜索→收斂三階段構思 |
| 03 | Experiment Design | `/experiment` | 假設→變數→指標→Baseline→Ablation |
| 04 | Proof Writer | `/prove` | 理論推導與 LaTeX 數學證明 |
| 05 | Paper Writing | `/write-paper` | 頂會標準論文撰寫 |
| 06 | Paper Review | `/review` | 4步驟學術審稿流程 |

## 研究流程 Pipeline

```
閱讀論文 → 發想 Idea → 設計實驗 → 理論推導 → 撰寫論文 → 審稿修改
   01          02          03          04          05         06
                                                    ↑          │
                                                    └──────────┘
                                                   (revision cycle)
```

## 安裝與使用

### 方法一：直接 Clone

```bash
git clone <repo-url> ~/research-skills
cd ~/research-skills
# 在 Claude Code 中開啟此目錄即可使用
```

### 方法二：加入現有專案

```bash
# 將本倉庫作為子目錄加入你的研究專案
cp -r <repo-path> ./research-skills/
```

### 使用方式

在 Claude Code 中使用 `/` 指令：

```
/read-paper          # 開始導讀一篇論文
/brainstorm          # 從論文出發發想新 Idea
/experiment          # 設計實驗方案
/prove               # 撰寫數學證明
/write-paper         # 撰寫論文各章節
/review              # 審稿一篇論文
```

## 目錄結構

```
├── CLAUDE.md                    # 調度器（定義路由與規則）
├── 01-paper-reading/            # 論文導讀
│   ├── SKILL.md
│   └── references/
├── 02-idea-generation/          # Idea 發想
│   ├── SKILL.md
│   └── references/
├── 03-experiment-design/        # 實驗設計
│   ├── SKILL.md
│   ├── references/
│   └── templates/
├── 04-proof-writer/             # 理論證明
│   ├── SKILL.md
│   └── references/
├── 05-paper-writing/            # 論文撰寫
│   ├── SKILL.md
│   ├── references/
│   └── templates/
├── 06-paper-review/             # 學術審稿
│   ├── SKILL.md
│   ├── references/
│   └── templates/
└── shared/                      # 共享資源
```

## 語言說明

- 分析、解釋、討論：繁體中文
- LaTeX 輸出、正式審稿：英文
- 數學符號與定理：英文

## 設計參考

- [Orchestra-Research/AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs)
- [Master-cai/Research-Paper-Writing-Skills](https://github.com/Master-cai/Research-Paper-Writing-Skills)

## License

MIT
