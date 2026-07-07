# PrimeSec Org Context

This file gives AI coding agents a cross-repository map for the local PrimeSec workspace. It complements repo-specific files such as `CLAUDE.md`, `AGENTS.md`, `DESIGN.md`, and each repo's `README.md`.

Use this file when work may cross repository boundaries, depend on generated API clients, affect end-to-end flows, or touch shared PrimeSec packages.

## Local Workspace Layout

The local workspace is a set of separate git repositories under the same parent directory:

```text
primesec/
  frontend/                  # React dashboard and shared frontend UI libraries
  front-service/             # Backend API used by the dashboard; source of generated clients
  eagle/                     # Python test/pipeline workspace plus Playwright e2e package
  packages/                  # Shared Python packages used across services and tests
  prime-cli/                 # PrimeSec CLI tooling
  audit-service/             # Audit domain service
  chatbot-service/           # Chatbot domain service
  code-management-service/   # Code management domain service
  rat-logic-service/         # RAT/risk-analysis logic service
  security-review-service/   # Security review domain service
```

These repositories are related, but they are not one git monorepo. Check git status, branches, and remotes per repository before making changes.

## GitHub Org Inventory

The PrimeSec GitHub org contains additional repositories beyond the local clones above. As of 2026-06-24, the authenticated GitHub MCP repo list includes 44 accessible internal repositories:

### Product Apps and Services

- `frontend`
- `front-service`
- `policy-service`
- `security-review-service`
- `company-knowledge-service`
- `gen-ai-service`
- `source-service`
- `fetcher-service`
- `code-management-service`
- `notification-service`
- `coin-service`
- `rat-logic-service`
- `chatbot-service`
- `user-service`
- `file-manager-service`
- `converter-service`
- `audit-service`
- `config-service`
- `security-violation-service`
- `alert-triage-service`
- `embedding-service`
- `mcp-service`
- `mcp-service-poc`

### Shared Packages and Tooling

- `packages`
- `common`
- `prime-cli`
- `openapi-generator`
- `prime-security-tools` (archived)
- `agent-skills`

### Infrastructure and Runtime Configuration

- `devops-infra`
- `argocd`
- `nginx-config`
- `api-gw-authorizers`
- `presignup-cognito`
- `presignin-cognito`

### E2E, Research, Demos, and Test Repositories

- `eagle`
- `research`
- `mcp-demo-fastapi`
- `prime-mcp`
- `ERP-DEMO-OWASP25`
- `Big-Project-4`
- `test-service`
- `mor-test-github-issues`
- `moto`

Not every org repository is cloned locally. If a task references a repo that is not present in the workspace, do not infer its internals from the name alone. Ask whether to clone it, use GitHub tooling to inspect it, or proceed with the available context.

## Repository Roles

### `frontend`

- Nx monorepo for the PrimeSec dashboard.
- Uses React, TypeScript, Vite, Tailwind CSS, shadcn/ui, TanStack Query, MSW, and Playwright.
- Main app lives in `apps/dashboard`.
- Shared frontend code lives in `libs/ui`, `libs/common`, and `string-mapper`.
- API-dependent frontend code should inspect `node_modules/prime-front-service-client/openapi.json` or the generated SDK before assuming request or response shapes.

### `front-service`

- Backend API surface consumed by the dashboard.
- Produces generated clients used by the frontend and other internal code.
- Its README documents the client update flow:
  - `uv sync --upgrade-package prime-rat-logic-service-client`
  - `uv sync`
  - `prime service client-ts`
  - `prime service client`

### `eagle`

- Cross-service test and pipeline workspace.
- Python project with dependencies on multiple generated PrimeSec service clients.
- Contains an `e2e/` package using Playwright for browser-based end-to-end tests.
- Check here when changing important user flows, authentication behavior, onboarding flows, or multi-service workflows.

### `packages`

- Shared Python packages such as `prime-auth`, `prime-db-utils`, `prime-logger`, `prime-service-kit`, `prime-tests`, and utility libraries.
- Check here before duplicating shared service behavior, auth helpers, logging, database utilities, test helpers, or common infrastructure code.

### Domain Services

- `audit-service` owns audit-related backend behavior.
- `chatbot-service` owns chatbot-related backend behavior.
- `code-management-service` owns repository/code-management behavior.
- `company-knowledge-service` owns company knowledge retrieval and related knowledge workflows.
- `config-service` owns shared configuration behavior.
- `converter-service` owns conversion behavior for supported content or document formats.
- `fetcher-service` owns fetching behavior for external or internal sources.
- `file-manager-service` owns file management behavior and generated file-manager clients.
- `gen-ai-service` owns generative AI service behavior.
- `notification-service` owns notification behavior.
- `policy-service` owns policy domain behavior.
- `rat-logic-service` owns RAT and risk-analysis logic.
- `security-review-service` owns security review behavior.
- `source-service` owns source integration behavior.
- `user-service` owns user domain behavior.
- `security-violation-service` owns security violation domain behavior.
- `alert-triage-service` owns alert triage behavior.
- `embedding-service` owns embedding generation or retrieval behavior.
- `mcp-service` owns MCP-related service behavior.

