# PHASE 5 Commands Executed

## Purpose
Record repository commands used to produce PHASE 5 architecture maps.

## Commands
- `pwd && rg --files -g 'AGENTS.md' -g 'CONTRIBUTING.md' -g 'package.json' -g 'pyproject.toml' | sed -n '1,80p'`
- `cat AGENTS.md && rg -n "Engineering Best Practices|Best Practices|Testing|Type" CONTRIBUTING.md | sed -n '1,80p'`
- `find rag-security-readiness-review -maxdepth 3 -type f | sort | sed -n '1,220p'`
- `find backend/onyx -maxdepth 2 -type f | sed -n '1,220p'`
- `find backend/onyx/server -maxdepth 3 -type f -name '*.py' | sort | sed -n '1,240p'`
- `find web/src/app web/src/refresh-pages web/src/sections web/src/refresh-components web/src/layouts web/src/lib -maxdepth 2 -type f 2>/dev/null | sort | sed -n '1,240p'`
- `find backend/onyx/configs -maxdepth 2 -type f | sort | sed -n '1,200p'`
- `find backend/onyx/db backend/ee/onyx/db backend/alembic -maxdepth 2 -type f 2>/dev/null | sort | sed -n '1,260p'`
- `find backend -maxdepth 3 -type f \( -name 'main.py' -o -name 'application.py' -o -name 'api.py' \) | sort | sed -n '1,120p'`
- `find web/src/app -maxdepth 3 -type f | sort | sed -n '1,220p'`
- `find deployment -maxdepth 3 -type f | sort | sed -n '1,220p'`
- `python` AST/path inventory commands for route/module and model discovery.
- `python` path validation command that checked backtick file-path references in PHASE 5 markdown files.

## Notes
- Commands were read-only until the PHASE 5 markdown deliverables and this command log were written.
- No application source code was changed.
