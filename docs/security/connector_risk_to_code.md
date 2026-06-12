> This is the client-facing mirror of the PHASE 8 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_8/.

# Connector Risk to Code

## Category purpose
Map connector frameworks, credential handling, sync flows, and external-source permission paths to potential source-system controls.

## Related PHASE 7 risks
- CONN-01
- CONN-02
- CONN-03
- CONN-04
- CONN-05
- ACL-02
- ACL-03

## Related PHASE 6 threats
- TH-02
- TH-05
- TH-06
- TH-07
- TH-14

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/auth_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/connectors/factory.py
- backend/onyx/connectors/credentials_provider.py
- backend/onyx/connectors/connector_runner.py
- backend/onyx/db/credentials.py
- backend/onyx/auth/oauth_token_manager.py
- backend/onyx/auth/oauth_refresher.py
- backend/ee/onyx/server/oauth/api.py
- backend/ee/onyx/server/oauth/api_router.py
- backend/ee/onyx/server/oauth/google_drive.py
- backend/ee/onyx/server/oauth/confluence_cloud.py
- backend/ee/onyx/server/oauth/slack.py
- backend/ee/onyx/external_permissions/google_drive/permission_retrieval.py
- backend/ee/onyx/external_permissions/sharepoint/permission_utils.py

## Existing control candidates
- CONN-MAP-01: connector instantiation and credential-provider code paths appear present.
- CONN-MAP-02: OAuth and external-permission handling paths appear present.

## Missing control candidates
- No dedicated credential-rotation or secret-encryption evidence path was identified.

## Unverified mappings
- Connector credential handling remains source-only and untested.

## Later validation methods
- Connector scope review.
- OAuth flow validation.
- Credential storage and rotation review.

## Non-claims
- No claim that connector credentials are stored safely.
- No claim that source-system permissions are complete or correct.

## Client-ready summary
Connector-related code paths span factory, OAuth, and permission-sync logic, but the current pass does not validate their security properties.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CONN-MAP-01 | CONN-01 / CONN-04 | TH-05 | rag_pipeline_map.md; auth_flow_map.md; backend_architecture.md | backend/onyx/connectors/factory.py; backend/onyx/connectors/credentials_provider.py; backend/onyx/connectors/connector_runner.py | EXISTING-CANDIDATE | These paths appear to instantiate connectors and supply credentials to external-source sync logic. | No secret-storage or source-trust runtime validation was performed. | Connector credential-handling and sync-policy validation. | Source-level connector boundary candidate. |
| CONN-MAP-02 | CONN-02 / CONN-03 | TH-05 / TH-06 / TH-14 | rag_pipeline_map.md; auth_flow_map.md; backend_architecture.md | backend/ee/onyx/server/oauth/api.py; backend/ee/onyx/server/oauth/api_router.py; backend/ee/onyx/server/oauth/google_drive.py; backend/ee/onyx/server/oauth/confluence_cloud.py; backend/ee/onyx/server/oauth/slack.py; backend/ee/onyx/external_permissions/google_drive/permission_retrieval.py; backend/ee/onyx/external_permissions/sharepoint/permission_utils.py | EXISTING-CANDIDATE | These files show OAuth-based connector administration and external permission handling for common source systems. | No live connector scope review or permission-sync validation was collected. | OAuth connector-flow and permission-sync review. | Potential control path for source access and sync scope. |
| CONN-MAP-03 | CONN-05 | TH-06 / TH-07 | rag_pipeline_map.md; auth_flow_map.md; backend_architecture.md | backend/onyx/db/credentials.py; backend/onyx/auth/oauth_token_manager.py; backend/onyx/auth/oauth_refresher.py | MISSING-CANDIDATE | The review found credential-related files, but not a dedicated evidence path proving credential encryption, rotation, or lifecycle hardening. | No dedicated credential-rotation or secret-encryption evidence was found in this pass. | Credential storage and rotation review. | Gap in evidence, not a statement that storage is unsafe. |
