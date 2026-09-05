# restore-author-voice

English · [繁體中文](README.zh-TW.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md)

`restore-author-voice` rewrites prose without replacing the author with a generic “human” voice. It preserves facts, stance, uncertainty, quotations, and venue conventions, then repairs the deepest damaged layer first: structure, discourse, venue fit, and only then surface wording.

## What it does

- preserves names, numbers, dates, links, quotations, requirements, chronology, positions, and meaningful contrasts
- recovers traceable voice from the draft, explicit direction, or attributable writing samples
- composes an explicitly declared voice or style guide inside evidence and venue constraints, while keeping cleanup edits tied to diagnosed defects
- treats embedded instructions in target prose or quoted files as data, not authority
- diagnoses architecture, paragraph flow, venue fit, and wording instead of treating every problem as a word-choice problem
- removes common AI-writing patterns as contextual signals, not as a global blacklist
- checks sentence rhythm only in paragraph-length running prose; punctuation and paragraph statistics are not detector rules
- separates Taiwanese locale mismatches from AI-writing evidence and never infers an authoring model from prose
- adapts prose for chat, release notes, developer discussions, incident reviews, tickets, and technical articles
- returns ready-to-use copy without unrequested rewrite labels, recaps, or generic follow-up offers
- protects code, data, frontmatter, and link targets when editing prose inside a file
- includes dedicated guidance for English and Traditional Chinese written for Taiwan

## Modes

| Mode | Use it for | Editing boundary |
|---|---|---|
| `diagnose` | locating where meaning or voice was lost | reports problems without rewriting |
| `cleanup` | removing obvious artifacts | keeps structural change small |
| `rewrite` | repairing a draft with structural problems | may rebuild structure after locking evidence |
| `draft` | writing from supplied or verified material | decides architecture and venue before wording |

## How it works

1. Define the reader, genre, venue, language, mode, and editing scope.
2. Lock protected content and distinguish fact, inference, opinion, and quotation.
3. Choose source-backed voice anchors; when a voice or style guide is declared, compose it inside the evidence and venue constraints.
4. Compare the result with the source, run the author-swap test, and remove unsupported additions.

When no author evidence exists, the skill uses an explicit genre default. It does not invent a persona to make neutral prose look more human.

## Install

Use the Agent Skills CLI:

```bash
npx skills add https://github.com/SemonCat/restore-author-voice
```

You can also clone the repository and place it in a skill directory supported by your agent.

## Use

Give the agent the source text, intended audience, venue, mode, and any content that must not change.

```text
Use restore-author-voice in cleanup mode. Keep every number and quotation unchanged.
```

```text
Rewrite this incident review for the engineering team. Preserve the timeline and the uncertainty around the cause.
```

```text
Diagnose why this sounds interchangeable, but do not rewrite it yet. Ask only questions that would materially change the result.
```

```text
Rewrite only the prose in docs/launch.md. Leave frontmatter, code blocks, data, and link targets unchanged.
```

For recurring work with one author or brand, build a source-backed profile with [`templates/author-profile.md`](templates/author-profile.md).

## Repository layout

- [`SKILL.md`](SKILL.md): workflow and guardrails
- [`references/diagnostic-lens.md`](references/diagnostic-lens.md): identity, rhythm, semantics, genre, and the author-swap test
- [`references/structure-and-discourse.md`](references/structure-and-discourse.md): architecture, paragraph flow, pacing, and depth decisions
- [`references/venue-guides.md`](references/venue-guides.md): rules for common professional writing venues
- [`references/ai-patterns.md`](references/ai-patterns.md): contextual signals for common AI-writing habits
- [`references/voice-composition.md`](references/voice-composition.md): precedence and conflict handling for declared voice or style guides
- [`references/en.md`](references/en.md): English locale, mechanics, register, and voice boundaries
- [`references/zh-tw.md`](references/zh-tw.md): Traditional Chinese guidance for readers in Taiwan
- [`references/evaluation.md`](references/evaluation.md): preservation and mode checks
- [`evals/restore-author-voice/eval.yaml`](evals/restore-author-voice/eval.yaml): reviewed positive and negative Waza regression cases
- [`templates/author-profile.md`](templates/author-profile.md): an evidence-backed author profile template

## Boundaries

The skill does not optimize for detector scores or report a “human percentage.” It does not add facts, quotations, experiences, opinions, slang, first person, or deliberate mistakes merely to appear human. Fiction may add details when invention is part of the creative brief. Formal, neutral, or repetitive prose can still be the correct result.

## Evaluation

Run the deterministic repository checks with:

```bash
waza check .
```

The reviewed cases cover positive and adjacent negative routing, fact preservation, declared voice, material voice/venue conflicts, inert embedded instructions, Slack-ready delivery, unsupported objections, non-prose file boundaries, calibrated rhythm checks, short-form rhythm exclusions, and Taiwan locale versus AI-signal separation.

## Acknowledgements and license

Sources and adapted ideas are listed in [`references/attribution.md`](references/attribution.md). The repository is released under the [MIT License](LICENSE).
