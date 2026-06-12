# Blocked and Skipped Checks

| Check name | Intended command or method | Status | Reason | Impact | Follow-up action |
| --- | --- | --- | --- | --- | --- |
| Original source availability check | `test -d rag-security-readiness-review/00_original_source && echo EXISTS || echo NOT_AVAILABLE` | NOT AVAILABLE | Directory was absent during PHASE 4. | Original source manifest from preserved snapshot could not be generated. | Restore or provide `00_original_source/` if snapshot-level comparison is required. |
| Original source manifest generation | `find rag-security-readiness-review/00_original_source -type f \| sort` | BLOCKED | Directory was absent, so a direct `find` would not produce a valid file list. | PHASE 4 cannot inventory original source snapshot contents. | Restore snapshot or generate a hash/file manifest from a trusted source. |
| Working copy availability check | `test -d rag-security-readiness-review/01_working_copy && echo EXISTS || echo NOT_AVAILABLE` | NOT AVAILABLE | Directory was absent during PHASE 4. | PHASE 4 cannot compare against a review working copy. | Preserve PHASE 3 limitation and use current checkout as documented target. |
| Working copy based review | Inspect `rag-security-readiness-review/01_working_copy/` | SKIPPED | Path was NOT AVAILABLE; PHASE 3 documented the same limitation. | Cannot claim PHASE 3 inventory ran inside `01_working_copy/`. | Recreate the working copy if later phases need it. |
| Cryptographic integrity/hashing | Generate hashes for original and review artifacts | SKIPPED | Not requested for PHASE 4 and original source snapshot was absent. | File separation is not cryptographic proof. | Add a hashing phase if integrity evidence is needed. |
| Source-code diff against original snapshot | Diff current checkout against `00_original_source/` | SKIPPED | `00_original_source/` was NOT AVAILABLE. | No snapshot diff can be claimed. | Restore original snapshot or use a known baseline commit. |
| Security tests | Run security scanners or exploit/security tests | SKIPPED | Explicitly prohibited by PHASE 4 instructions. | No security validation performed. | Run only in a later approved testing phase. |
| Exploit tests | Run exploit or adversarial tests | SKIPPED | Explicitly prohibited by PHASE 4 instructions. | No exploit validation performed. | Run only with explicit authorization and scope. |
| Runtime tests / CI | Run application tests, runtime checks, or CI | SKIPPED | Out of PHASE 4 scope; no tests requested. | No test or CI pass claim can be made. | Execute in an authorized testing phase. |
| Command failures | Record command failures | NOT APPLICABLE | No command failures occurred during PHASE 4 file generation. | No failure-specific evidence needed. | Continue recording future failures exactly if they occur. |

## Additional unavailable paths
- `rag-security-readiness-review/00_original_source/`: NOT AVAILABLE.
- `rag-security-readiness-review/01_working_copy/`: NOT AVAILABLE.

## Limitation carried forward from PHASE 3
PHASE 3 documented that `rag-security-readiness-review/01_working_copy/` was not present and that inventory was generated from the current repository checkout. PHASE 4 preserves that limitation.
