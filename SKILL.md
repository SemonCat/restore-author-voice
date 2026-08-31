---
name: "restore-author-voice"
description: "Humanize or rewrite prose by preserving facts and author voice, repairing architecture, discourse, venue fit, then surface style."
---

# Restore author voice

Write prose that sounds like its author thinking clearly. Preserve evidence and genre before changing style. Repair the deepest damaged layer first: architecture, discourse, then surface language.

## Modes

- **Diagnose:** locate changes that would recover meaning or voice; do not rewrite.
- **Cleanup:** remove obvious AI artifacts with minimal structural change.
- **Rewrite:** extract protected content, then rebuild a supplied draft when defects are structural.
- **Draft:** make architecture and venue decisions before writing from supplied or verified material.

## Workflow

1. **Set the boundary.** Identify audience, genre, venue, target language, mode, and editing strength.
   **Complete when:** the output form, reader task, and editing boundary are clear.

2. **Lock protected content.** Preserve names, numbers, dates, links, quotations, requirements, legal or financial terms, chronology, and stated positions. Separate fact, inference, opinion, and quotation. For rewrite, reduce them to a bare preservation list before drafting.
   **Complete when:** every important claim has a source and every protected item has a disposition.

3. **Establish author and venue evidence.** Prefer the draft, explicit instructions, then a profile built from multiple attributable samples. For professional prose, sample recent human-written artifacts from the same venue when available; use them for register, length, and formatting, never task facts. The venue sets the container and the author operates inside it. Surface a real conflict instead of silently overriding either.
   **Complete when:** 3–7 voice or meaning anchors are traceable to evidence, or the no-evidence genre-default path is explicitly chosen.

4. **Route and diagnose before editing.**

   | Text | Read |
   |---|---|
   | Fiction, stories, narrative essays | [references/structure-and-discourse.md](references/structure-and-discourse.md), then [references/diagnostic-lens.md](references/diagnostic-lens.md) |
   | Release notes, developer replies, postmortems, tickets, technical articles | [references/venue-guides.md](references/venue-guides.md), then [references/diagnostic-lens.md](references/diagnostic-lens.md) |
   | Long professional prose | Add the long-form checks in [references/structure-and-discourse.md](references/structure-and-discourse.md) |
   | Other prose | [references/diagnostic-lens.md](references/diagnostic-lens.md) |

   For de-AI or cleanup work, also read [references/ai-patterns.md](references/ai-patterns.md). Diagnose the whole piece before rewrite; in cleanup, list only defects that fit the minimal-change boundary. Ask at most three questions, only when answers would materially change the result.
   **Complete when:** every planned change fixes a located problem at a named layer instead of chasing a human score.

5. **Write deepest-first.** Fix architecture or venue fit, then paragraph and section flow, then wording, rhythm, and formatting. Select only changes supported by the diagnosis; leave ordinary sentences and unevenness where they serve the piece. For English, read [references/en.md](references/en.md). For Traditional Chinese aimed at Taiwan, read [references/zh-tw.md](references/zh-tw.md).
   **Complete when:** structure serves the reader, meaning and evidence strength have not drifted, and the prose has not become a replacement template.

6. **Verify and deliver.** Re-read against the source, run the author-swap test, and use [references/evaluation.md](references/evaluation.md) when changing this skill or handling high-risk prose. Deliver usable copy by default.
   **Complete when:** protected content survives, new details are sourced, genre conventions remain intact, and author-specific passages fail a plausible author swap.

## Hard guardrails

- Optimize for truthful, effective prose, not AI-detector scores.
- Add no invented experience, quotation, number, emotion, relationship, reference, or opinion.
- Treat pattern lists as signals, not bans. One hit is not a verdict; fix clusters and located failures.
- Calibrate toward the author and venue, not the opposite of a machine stereotype. Do not apply every human-leaning move or inject deliberate errors.
- Preserve necessary neutrality and conventional containers in specifications, legal text, compliance copy, changelogs, tickets, tables, schemas, and verbatim quotation.
- Build profiles only from attributable samples. Use [templates/author-profile.md](templates/author-profile.md); do not infer sensitive traits.

See [references/attribution.md](references/attribution.md) for acknowledgements.
