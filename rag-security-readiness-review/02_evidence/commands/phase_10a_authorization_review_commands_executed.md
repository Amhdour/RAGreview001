# PHASE 10A Authorization Review Commands Executed

## Repository and instruction discovery
- `pwd`
- `git rev-parse --show-toplevel`
- `git branch --show-current`
- `git rev-parse HEAD`
- `git status --short`
- `find .. -name AGENTS.md -print`
- `sed -n '1,260p' AGENTS.md`
- `sed -n '1,260p' web/AGENTS.md`

## Prior-phase evidence inventory
- `find rag-security-readiness-review/02_evidence/phase_8 -maxdepth 2 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_9 -maxdepth 3 -type f | sort`
- `test -f rag-security-readiness-review/03_reports/phase_9_control_to_test_mapping_report.md && echo EXISTS || echo NOT_AVAILABLE`

## Source inspection commands
- `rg --files backend web docs rag-security-readiness-review/02_evidence | rg -i "permission|role|admin|curator|group|tenant|workspace|grant|access|authz|document|connector|credential|permission_sync|acl|visibility|ownership|owner" | sort`
- `rg -n -i "permission|permissions|role|roles|admin|curator|global_curator|group|groups|tenant|workspace|grant|grants|access|authz|require|check|allowed|denied|document_set|document|connector|credential|permission_sync|acl|private|public|deleted|restricted|visibility|ownership|owner" backend web docs rag-security-readiness-review/02_evidence 2>/dev/null || true`
- `rg -n "class (Permission|UserRole|Role|GroupRole|ConnectorCredentialPairStatus|AccessType|ChatSessionSharedStatus|SyncType|PermissionSyncStatus|DocumentSet|UserGroup|Workspace|Tenant)" backend/onyx/db/enums.py backend/onyx/db/models.py backend/onyx/db/users.py backend/onyx/db/document.py backend/onyx/db/document_set.py backend/onyx/db/connector.py backend/ee/onyx/db/user_group.py backend/ee/onyx/db/external_perm.py backend/ee/onyx/db/connector_credential_pair.py`
- `rg -n "UserRole|Permission|effective_permissions|role|curator|admin|group|tenant|workspace|grant|permission" backend/onyx/db/models.py backend/onyx/db/users.py backend/onyx/db/document.py backend/onyx/db/document_set.py backend/onyx/db/connector.py backend/ee/onyx/db/user_group.py backend/ee/onyx/db/external_perm.py backend/ee/onyx/db/connector_credential_pair.py`
- `rg -n "def (current_.*user|.*admin.*|.*curator.*|.*anonymous.*|.*role.*|.*permission.*|.*auth.*)" backend/onyx/auth/users.py backend/onyx/server/manage/users.py backend/onyx/server/features/oauth_config/api.py backend/onyx/server/features/default_assistant/api.py backend/onyx/server/features/search/api.py`
- `rg -n "requireAdminAuth|requireAuth|redirect\(|UserRole|admin|curator|global_curator|is_verified" web/src/app/admin web/src/app/ee/admin web/src/layouts/admin web/src/sections/sidebar web/src/sections/onboarding web/src/components`
- `find backend/tests web/tests tests -type f 2>/dev/null | sort | rg -i "permission|admin|curator|group|tenant|document|connector|access|role|authz|acl|permission_sync"`
- `rg -n -i "permission|admin|curator|group|tenant|document|connector|access|role|authz|acl|permission_sync" backend/tests web/tests tests 2>/dev/null || true`

## File inspection commands
- `nl -ba backend/onyx/db/enums.py | sed -n '490,554p'`
- `nl -ba backend/onyx/auth/schemas.py | sed -n '1,120p'`
- `nl -ba backend/onyx/db/models.py | sed -n '312,375p'`
- `nl -ba backend/onyx/db/models.py | sed -n '4308,4352p'`
- `nl -ba backend/onyx/db/models.py | sed -n '963,1036p'`
- `nl -ba backend/onyx/db/models.py | sed -n '3408,3465p'`
- `nl -ba backend/onyx/db/document_access.py | sed -n '1,220p'`
- `nl -ba backend/onyx/access/access.py | sed -n '1,240p'`
- `nl -ba backend/ee/onyx/access/access.py | sed -n '1,260p'`
- `nl -ba backend/onyx/auth/users.py | sed -n '150,260p'`
- `nl -ba backend/onyx/auth/users.py | sed -n '1940,2005p'`
- `nl -ba backend/onyx/server/manage/users.py | sed -n '120,220p'`
- `nl -ba backend/onyx/server/manage/users.py | sed -n '760,820p'`
- `nl -ba backend/onyx/server/manage/users.py | sed -n '840,920p'`
- `nl -ba backend/onyx/server/features/oauth_config/api.py | sed -n '55,150p'`
- `nl -ba backend/onyx/server/features/search/api.py | sed -n '1,180p'`
- `nl -ba backend/ee/onyx/db/user_group.py | sed -n '1,120p'`
- `nl -ba backend/ee/onyx/db/user_group.py | sed -n '260,430p'`
- `nl -ba backend/ee/onyx/db/user_group.py | sed -n '540,760p'`
- `nl -ba backend/ee/onyx/db/user_group.py | sed -n '760,835p'`
- `nl -ba backend/ee/onyx/db/user_group.py | sed -n '930,1015p'`
- `nl -ba backend/onyx/db/permissions.py | sed -n '1,180p'`
- `nl -ba backend/ee/onyx/db/external_perm.py | sed -n '1,220p'`
- `nl -ba backend/ee/onyx/db/external_perm.py | sed -n '219,360p'`
- `nl -ba backend/ee/onyx/db/document.py | sed -n '1,140p'`
- `nl -ba backend/ee/onyx/db/connector_credential_pair.py | sed -n '1,120p'`
- `nl -ba backend/ee/onyx/access/hierarchy_access.py | sed -n '1,200p'`
- `nl -ba web/src/lib/auth/requireAuth.ts | sed -n '1,240p'`
- `nl -ba web/src/layouts/admin/Layout.tsx | sed -n '1,220p'`
- `nl -ba web/src/app/ee/admin/layout.tsx | sed -n '1,220p'`
- `nl -ba web/src/components/IsPublicGroupSelector.tsx | sed -n '1,140p'`
- `nl -ba web/src/lib/types.ts | sed -n '56,110p'`

## Raw output capture commands used for the evidence files
- `find rag-security-readiness-review/02_evidence/phase_8 -maxdepth 2 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_9 -maxdepth 3 -type f | sort`
- `find backend/tests web/tests tests -type f 2>/dev/null | sort | rg -i "permission|admin|curator|group|tenant|document|connector|access|role|authz|acl|permission_sync"`
- `rg -n -i "permission|admin|curator|group|tenant|document|connector|access|role|authz|acl|permission_sync" backend/tests web/tests tests 2>/dev/null || true`
