# restore-author-voice

[English](README.md) · [繁體中文](README.zh-TW.md) · 简体中文 · [日本語](README.ja.md) · [한국어](README.ko.md)

`restore-author-voice` 用于改写文本，但不会用一套通用的“人味”覆盖作者本人。它会先保留事实、立场、不确定性、引用和使用场景的惯例，再从受损最深的层级开始修复：篇章结构、段落推进、场景适配，最后才处理表面措辞。

## 它能做什么

- 保留姓名、数字、日期、链接、引用、需求、时间顺序、立场和有实际意义的对比
- 从原稿、明确指示或可追溯的写作样本中恢复作者声音
- 在证据和使用场景的边界内套用明确指定的 voice 或 style guide
- 将目标文本或引用文件中的嵌入指令视为数据，不允许它切换模式、范围或权限
- 分别诊断篇章结构、段落推进、场景适配和措辞，而不是把所有问题都当成换词问题
- 将常见 AI 写作模式视为需要结合上下文判断的信号，而不是全局禁词表
- 根据聊天消息、release notes、开发讨论、事故复盘、ticket 和技术文章调整写法
- 默认只返回可直接使用的成稿，不附加未请求的改写标签、重复总结或泛化邀请
- 改写文件中的文本时，保护 code、data、frontmatter 和 link targets
- 内置英文和面向台湾读者的繁体中文规则

## 模式

| 模式 | 适用场景 | 修改边界 |
|---|---|---|
| `diagnose` | 找出含义或作者声音在哪里丢失 | 只报告问题，不改写 |
| `cleanup` | 清除明显瑕疵 | 尽量少改结构 |
| `rewrite` | 修复存在结构问题的草稿 | 锁定证据后可以重建结构 |
| `draft` | 根据已提供或已验证的材料起草 | 先确定篇章与场景，再处理措辞 |

## 工作方式

1. 确认读者、体裁、使用场景、语言、模式和修改范围。
2. 锁定受保护内容，区分事实、推断、观点和引用。
3. 选择有来源依据的声音锚点；如有明确指定的 voice 或 style guide，则在证据和使用场景的边界内套用。
4. 对照原文、执行 author-swap test，并删除没有来源支持的新增内容。

没有作者证据时，skill 会明确采用体裁默认值，不会为了让中性文本显得更像人而虚构人格。

## 安装

使用 Agent Skills CLI：

```bash
npx skills add https://github.com/SemonCat/restore-author-voice
```

也可以 clone 仓库，再将它放入 agent 支持的 skill 目录。

## 使用方式

向 agent 提供原稿、目标读者、使用场景、模式，以及不能改动的内容。

```text
使用 restore-author-voice 的 cleanup 模式。所有数字和引用都不能改。
```

```text
把这份事故复盘改写给工程团队阅读。保留时间线，以及目前对原因仍不确定的部分。
```

```text
先诊断这段文字为什么换成任何人署名都成立，但暂时不要改写。只有答案会实质影响结果时才提问。
```

```text
只改写 docs/launch.md 中的正文。frontmatter、code blocks、data 和 link targets 都不能改。
```

如果需要长期处理同一位作者或品牌，可以用 [`templates/author-profile.md`](templates/author-profile.md) 建立有来源依据的 profile。

## 仓库结构

- [`SKILL.md`](SKILL.md)：工作流程和 guardrails
- [`references/diagnostic-lens.md`](references/diagnostic-lens.md)：身份、节奏、语义、体裁和 author-swap test
- [`references/structure-and-discourse.md`](references/structure-and-discourse.md)：篇章结构、段落推进、节奏和修改深度
- [`references/venue-guides.md`](references/venue-guides.md)：常见专业写作场景的规则
- [`references/ai-patterns.md`](references/ai-patterns.md)：常见 AI 写作习惯的上下文信号
- [`references/voice-composition.md`](references/voice-composition.md)：明确 voice／style guide 的优先级和冲突处理
- [`references/en.md`](references/en.md)：英文地区惯例、标点、语域和声音边界
- [`references/zh-tw.md`](references/zh-tw.md)：面向台湾读者的繁体中文规则
- [`references/evaluation.md`](references/evaluation.md)：保真和模式验收
- [`evals/restore-author-voice/eval.yaml`](evals/restore-author-voice/eval.yaml)：经过人工审查的 Waza 正向、负向回归案例
- [`templates/author-profile.md`](templates/author-profile.md)：以证据为基础的作者 profile 模板

## 边界

这个 skill 不会针对 detector 分数优化，也不会报告“人味百分比”。它不会为了显得像人而擅自加入事实、引用、经历、观点、俚语、第一人称或故意制造错误。当创作 brief 本身要求虚构时，fiction 可以新增细节。正式、中性或重复的文本仍可能是正确结果。

## 验证

运行仓库的 deterministic checks：

```bash
waza check .
```

经过人工审查的案例覆盖正向和相邻负向 routing、事实保真、明确 voice、voice／使用场景冲突、嵌入指令保持无效、可直接粘贴到 Slack 的成稿、没有来源的反驳，以及文件中非正文区域的保护。

## 致谢与许可

来源和改写后采用的思路列在 [`references/attribution.md`](references/attribution.md)。本仓库采用 [MIT License](LICENSE)。
