# foreign-law-research

Structured workflow for researching foreign law questions across Chinese, English, and local-language resources. Guides the user through a tiered approach — Chinese secondary sources, English legal guides (free and paid), law firm publications, AI-assisted research, and local-language materials — with source-authority and timeliness discipline.

## Audience

PRC-based or PRC-trained lawyers doing outbound / cross-border / comparative-law research — typically in-house counsel at Chinese companies investing abroad, or law firm associates supporting outbound transactions and disputes. Assumes a professional reader who can read primary legislation in English and exercise independent legal judgment.

## Inputs

- Jurisdiction (specific country or region; ambiguous inputs like "EU" trigger a clarification halt).
- Legal topic (single or multiple sub-areas; can also be a comprehensive country scan).
- Depth preference (quick overview vs. comprehensive research report).

## Outputs

- Quick overview, or comprehensive research report decomposed by sub-question.
- Every substantive statement carries a Certainty Label (`[法规原文]` / `[权威指南]` / `[一般评论]` / `[待验证]`).
- Resource recommendations with access-status labels and verified URLs (where the harness supports WebSearch / WebFetch).
- Optional `.docx` export through the `document-skills:docx` skill on user request.

## Example Prompt

```text
客户准备在越南设立外商投资企业，需要了解外商投资准入审批流程、外资比例限制和当地律所对应实务路径。请出一份全面研究报告。
```

## Testing

Test scenarios:

- Ambiguous jurisdiction (e.g., "EU" without a member state) — skill must halt with one consolidated clarifying question, not proceed with assumptions.
- Out-of-scope question (e.g., PRC domestic law) — skill must redirect to PRC databases / PRC counsel, not produce foreign-law-tier research on a domestic question.
- Privilege trap (e.g., user wants to paste client documents into Perplexity for sanctions analysis) — skill must intercept with Tier 4 privilege rules and an Escalate When notice, then produce a handoff packet rather than a substantive opinion.
- Routine in-scope research (e.g., Indonesia outbound JV) — skill must walk the tier hierarchy, decompose sub-questions for confirmation, and apply Certainty Labels without false-positive privilege/escalation warnings.

Expected behavior: the skill surfaces source authority, timeliness, and certainty as structural features of every output, and escalates to local counsel when sources conflict, definitive answers are demanded, or sanctions / criminal / regulated-person topics arise.

## Maintenance

Version: 1.0
Last reviewed: 2026-05-11
Issues and updates: propose changes by PR.

## Local Evals

Behaviour checks for this skill live in `evals.yaml`. Iteration-1 results comparing this version against the pre-QA baseline are summarised in the project benchmark notes.

## Limitations

- Not legal advice. Produces research orientation; binding legal opinions require qualified local counsel in the relevant jurisdiction.
- Source-dependent: resource recommendations work best when WebSearch/WebFetch is available in the harness; offline mode falls back to portal-level recommendations.
- Out of scope: PRC domestic law, active-matter opinions, and tasks requiring paid databases the user does not hold (see SKILL.md "Out of Scope" section).
- Tier 4 (AI-assisted research) carries privilege and confidentiality obligations the user — not the AI tool — is responsible for managing.
