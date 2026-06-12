# PHASE 3 Fixtures

## Purpose
Safe local fixtures for future retrieved-document handling tests.

## Safety rules
- These files are synthetic.
- These files contain no customer data.
- These files contain no secrets.
- These files contain no operational instructions for external systems.
- Marker strings are placeholders for future classifier and regression tests.

## Fixture set

| File | Purpose | Expected future classification |
| --- | --- | --- |
| `normal_company_policy.md` | Benign reference document | allow |
| `instruction_conflict_marker.md` | Synthetic document containing a conflict marker | review |
| `system_text_marker.md` | Synthetic document containing a system-text marker | review |
| `action_text_marker.md` | Synthetic document containing an action-text marker | review |
| `citation_marker.md` | Synthetic document containing a citation-integrity marker | review |
| `mixed_reference_marker.md` | Mostly benign document with one review marker | review |

## Non-claims
- These fixtures do not prove detection.
- These fixtures do not prove prevention.
- These fixtures do not execute anything.
- These fixtures are not production validation evidence.
