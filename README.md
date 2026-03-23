# Academic Research Skills

一套完整的學術研究 Skill 套件，符合 [Agent Skills 開放標準](https://agentskills.io/specification)。支援 **Claude Code**、**ChatGPT / Codex CLI**、**Gemini CLI**。

## Usage  
Claude Code: `git clone <repo> ~/.claude/skills/academic-research` 

ChatGPT/Codex CLI: `git clone <repo> ~/.codex/skills/academic-research` 

Gemini CLI: `git clone <repo> ~/.gemini/skills/academic-research` 

## 功能總覽

| # | Skill | 說明 |
|---|-------|------|
| 01 | Paper Reading | 太奶角色論文導讀，繁中敘事風格 |
| 02 | Idea Generation | 發散→搜索→收斂三階段構思 |
| 03 | Experiment Design | 假設→變數→指標→Baseline→Ablation |
| 04 | Proof Writer | 理論推導與 LaTeX 數學證明 |
| 05 | Paper Writing | 頂會標準論文撰寫 |
| 06 | Paper Review | 4步驟學術審稿流程 |
| 07 | Professor Fit Analyser | 教授適配度分析與申請策略 |

## 研究流程 Pipeline

```
教授分析 ─┐
   07     ↓
閱讀論文 → 發想 Idea → 設計實驗 → 理論推導 → 撰寫論文 → 審稿修改
   01          02          03          04          05         06
                                                    ↑          │
                                                    └──────────┘
                                                   (revision cycle)
```

## 安裝與使用

本套件支援三大 AI agent 平台。選擇你使用的平台，將倉庫 clone 到對應的 skills 目錄即可。

### Claude Code

```bash
# 使用者層級（全域可用）
git clone <repo-url> ~/.claude/skills/academic-research

# 專案層級（僅該專案可用）
git clone <repo-url> .claude/skills/academic-research
```

在 Claude Code 中使用 `/` 指令：

```
/read-paper          # 開始導讀一篇論文
/brainstorm          # 從論文出發發想新 Idea
/experiment          # 設計實驗方案
/prove               # 撰寫數學證明
/write-paper         # 撰寫論文各章節
/review              # 審稿一篇論文
/prof-fit            # 分析教授適配度
```

### ChatGPT / Codex CLI

```bash
# 使用者層級
git clone <repo-url> ~/.codex/skills/academic-research

# 專案層級
git clone <repo-url> .codex/skills/academic-research
```

Skills 會自動被偵測。可透過 `@academic-research` 提及來啟用，或讓 agent 根據任務自動匹配。

### Gemini CLI

```bash
# 使用者層級
git clone <repo-url> ~/.gemini/skills/academic-research

# 專案層級
git clone <repo-url> .gemini/skills/academic-research
```

Skills 會透過 `activate_skill` 機制自動匹配使用者意圖。

### 通用方式

將本倉庫目錄複製到你的 AI agent 的 skills 目錄即可。根目錄 `SKILL.md` 作為入口，agent 會透過 `*/SKILL.md` 模式自動發現所有子 skills。

## 目錄結構

```
├── SKILL.md                     # 根入口（monorepo skill，路由到子 skills）
├── CLAUDE.md                    # Claude Code 調度器（定義 / 指令路由）
├── paper-reading/               # 論文導讀
│   ├── SKILL.md
│   └── references/
├── idea-generation/             # Idea 發想
│   ├── SKILL.md
│   └── references/
├── experiment-design/           # 實驗設計
│   ├── SKILL.md
│   ├── references/
│   └── templates/
├── proof-writer/                # 理論證明
│   ├── SKILL.md
│   └── references/
├── paper-writing/               # 論文撰寫
│   ├── SKILL.md
│   └── references/
├── paper-review/                # 學術審稿
│   ├── SKILL.md
│   ├── references/
│   └── templates/
├── professor-fit-analyser/      # 教授適配度分析
│   ├── SKILL.md
│   ├── references/
│   └── templates/
└── shared/                      # 共享資源
    ├── chinese-academic-glossary.md
    ├── conference-standards.md
    └── researcher-philosophies.md
```

## 語言說明

- 分析、解釋、討論：繁體中文
- LaTeX 輸出、正式審稿：英文
- 數學符號與定理：英文

## 設計參考

- [Agent Skills 開放標準](https://agentskills.io/specification)
- [Orchestra-Research/AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs)
- [Master-cai/Research-Paper-Writing-Skills](https://github.com/Master-cai/Research-Paper-Writing-Skills)

## License

MIT
