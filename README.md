# restore-author-voice

[繁體中文](README.zh-TW.md)

`restore-author-voice` is an agent skill for drafting and editing prose without replacing the author with a generic "human" voice. It repairs the deepest damaged layer first: architecture, discourse, venue fit, then surface language.

It treats style as evidence. A draft, explicit direction, or a set of attributable writing samples can show how an author makes claims, handles uncertainty, and moves through an argument. When that evidence is missing, the skill stays within the genre instead of inventing a persona.

## What it does

- drafts new prose from supplied or verified material
- rewrites while preserving facts, stance, uncertainty, quotations, and constraints
- diagnoses where editing erased useful authorship
- removes common AI-writing patterns without turning them into a global blacklist
- prefers literal wording when ornamental metaphor makes a sentence less precise
- repairs structural and paragraph-flow problems before polishing sentences
- matches prose to its venue, including chat, release notes, developer replies, postmortems, tickets, and technical articles
- returns ready-to-use copy without unrequested rewrite labels, editing notes, recaps, or generic follow-up offers
- removes unsupported defenses and discarded alternatives while preserving real objections and decision options
- protects code, data, frontmatter, and link targets when editing prose in a file
- applies language-specific guidance for English and Traditional Chinese used in Taiwan

The skill has four modes: `diagnose`, `cleanup`, `rewrite`, and `draft`. A cleanup should stay small. A rewrite can change the structure, but it still has to pass the same preservation checks.

## Why it works this way

Removing a few stock phrases does not recover an author's voice. It can leave a shorter draft with the same machine-shaped structure and still sound interchangeable.

This skill starts with source boundaries: what is fact, what is judgment, what remains uncertain, and which details cannot move. It then looks for author evidence in the wording and the material itself. The final author-swap test asks a blunt question: could the same passage appear under a plausible peer's name without changing anything?

That test is diagnostic, not a score. The skill does not optimize for AI detectors or report a "human percentage."

## Install

Use the Agent Skills CLI:

```bash
npx skills add https://github.com/SemonCat/restore-author-voice
```

Or clone the repository and place it in a skill directory supported by your agent.

## Use

Ask your agent to use `restore-author-voice`, then give it the draft or source material and the intended audience.

Examples:

```text
Use restore-author-voice in cleanup mode. Keep every number and quotation unchanged.
```

```text
Rewrite this incident review for the engineering team. Preserve the timeline and uncertainty around the cause.
```

```text
Draft a Traditional Chinese announcement for readers in Taiwan from these confirmed facts. Do not add a promotional conclusion.
```

For a recurring author or brand, start with [`templates/author-profile.md`](templates/author-profile.md). Build the profile from attributable samples, not guesses about personality.

## Repository layout

- [`SKILL.md`](SKILL.md): modes, workflow, and hard guardrails
- [`references/diagnostic-lens.md`](references/diagnostic-lens.md): identity, rhythm, semantics, genre, and the author-swap test
- [`references/structure-and-discourse.md`](references/structure-and-discourse.md): architecture, paragraph questions, pacing, and depth decisions
- [`references/venue-guides.md`](references/venue-guides.md): rules for common professional writing venues
- [`references/ai-patterns.md`](references/ai-patterns.md): diagnostic signals for common AI-writing habits
- [`references/en.md`](references/en.md): English locale, mechanics, register, and voice boundaries
- [`references/zh-tw.md`](references/zh-tw.md): Traditional Chinese guidance for readers in Taiwan
- [`references/evaluation.md`](references/evaluation.md): preservation and mode checks
- [`evals/restore-author-voice/eval.yaml`](evals/restore-author-voice/eval.yaml): reviewed positive and negative Waza regression cases
- [`templates/author-profile.md`](templates/author-profile.md): a source-backed profile template

## Boundaries

The skill does not invent experiences, opinions, emotions, sources, or biographical details. It does not add slang, fragments, first person, or deliberate mistakes to make prose look human. Formal, neutral, or repetitive writing can be the right result when the author and genre call for it.

## Acknowledgements and license

The diagnostic catalog draws on public work credited in [`references/attribution.md`](references/attribution.md). The repository is released under the [MIT License](LICENSE).
