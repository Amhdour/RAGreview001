# PHASE 5 Frontend Architecture Map

## 1. Purpose
The frontend provides the browser-facing Next.js application, feature pages, shared UI sections, client/server helpers, instrumentation, and proxy route handlers.

## 2. Scope
- In scope: `web/src/app/`, `web/src/refresh-pages/`, `web/src/sections/`, `web/src/refresh-components/`, `web/src/layouts/`, `web/src/lib/`, `web/src/instrumentation.ts`, and `web/src/instrumentation-client.ts`.
- Out of scope: backend implementation internals, mobile/desktop apps, generated dependencies, and browser behavior not supported by source files.

## 3. Main entry points
- Root layout and global app shell: `web/src/app/layout.tsx`.
- App Router pages and route handlers: `web/src/app/`.
- Backend API proxy route: `web/src/app/api/[...path]/route.ts`.
- MCP proxy route: `web/src/app/mcp/[[...path]]/route.ts`.
- Auth screens: `web/src/app/auth/`.
- Main chat/app surface: `web/src/app/app/`.
- Build/craft surface: `web/src/app/craft/`.
- Admin surfaces: `web/src/app/admin/`.
- Shared feature sections: `web/src/sections/`.
- Shared frontend libraries: `web/src/lib/`.
- Instrumentation: `web/src/instrumentation.ts`, `web/src/instrumentation-client.ts`.

## 4. Architecture flow
1. `web/src/app/layout.tsx` defines the application-level layout entry point for the Next.js App Router tree.
2. User-facing pages are organized under `web/src/app/`, including auth pages under `web/src/app/auth/`, main application pages under `web/src/app/app/`, admin pages under `web/src/app/admin/`, and craft/build pages under `web/src/app/craft/`.
3. Frontend API calls can pass through `web/src/app/api/[...path]/route.ts` to reach backend API paths.
4. MCP-specific requests use `web/src/app/mcp/[[...path]]/route.ts` as a separate route handler.
5. Shared UI and feature code lives outside page directories in `web/src/sections/`, `web/src/refresh-pages/`, `web/src/refresh-components/`, `web/src/layouts/`, and `web/src/lib/`.
6. Frontend telemetry/instrumentation code is split between server-side instrumentation in `web/src/instrumentation.ts` and client-side instrumentation in `web/src/instrumentation-client.ts`.

## 5. Supporting evidence
- `web/src/app/layout.tsx` — root App Router layout.
- `web/src/app/api/[...path]/route.ts` — catch-all API route handler.
- `web/src/app/mcp/[[...path]]/route.ts` — MCP route handler.
- `web/src/app/auth/login/page.tsx`, `web/src/app/auth/logout/route.ts`, `web/src/app/auth/signup/page.tsx` — auth screens/routes.
- `web/src/app/app/page.tsx`, `web/src/app/app/layout.tsx` — main application surface.
- `web/src/app/admin/layout.tsx`, `web/src/app/admin/agents/page.tsx`, `web/src/app/admin/users/page.tsx` — admin surfaces.
- `web/src/app/craft/page.tsx`, `web/src/app/craft/services/apiServices.ts` — craft/build frontend surface and API service helpers.
- `web/src/lib/admin-routes.ts` — frontend admin route metadata.
- `web/src/lib/connector.ts`, `web/src/lib/credential.ts`, `web/src/lib/tools/mcpService.ts`, `web/src/lib/tools/openApiService.ts` — frontend service helpers for backend features.
- `web/src/instrumentation.ts`, `web/src/instrumentation-client.ts` — frontend instrumentation files.

## 6. Dependencies
- Internal dependencies: `web/src/app/` uses shared code from `web/src/lib/`, `web/src/sections/`, `web/src/refresh-pages/`, `web/src/refresh-components/`, and `web/src/layouts/`.
- Backend/API dependencies supported by files: `web/src/app/api/[...path]/route.ts` and frontend service helpers under `web/src/lib/` issue requests to backend API paths.
- MCP dependency supported by files: `web/src/app/mcp/[[...path]]/route.ts` and `web/src/lib/tools/mcpService.ts` represent MCP frontend/backend plumbing.

## 7. Gaps / unknowns
- The exact runtime environment for the deployed frontend is not established by frontend source files alone.
- Browser analytics destinations are not claimed unless directly present in instrumentation files.

## 8. Client-ready summary
The frontend is a Next.js application organized by routes and feature areas. It has separate pages for login, the main chat app, admin functions, and the craft/build experience. Shared frontend services and UI components live in library and section directories. API and MCP requests have dedicated route handlers.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| The frontend uses the Next.js App Router file tree. | `web/src/app/`, `web/src/app/layout.tsx` | Supported | The directory contains layouts, pages, and route handlers. |
| Auth screens are implemented in the frontend. | `web/src/app/auth/login/page.tsx`, `web/src/app/auth/signup/page.tsx`, `web/src/app/auth/logout/route.ts` | Supported | Auth pages and logout route are present. |
| Admin pages are implemented under the app route tree. | `web/src/app/admin/`, `web/src/lib/admin-routes.ts` | Supported | Admin route files and admin route metadata are present. |
| Frontend API proxying has a catch-all route handler. | `web/src/app/api/[...path]/route.ts` | Supported | The route handler exists. |
| MCP frontend routing has a dedicated route handler. | `web/src/app/mcp/[[...path]]/route.ts`, `web/src/lib/tools/mcpService.ts` | Supported | Both route and service files exist. |
| Production frontend hosting details are known from source files. | No repository evidence identified. | Unsupported | Hosting topology requires deployment evidence outside frontend source. |

## Missing or unsupported items
- Production frontend hosting topology and analytics destinations are unsupported unless corroborated by deployment or instrumentation files.
