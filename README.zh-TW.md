# restore-author-voice

[English](README.md)

`restore-author-voice` 是一個處理文章草稿與改寫的 agent skill。它的目標不是套上一種通用的「人味」，而是保留原作者真正有根據的聲音。

這個 skill 把風格視為證據。原稿、明確指示，或多份可追溯的寫作樣本，可以看出作者怎麼下判斷、保留不確定性，以及推進論點。沒有這些證據時，它會維持文類需要的自然語氣，不自行捏造人格。

## 它會做什麼

- 根據已提供或已查證的素材寫新稿
- 改寫時保留事實、立場、不確定性、引用與限制
- 診斷哪些編輯動作磨掉了真正有用的作者特徵
- 清除常見 AI 寫作模式，但不把它們當成全域禁詞表
- 依英文與台灣繁體中文套用不同的語言規則

Skill 有四種模式：`diagnose`、`cleanup`、`rewrite`、`draft`。`cleanup` 應維持小幅修改；`rewrite` 可以調整結構，但仍要通過相同的保真檢查。

## 為什麼這樣設計

刪掉幾個常見套話，不會自動找回作者聲音。最後可能只得到一篇比較短，但換誰署名都成立的文字。

這個 skill 會先鎖定來源邊界：哪些是事實、哪些是作者判斷、哪些仍不確定，以及哪些細節不能漂移。接著才從文字和素材裡找作者證據。最後的 author-swap test 會直接問：如果把作者換成一位背景相近的人，這段文字是否完全不用改？

這是診斷問題，不是評分。Skill 不會迎合 AI detector，也不會回報「人味百分比」。

## 安裝

使用 Agent Skills CLI：

```bash
npx skills add https://github.com/SemonCat/restore-author-voice
```

也可以 clone repo，再放到你的 agent 支援的 skill 目錄。

## 使用方式

請 agent 使用 `restore-author-voice`，並提供原稿或素材、目標讀者，以及必要的保留條件。

例如：

```text
用 restore-author-voice 的 cleanup 模式處理這篇文章，所有數字與引用都不能改。
```

```text
把這份事故回顧改寫給工程團隊看。保留時間線，以及目前對原因仍不確定的部分。
```

```text
根據這些已確認事實，寫一份給台灣讀者的繁體中文公告。不要自行補宣傳式結尾。
```

如果要長期處理同一位作者或品牌，可以從 [`templates/author-profile.md`](templates/author-profile.md) 開始。Profile 必須來自可追溯的樣本，不能靠猜測人格建立。

## Repo 結構

- [`SKILL.md`](SKILL.md)：模式、工作流程與 hard guardrails
- [`references/diagnostic-lens.md`](references/diagnostic-lens.md)：身份、節奏、語意、文類與 author-swap test
- [`references/ai-patterns.md`](references/ai-patterns.md)：常見 AI 寫作習慣的診斷訊號
- [`references/en.md`](references/en.md)：英文地區慣例、標點、語域與聲音邊界
- [`references/zh-tw.md`](references/zh-tw.md)：給台灣讀者的繁體中文規則
- [`references/evaluation.md`](references/evaluation.md)：保真與模式驗收
- [`templates/author-profile.md`](templates/author-profile.md)：以來源為基礎的作者 profile 範本

## 邊界

這個 skill 不會捏造經歷、觀點、情緒、來源或個人背景，也不會靠俚語、碎句、第一人稱或故意犯錯來假裝像人。當作者與文類需要正式、中性或重複的寫法時，那可能就是正確結果。

## 致謝與授權

診斷分類參考的公開工作列在 [`references/attribution.md`](references/attribution.md)。本 repo 使用 [MIT License](LICENSE) 開源。