When frontend or `front-service` behavior depends on one of these domains, inspect the owning service before guessing business logic.

### Infrastructure and Tooling Repositories

- `devops-infra` owns infrastructure-as-code.
- `argocd` owns Argo CD or GitOps runtime configuration.
- `nginx-config` owns Nginx runtime configuration.
- `api-gw-authorizers` owns API Gateway authorizer behavior.
- `presignup-cognito` and `presignin-cognito` own Cognito trigger behavior.
- `openapi-generator` owns generated-client templates and generation behavior.
- `prime-security-tools` owns internal security tooling.
- `prime-cli` owns PrimeSec CLI tooling.
- `agent-skills` owns reusable agent skill content.
- `common` may contain shared cross-repo material; inspect before duplicating shared conventions.

### Research, Demo, and Test Repositories

- `eagle` owns cross-service tests and Playwright E2E coverage.
- `research` contains research notebooks or experiments.
- `mcp-demo-fastapi`, `prime-mcp`, and `mcp-service-poc` are MCP demo/proof-of-concept related.
- `ERP-DEMO-OWASP25` is a vulnerable-code demo/testing repository.
- `test-service`, `mor-test-github-issues`, `Big-Project-4`, and `moto` are test/demo/special-purpose repositories unless local documentation says otherwise.

## Cross-Repo Contract Rules

1. Treat generated API clients and OpenAPI specs as source-of-truth for request and response shapes.
2. For frontend API hooks, inspect `frontend/node_modules/prime-front-service-client/openapi.json` or generated SDK types before editing UI flows, mocks, or request payloads.
3. If the frontend needs an API field that is missing from the generated client, inspect `front-service` before adding frontend-only assumptions.
4. If `front-service` delegates to another generated service client, inspect the owning service or its client package before changing behavior.
5. Regenerate clients through the repo-documented commands instead of editing generated SDK files manually.

## E2E and Pipeline Rules

1. Check `eagle/e2e` when changing high-value dashboard workflows, authentication, MFA, onboarding, user settings, repository connection flows, or security-review flows.
2. Prefer updating existing Playwright flows over creating duplicate coverage.
3. If a behavior relies on test users, seeded data, QR codes, MFA, or secrets manager values, inspect existing Eagle helpers before adding new setup logic.
4. Keep local frontend validation separate from Eagle validation: frontend unit/UI tests prove component behavior; Eagle proves integrated product behavior.

## Shared Package Rules

1. Search `packages` before creating reusable Python utilities in a service.
2. Prefer existing shared packages for auth, logging, database access, tests, service scaffolding, Cognito, RabbitMQ, Redis, and AWS SigV4 concerns.
3. Avoid moving service-specific business logic into shared packages unless more than one service genuinely needs it.
4. When changing a shared package, identify every repository that imports it and plan compatibility carefully.

## Agent Checklist Before Cross-Repo Changes

- Identify the repository that owns the behavior.
- Read the local repo instructions first: `CLAUDE.md`, `AGENTS.md`, `DESIGN.md`, and `README.md` where present.
- Check git status in each repository you may touch.
- Inspect generated API contracts before changing API-dependent code.
- Check Eagle coverage before changing integrated user journeys.
- Search `packages` before duplicating shared utilities.
- Keep changes scoped to the owning repository unless the task explicitly needs coordinated edits.
- Do not expose tokens, credentials, or private remote URLs in logs, docs, commits, or responses.

## Common Development Paths

### Frontend change backed by existing API

1. Inspect `frontend/node_modules/prime-front-service-client/openapi.json` or generated SDK types.
2. Update frontend API hook, UI, state, mocks, and tests.
3. Run frontend validation from `frontend`.
4. Check whether Eagle E2E coverage should be updated.

### Frontend change needing API support

1. Inspect desired behavior in `frontend`.
2. Inspect `front-service` endpoint ownership and generated-client flow.
3. Inspect downstream domain service if `front-service` delegates the behavior.
4. Update backend contract first, regenerate clients, then update frontend code.
5. Update tests at the right layers.

### Integrated product-flow change

1. Identify all repos involved in the flow.
2. Check frontend route/component behavior.
3. Check `front-service` API contract.
4. Check domain service ownership.
5. Check Eagle E2E flows and helpers.
6. Validate each touched repo independently.

## Naming Guidance

Call this an org context or repo map, not a monorepo guide. The workspace contains many related repositories, but each repository has its own git history, commands, CI, and ownership boundaries.
