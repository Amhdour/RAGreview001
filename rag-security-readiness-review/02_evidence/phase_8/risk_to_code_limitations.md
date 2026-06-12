# PHASE 8 Risk to Code Mapping Limitations

## Source-only limitation
This phase is based only on repository source and review artifacts.

## Current-checkout limitation
The mapping reflects the current GitHub repository checkout and not a separate review copy.

## Unavailable original source limitation
The original source snapshot path remained unavailable during this phase.

## Unavailable working-copy limitation
The separate `01_working_copy/` path remained unavailable during earlier phases and was not used here.

## File/path search limitation
File and path searches only identify candidates; they do not prove runtime behavior or effective enforcement.

## Static mapping limitation
This is a static risk-to-code map, not a control assessment or remediation verification.

## No runtime validation
No runtime validation of auth, ACL, ingestion, prompt, agent, connector, logging, or deployment behavior was performed.

## No exploit validation
No exploit or adversarial validation was performed.

## No CI/test validation
No application tests or CI jobs were run for this phase.

## No production validation
No production deployment or live service validation was performed.

## No live database/vector index/connector/log/telemetry access
No live database, vector index, connector system, log sink, or telemetry sink was inspected.

## No customer data
No customer data was used or inspected.

## No real secrets
No real secrets were used or collected.

## Existing candidate does not mean effective control
A path that looks like a control candidate may still be incomplete, bypassable, or unvalidated.

## Missing candidate does not prove absence of control
A missing candidate reflects absent evidence in this pass, not proof that a control does not exist.

## Risk-to-code mapping is not remediation verification
The mapping does not confirm that the repository is secure or that risks are mitigated.

## Later validation is required before final control claims
Later phases must validate the control candidates before any final control claim is made.
