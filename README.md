# PotetoCraft

[English](#english) · [繁體中文](#繁體中文)

## English

PotetoCraft is a plugin for coding agents (Claude Code and Codex). It gives the agent one way of working: classify the task, follow the matching playbook, keep a todo list, and verify against the real artifact before reporting. The agent does local, reversible work on its own. It stops and hands anything outward (commit, push, PR, merge, posting, messages, tickets) or destructive back to you as a draft.

### A tribute to pstack

PotetoCraft is inspired by [pstack](https://github.com/cursor/plugins/tree/main/pstack), the workflow plugin by [poteto](https://github.com/poteto) (Lauren Tan), released under the MIT license. pstack showed that an agent goes faster when it goes deep first: name the data shape, read before changing, prove the work, and write plainly. PotetoCraft keeps that way of working and rewrites it in our own words for a narrower set of guardrails. pstack's license notice is kept in [NOTICE](NOTICE). Thank you, poteto.

What PotetoCraft changes from pstack:

- Subagents run on one model at a fixed effort (`opus`, `medium` in Claude Code). No multi-model panels.
- No outward action without the user. The agent prepares commits, PR descriptions, and review comments as drafts and waits.
- No scripts, no downloads, no global configuration writes, no cleanup flows that delete files.
- A smaller first release that focuses on the core loop, review, explanation, and design.

### Skills

| Skill | Invoke | What it does |
| --- | --- | --- |
| `poteto-mode` | you type it | The main workflow. Picks a playbook (investigation, bug fix, feature, refactoring, perf issue, prototype, PR review), applies engineering principles, verifies, and ends with a hand-off report. |
| `review` | you or the agent | Reviews a diff or PR for correctness, blast radius, design, tests, and comments. Report only. |
| `explain` | you or the agent | Explains how code works and why it is that way, from the code and local git history. |
| `design` | you or the agent | Sketches data shapes, types, and module boundaries before code, with options and tradeoffs. |
| `tdd` | you or the agent | Red, green, refactor when a cheap test target exists. |
| `sharpen` | you, or poteto-mode | Restates the goal and approach before any work starts. |
| `catch-up` | you, or poteto-mode | Summarizes what changed and lists what is waiting on you. |
| `correct` | you, or poteto-mode | Finds mistakes agents keep repeating in a repo and proposes structural fixes in the working tree. |

In Claude Code the skills carry the plugin prefix, for example `/potetocraft:poteto-mode`.

### Install

Claude Code:

```
/plugin marketplace add pkyosx/PotetoCraft
/plugin install potetocraft@potetocraft
```

Codex:

```
codex plugin marketplace add pkyosx/PotetoCraft
codex plugin add potetocraft@potetocraft
```

To pin a version, add the marketplace at a tag (`--ref <tag>` for Codex, `pkyosx/PotetoCraft#<tag>` for Claude Code). Installed copies are cached by version number, so every release bumps the version in both manifests.

### License

MIT. See [LICENSE](LICENSE). pstack attribution is in [NOTICE](NOTICE).

## 繁體中文

PotetoCraft 是給程式開發 agent（Claude Code 與 Codex）使用的外掛。它讓 agent 用同一套方式工作：先判斷工作類型，套用對應的 playbook，列出待辦，並在回報前用實際產物驗證結果。本機、可復原的工作由 agent 自己完成；commit、push、PR、merge、留言、發訊息、建 ticket 這類對外動作，以及刪除，一律整理成草稿交給你決定。

### 向 pstack 致敬

PotetoCraft 參考了 [poteto](https://github.com/poteto)（Lauren Tan）的工作流程外掛 [pstack](https://github.com/cursor/plugins/tree/main/pstack)（MIT 授權）。pstack 的核心想法是「想走得快，先走得深」：先定資料結構、先讀懂再修改、證明成果真的可行、用平實的文字寫作。PotetoCraft 保留這套工作方式，並依照較嚴格的使用規範，用我們自己的文字重新撰寫；pstack 的授權聲明保留在 [NOTICE](NOTICE)。謝謝 poteto。

PotetoCraft 和 pstack 的差異：

- sub-agent 一律用同一個模型與固定 effort（Claude Code 中為 `opus`、`medium`），不做多模型比較。
- 沒有使用者同意，不做任何對外動作。commit、PR 描述、review 留言都先寫成草稿，等你指示。
- 不附任何腳本，不下載外部程式，不寫全域設定，沒有會刪除檔案的清理流程。
- 第一版只做核心：主流程、review、解釋與設計。

### Skill 一覽

| Skill | 觸發方式 | 用途 |
| --- | --- | --- |
| `poteto-mode` | 由你輸入 | 主流程。選擇 playbook（調查、修 bug、新功能、重構、效能、原型、PR review），套用工程原則、實際驗證，最後產出交付報告。 |
| `review` | 你或 agent | 審查 diff 或 PR 的正確性、影響範圍、設計、測試與註解，只產出報告。 |
| `explain` | 你或 agent | 從程式碼與本機 git 歷史，說明程式怎麼運作、為什麼這樣設計。 |
| `design` | 你或 agent | 寫程式前先畫出資料結構、型別與模組邊界，列出選項與取捨。 |
| `tdd` | 你或 agent | 有便宜的測試目標時，依紅、綠、重構的順序開發。 |
| `sharpen` | 你，或由 poteto-mode 引導 | 開工前先用自己的話重述目標與做法。 |
| `catch-up` | 你，或由 poteto-mode 引導 | 整理目前的進度，列出等你決定的事項。 |
| `correct` | 你，或由 poteto-mode 引導 | 找出 agent 在 repo 裡反覆犯的錯，在工作目錄提出結構性的修正。 |

在 Claude Code 中，skill 名稱會帶外掛前綴，例如 `/potetocraft:poteto-mode`。

### 安裝

Claude Code：

```
/plugin marketplace add pkyosx/PotetoCraft
/plugin install potetocraft@potetocraft
```

Codex：

```
codex plugin marketplace add pkyosx/PotetoCraft
codex plugin add potetocraft@potetocraft
```

要固定版本時，請加上 tag（Codex 用 `--ref <tag>`，Claude Code 用 `pkyosx/PotetoCraft#<tag>`）。安裝後的內容依版本號存放，所以每次發布都要更新兩份 manifest 的版本號。

### 授權

MIT，見 [LICENSE](LICENSE)。pstack 的授權聲明見 [NOTICE](NOTICE)。
