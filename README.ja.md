# restore-author-voice

[English](README.md) · [繁體中文](README.zh-TW.md) · [简体中文](README.zh-CN.md) · 日本語 · [한국어](README.ko.md)

`restore-author-voice` は、文章を誰にでも当てはまる「人間らしい文体」に置き換えず、書き手自身の声を保ったまま書き直すための skill です。事実、立場、不確実性、引用、媒体ごとの慣習を先に固定し、構成、論理の流れ、媒体との適合、表現の順に、問題の深い層から修復します。

## できること

- 人名、数値、日付、リンク、引用、要件、時系列、立場、意味のある対比を保持する
- 原稿、明示された指示、出典を確認できる文章サンプルから書き手の声を復元する
- すべてを言い換えの問題にせず、構成、段落の流れ、媒体との適合、表現を分けて診断する
- AI らしい表現パターンを一律の禁止語ではなく、文脈に応じて判断する手掛かりとして扱う
- チャット、release notes、開発者間の議論、インシデントレビュー、ticket、技術記事に合わせて文体を調整する
- 頼まれていない見出し、要約、追加提案を付けず、そのまま使える文章を返す
- ファイル内の文章を編集するとき、code、data、frontmatter、link targets を変更しない
- 英語と台湾向け繁体字中国語の専用ガイドを含む

## モード

| モード | 用途 | 編集範囲 |
|---|---|---|
| `diagnose` | 意味や書き手の声が失われた箇所を特定する | 問題を報告し、書き直さない |
| `cleanup` | 明らかな不自然さを取り除く | 構造変更を最小限にする |
| `rewrite` | 構造に問題がある原稿を修復する | 根拠を固定した後で構造を組み直せる |
| `draft` | 提供済み、または確認済みの素材から起草する | 表現より先に構成と媒体を決める |

## 仕組み

1. 読者、ジャンル、媒体、言語、モード、編集範囲を決めます。
2. 保護する内容を固定し、事実、推論、意見、引用を区別します。
3. 根拠のある文体上の手掛かりを選び、最も深い問題を診断して、構成から表現へ順に修正します。
4. 原文と照合し、author-swap test を行い、根拠のない追加を削除します。

書き手を示す根拠がない場合は、ジャンルに合った標準的な文体を明示的に使います。中立的な文章を人間らしく見せるために人格を作りません。

## インストール

Agent Skills CLI を使います。

```bash
npx skills add https://github.com/SemonCat/restore-author-voice
```

リポジトリを clone し、agent が対応する skill ディレクトリへ配置することもできます。

## 使い方

原文、想定読者、媒体、モード、変更してはいけない内容を agent に渡します。

```text
restore-author-voice を cleanup モードで使ってください。数値と引用は一切変更しないでください。
```

```text
このインシデントレビューをエンジニアリングチーム向けに書き直してください。時系列と、原因がまだ確定していない点を保持してください。
```

```text
この文章が誰の名前でも成立してしまう理由を診断してください。まだ書き直さず、答えによって結果が変わる質問だけをしてください。
```

```text
docs/launch.md の本文だけを書き直してください。frontmatter、code blocks、data、link targets は変更しないでください。
```

同じ書き手やブランドの文章を継続して扱う場合は、[`templates/author-profile.md`](templates/author-profile.md) を使い、根拠に基づく profile を作成できます。

## リポジトリ構成

- [`SKILL.md`](SKILL.md): ワークフローと guardrails
- [`references/diagnostic-lens.md`](references/diagnostic-lens.md): identity、rhythm、semantics、genre、author-swap test
- [`references/structure-and-discourse.md`](references/structure-and-discourse.md): 構成、段落の流れ、ペース、編集の深さ
- [`references/venue-guides.md`](references/venue-guides.md): 主な業務文書ごとのルール
- [`references/ai-patterns.md`](references/ai-patterns.md): AI らしい文章に見られるパターンを判断するための手掛かり
- [`references/en.md`](references/en.md): 英語の地域差、表記、語調、voice の境界
- [`references/zh-tw.md`](references/zh-tw.md): 台湾向け繁体字中国語のガイド
- [`references/evaluation.md`](references/evaluation.md): 内容保持とモードの確認項目
- [`evals/restore-author-voice/eval.yaml`](evals/restore-author-voice/eval.yaml): レビュー済みの Waza 正例・負例テスト
- [`templates/author-profile.md`](templates/author-profile.md): 根拠に基づく author profile テンプレート

## 境界

この skill は detector のスコアを最適化せず、「人間らしさの割合」も出しません。人間らしく見せるためだけに、事実、引用、経験、意見、俗語、一人称、意図的な誤りを追加しません。創作 brief に発明が含まれる場合、fiction ではその範囲内で詳細を追加できます。形式的、中立的、反復のある文章が正しい場合もあります。

## 評価

リポジトリの deterministic checks を実行します。

```bash
waza check .
```

レビュー済みのケースは、正しい routing、隣接する負例 trigger、事実の保持、Slack にそのまま貼れる出力、根拠のない反論、ファイル内の本文以外の領域を対象にしています。

## 謝辞とライセンス

参照元と取り入れた考え方は [`references/attribution.md`](references/attribution.md) に記載しています。このリポジトリは [MIT License](LICENSE) で公開されています。
