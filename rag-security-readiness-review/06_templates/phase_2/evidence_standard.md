# Phase 2 Evidence Standard

## Evidence naming rules
- Use clear, phase-specific filenames.
- Prefix artifacts with `phase_2_` where helpful.
- Keep names descriptive and stable.

## Evidence folder rules
- Store Phase 2 evidence under `02_evidence/phase_2/`.
- Store reusable Phase 2 templates under `06_templates/phase_2/`.
- Keep command logs under `02_evidence/commands/`.

## Command logging rules
- Record every command executed for Phase 2.
- Include commands that fail, are skipped, or are blocked.
- Preserve the exact command text and the failure reason when relevant.

## Screenshot rules if used
- Use screenshots only if a visual artifact is necessary.
- Label screenshots with phase and context.
- Do not expose secrets or customer data in screenshots.

## Raw output preservation rules
- Preserve raw outputs when they are used as evidence.
- Do not paraphrase away critical details.
- Keep raw outputs separate from summaries when practical.

## Confirmed vs assumed distinction
- Confirmed facts must be directly supported by evidence.
- Assumptions must be explicitly labeled.
- UNCONFIRMED values must not be presented as facts.

## Failed/skipped/blocked command rules
- Record failed commands exactly.
- Record why the command failed or was skipped.
- Do not silently omit blocked work.

## Source reference rules
- Cite file paths and evidence locations in later reports.
- Separate review observations from conclusions.
- Do not infer unsupported claims from partial evidence.

## Client-safe redaction rules
- Redact secrets, tokens, credentials, and private identifiers.
- Do not expose sensitive customer data.
- Keep evidence suitable for client sharing where possible.

## No unsupported claims rule
- Do not claim security, readiness, or validation without direct evidence.
- Do not infer production behavior from source-only observations.

## Minimum evidence required before each next phase
- A documented scope and boundary set.
- A documented access limitation summary.
- A documented claim boundary summary.
- A documented testing rule set.
- A documented go/no-go decision framework.
