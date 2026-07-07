# PrimeSec

Internal engineering hub for the PrimeSec org. Most repositories here are private, so this page exists to index them in one place — grouped the way engineers actually reason about the system (product code, shared packages, infra, and demo/test repos).

PrimeSec's product surface spans security review, risk analysis (RAT), policy management, and alert triage, built as a set of independently-deployed services behind a shared frontend.

## Repositories

### Product apps & services

| Repo | Description |
|---|---|
| [frontend](https://github.com/primesec-ai/frontend) | React dashboard + shared frontend UI libraries (Nx monorepo). |
| [front-service](https://github.com/primesec-ai/front-service) | Backend API for the dashboard; source of generated API clients. |
| [security-review-service](https://github.com/primesec-ai/security-review-service) | Security review domain behavior. |
| [rat-logic-service](https://github.com/primesec-ai/rat-logic-service) | RAT / risk-analysis logic. |
| [policy-service](https://github.com/primesec-ai/policy-service) | Policy domain behavior. |
| [security-violation-service](https://github.com/primesec-ai/security-violation-service) | Security violation domain behavior. |
| [alert-triage-service](https://github.com/primesec-ai/alert-triage-service) | Alert triage behavior. |
| [company-knowledge-service](https://github.com/primesec-ai/company-knowledge-service) | Company knowledge retrieval and related knowledge workflows. |
| [gen-ai-service](https://github.com/primesec-ai/gen-ai-service) | Generative AI service behavior. |
| [embedding-service](https://github.com/primesec-ai/embedding-service) | Embedding generation / retrieval behavior. |
| [chatbot-service](https://github.com/primesec-ai/chatbot-service) | Chatbot behavior. |
| [source-service](https://github.com/primesec-ai/source-service) | Source integration behavior. |
| [fetcher-service](https://github.com/primesec-ai/fetcher-service) | Fetching behavior for external/internal sources. |
| [code-management-service](https://github.com/primesec-ai/code-management-service) | Repository / code-management behavior. |
| [converter-service](https://github.com/primesec-ai/converter-service) | Conversion behavior for supported content/document formats. |
| [file-manager-service](https://github.com/primesec-ai/file-manager-service) | File management behavior and generated file-manager clients. |
| [notification-service](https://github.com/primesec-ai/notification-service) | Notification behavior. |
| [user-service](https://github.com/primesec-ai/user-service) | User domain behavior. |
| [config-service](https://github.com/primesec-ai/config-service) | Shared configuration behavior. |
| [audit-service](https://github.com/primesec-ai/audit-service) | Audit-related backend behavior. |
| [coin-service](https://github.com/primesec-ai/coin-service) | Domain service — see repo for details. |
| [mcp-service](https://github.com/primesec-ai/mcp-service) | MCP-related service behavior. |

### Shared packages & tooling

| Repo | Description |
|---|---|
| [packages](https://github.com/primesec-ai/packages) | Shared Python packages (auth, db-utils, logger, service-kit, test helpers). |
| [common](https://github.com/primesec-ai/common) | Shared cross-repo material and conventions. |
| [prime-cli](https://github.com/primesec-ai/prime-cli) | PrimeSec CLI tooling. |
| [openapi-generator](https://github.com/primesec-ai/openapi-generator) | Generated-client templates and generation behavior. |
| [agent-skills](https://github.com/primesec-ai/agent-skills) | Reusable AI-agent skill content. |
| [prime-security-tools](https://github.com/primesec-ai/prime-security-tools) | Internal security tooling. *(archived)* |

### Infrastructure & runtime configuration

| Repo | Description |
|---|---|
| [devops-infra](https://github.com/primesec-ai/devops-infra) | Infrastructure-as-code. |
| [argocd](https://github.com/primesec-ai/argocd) | Argo CD / GitOps runtime configuration. |
| [nginx-config](https://github.com/primesec-ai/nginx-config) | Nginx runtime configuration. |
| [api-gw-authorizers](https://github.com/primesec-ai/api-gw-authorizers) | API Gateway authorizer behavior. |
| [presignup-cognito](https://github.com/primesec-ai/presignup-cognito) | Cognito pre-signup trigger behavior. |
| [presignin-cognito](https://github.com/primesec-ai/presignin-cognito) | Cognito pre-signin trigger behavior. |

### E2E, research, demos & test

| Repo | Description |
|---|---|
| [eagle](https://github.com/primesec-ai/eagle) | Cross-service test/pipeline workspace; Playwright E2E coverage. |
| [research](https://github.com/primesec-ai/research) | Research notebooks and experiments. |
| [mcp-demo-fastapi](https://github.com/primesec-ai/mcp-demo-fastapi) | MCP demo (FastAPI). |
| [prime-mcp](https://github.com/primesec-ai/prime-mcp) | MCP demo. |
| [mcp-service-poc](https://github.com/primesec-ai/mcp-service-poc) | MCP proof-of-concept. |
| [ERP-DEMO-OWASP25](https://github.com/primesec-ai/ERP-DEMO-OWASP25) | Vulnerable-code demo/testing repo. |
| [test-service](https://github.com/primesec-ai/test-service) | Test/demo repo. |
| [mor-test-github-issues](https://github.com/primesec-ai/mor-test-github-issues) | Test repo for GitHub Issues workflows. |
| [Big-Project-4](https://github.com/primesec-ai/Big-Project-4) | Test/demo repo. |
| [moto](https://github.com/primesec-ai/moto) | Test/demo repo. |

---

Not every repo above reflects production-owned behavior — POC, demo, and test repos exist for prototyping and are called out as such. Check each repo's own `README.md` / `CLAUDE.md` / `AGENTS.md` for specifics before making changes.
