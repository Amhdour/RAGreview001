> This is the client-facing mirror of the PHASE 2 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_2/.

# Phase 2 Constraints

## Technical constraints
- Source-only review preparation only.
- No application source code modifications.
- No exploit validation.
- No runtime proof claims.
- No production readiness claims.

## Access constraints
- Limited to local repository files and review artifacts.
- Production access is NOT AVAILABLE.
- Staging access is NOT AVAILABLE unless later documented.
- External systems are NOT AVAILABLE unless later documented and authorized.

## Environment constraints
- Work only inside `rag-security-readiness-review/`.
- Preserve `00_original_source/` unchanged.
- Treat unavailable tools and environments as NOT AVAILABLE, not as proof of absence.

## Testing constraints
- No security testing in Phase 2.
- No destructive testing.
- No DoS testing.
- No unauthorized scanning.
- No credential attacks.
- No malware execution.

## Data constraints
- Do not use real customer data.
- Do not use real credentials.
- Redact sensitive values from any future evidence artifacts.
- Treat all secrets as sensitive until proven otherwise.

## Time/scope constraints
- This phase is limited to boundary establishment and review planning.
- Deeper technical validation is deferred to later phases.

## Evidence constraints
- Only record evidence that can be directly supported by local files or recorded commands.
- Distinguish confirmed facts from assumptions.
- Preserve raw outputs when used as evidence.

## Legal/authorization constraints
- Do not test systems or third-party services without explicit authorization.
- Do not infer legal compliance or certification from source review alone.
- Do not claim any warranty or guarantee.

## Client-communication constraints
- Use client-safe wording.
- Avoid overstating confidence.
- Mark unknown values as UNCONFIRMED.
- Mark not applicable as NOT APPLICABLE.
- Mark unavailable as NOT AVAILABLE.
