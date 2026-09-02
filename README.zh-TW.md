# restore-author-voice

[English](README.md) · 繁體中文 · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md)

`restore-author-voice` 會改寫文字，但不會把作者換成一種通用的「人味」。它先保留事實、立場、不確定性、引用與場域慣例，再從最深的損壞層開始修復：篇章結構、段落推進、場域適配，最後才處理表面語句。

## 它會做什麼

- 保留姓名、數字、日期、連結、引用、需求、時間順序、立場與真正有意義的對比
- 從原稿、明確指示或可追溯的寫作樣本找回作者聲音
- 分別診斷篇章結構、段落推進、場域適配與措辭，不把所有問題都當成換字問題
- 把常見 AI 寫作模式視為依情境判斷的訊號，不當成全域禁詞表
- 依聊天訊息、release notes、開發討論、事故回顧、ticket 與技術文章調整寫法
- 預設只交付可直接使用的成稿，不自行加上改寫標籤、重複總結或泛用邀請句
- 改寫檔案內文時，保護 code、data、frontmatter 與 link targets
- 內建英文與台灣繁體中文的專用規則

## 模式

| 模式 | 適用情境 | 修改邊界 |
|---|---|---|
| `diagnose` | 找出意義或作者聲音在哪裡流失 | 只回報問題，不改寫 |
| `cleanup` | 清除明顯瑕疵 | 盡量不動結構 |
| `rewrite` | 修復有結構問題的草稿 | 鎖定證據後可以重建結構 |
| `draft` | 根據已提供或已查證的素材寫新稿 | 先決定篇章與場域，再處理措辭 |

## 它怎麼運作

1. 確認讀者、文類、場域、語言、模式與修改範圍。
2. 鎖定受保護內容，分清楚事實、推論、觀點與引用。
3. 選出有來源的聲音錨點，診斷最深的損壞層，再從結構一路修到措辭。
4. 對照原文、執行 author-swap test，並刪除沒有來源的新增內容。

沒有作者證據時，skill 會明確採用文類預設，不會為了讓中性文字看起來更像人而捏造人格。

## 安裝

使用 Agent Skills CLI：

```bash
npx skills add https://github.com/SemonCat/restore-author-voice
```

也可以 clone repo，再放進 agent 支援的 skill 目錄。

## 使用方式

提供原稿、目標讀者、場域、模式，以及不能改動的內容。

```text
用 restore-author-voice 的 cleanup 模式處理。所有數字與引用都不能改。
```

```text
把這份事故回顧改寫給工程團隊看。保留時間線，以及目前對原因仍不確定的部分。
```

```text
先診斷這段文字為什麼換誰署名都成立，但暫時不要改寫。只有答案會實質影響結果時才問問題。
```

```text
只改寫 docs/launch.md 的內文。frontmatter、code blocks、data 與 link targets 都不能動。
```

如果要長期處理同一位作者或品牌，可以用 [`templates/author-profile.md`](templates/author-profile.md) 建立有來源依據的 profile。

## Repo 結構

- [`SKILL.md`](SKILL.md)：工作流程與 guardrails
- [`references/diagnostic-lens.md`](references/diagnostic-lens.md)：身份、節奏、語意、文類與 author-swap test
- [`references/structure-and-discourse.md`](references/structure-and-discourse.md)：篇章結構、段落推進、節奏與修改深度
- [`references/venue-guides.md`](references/venue-guides.md)：常見專業寫作場域的規則
- [`references/ai-patterns.md`](references/ai-patterns.md)：常見 AI 寫作習慣的情境訊號
- [`references/en.md`](references/en.md)：英文地區慣例、標點、語域與聲音邊界
- [`references/zh-tw.md`](references/zh-tw.md)：給台灣讀者的繁體中文規則
- [`references/evaluation.md`](references/evaluation.md)：保真與模式驗收
- [`evals/restore-author-voice/eval.yaml`](evals/restore-author-voice/eval.yaml)：經人工檢視的 Waza 正向、負向回歸案例
- [`templates/author-profile.md`](templates/author-profile.md)：以證據為基礎的作者 profile 範本

## 邊界

這個 skill 不會迎合 detector 分數，也不會回報「人味百分比」。它不會為了看起來像人而自行加入事實、引用、經歷、觀點、俚語、第一人稱或故意犯錯。當創作 brief 本來就要求虛構時，fiction 可以新增細節。正式、中性或重複的文字仍可能是正確結果。

## 驗證

執行 repo 的 deterministic checks：

```bash
waza check .
```

經人工檢視的案例涵蓋正向 routing、相鄰負向 trigger、事實保真、可直接貼到 Slack 的成稿、沒有來源的反駁，以及檔案內非內文區塊的保護。

## 致謝與授權

來源與改寫後採用的概念列在 [`references/attribution.md`](references/attribution.md)。本 repo 使用 [MIT License](LICENSE) 開源。
