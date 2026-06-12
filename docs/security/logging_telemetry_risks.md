> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# Logging/Telemetry Risks

## Category purpose

Track how observability systems can leak prompts, documents, or tokens.

## Scope

Logs, traces, metrics, spans, and observability access patterns.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/logging_telemetry_map.md

## Related PHASE 6 threats

- TH-01
- TH-10
- TH-13
- TH-15

## Protected assets affected

Logs; telemetry spans; metrics; prompts; documents; tokens

## Actors involved

Background worker; deployment operator; malicious insider

## Trust boundaries involved

Logging/telemetry; deployment/runtime; observability

## Data flows involved

Request or prompt data into logs; telemetry span emission; observability access by operators

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LOG-01 | Prompt leakage into logs can expose user or system content. | EVIDENCE-LINKED | TH-10 | logging_telemetry_map.md | Logs; telemetry spans; metrics; prompts; documents; tokens | Background worker; deployment operator; malicious insider | Logging/telemetry; deployment/runtime; observability | Private prompts may be visible outside the user-facing flow. | No live log review. | Later log-redaction review. | High candidate |
| LOG-02 | Retrieved document leakage into logs can expose source content and metadata. | EVIDENCE-LINKED | TH-10, TH-01 | logging_telemetry_map.md | Logs; telemetry spans; metrics; prompts; documents; tokens | Background worker; deployment operator; malicious insider | Logging/telemetry; deployment/runtime; observability | Private documents may be copied into observability systems. | No live telemetry sink inspection. | Later telemetry-content review. | High candidate |
| LOG-03 | Token or API-key leakage into logs can turn observability into a credential sink. | EVIDENCE-LINKED | TH-10, TH-13, TH-15 | logging_telemetry_map.md | Logs; telemetry spans; metrics; prompts; documents; tokens | Background worker; deployment operator; malicious insider | Logging/telemetry; deployment/runtime; observability | Credentials may become reusable by an attacker with log access. | No live redaction validation. | Later secret-redaction review. | Critical candidate |
| LOG-04 | Sensitive telemetry spans can carry more context than needed for debugging. | EVIDENCE-LINKED | TH-10 | logging_telemetry_map.md | Logs; telemetry spans; metrics; prompts; documents; tokens | Background worker; deployment operator; malicious insider | Logging/telemetry; deployment/runtime; observability | Operational observability could disclose message or document content. | No live telemetry review. | Later observability-content review. | Medium candidate |
| LOG-05 | Missing redaction evidence leaves observability protections unproven. | UNVERIFIED | TH-10 | logging_telemetry_map.md | Logs; telemetry spans; metrics; prompts; documents; tokens | Background worker; deployment operator; malicious insider | Logging/telemetry; deployment/runtime; observability | The review cannot confirm that sensitive fields are filtered. | No redaction proof. | Later redaction review. | Informational |

## Missing evidence

No live log or telemetry sink review; no redaction verification; no live observability access review.

## Later validation methods

Log/telemetry redaction review; access-control review for observability sinks; live telemetry content review.

## Non-claims

No claim that observability is redacted; no claim that telemetry is safe; no claim of live review.

## Client-ready summary

The category shows how prompt and document data can leak from systems intended for visibility, not disclosure.
