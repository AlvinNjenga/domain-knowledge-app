# PROJECT.md

# AI Knowledge & Workflow Platform

## 1. Project overview

A multi-tenant SaaS platform that allows businesses to:

- Centralise and manage internal documents and knowledge.
- Create AI assistants that answer questions using company knowledge.
- Use controlled AI tools to perform application operations.
- Build AI-powered workflows combining retrieval, generation, conditions and tools.
- Introduce human approval into automated processes.

**Primary objective:** Build a production-quality AI platform demonstrating practical AI engineering, RAG, agent orchestration, workflow automation and full-stack software development.

The priority is to build a reliable, useful product incrementally rather than implement every planned feature immediately.

## 2. Technology stack

| Area | Technology |
|---|---|
| Frontend | React, TypeScript, Vite |
| UI | Tailwind CSS, shadcn/ui |
| Server state | TanStack Query |
| Workflow editor | React Flow |
| Main backend | ASP.NET Core / C# |
| AI service | Python / FastAPI |
| AI orchestration | LangGraph where appropriate |
| LLM and embeddings | OpenAI API |
| Database | PostgreSQL |
| Vector search | pgvector |
| File storage | AWS S3 |
| Background jobs | AWS SQS |
| Caching | Redis |
| Authentication | Cognito / OIDC |
| Hosting | AWS ECS Fargate |
| Infrastructure | Terraform |
| CI/CD | GitHub Actions |

Do not introduce additional technologies without a clear justification.

## 3. Architecture principles

1. **Modular monolith:** Keep the main .NET application modular. Do not introduce unnecessary microservices.
2. **Separate AI service:** AI orchestration and document processing belong in the Python service.
3. **Clear boundaries:** The frontend, backend and AI service must communicate through defined interfaces.
4. **Asynchronous processing:** Use durable queues for document processing and long-running workflows.
5. **Persistent state:** Store important application and workflow state in PostgreSQL.
6. **Security first:** Enforce authentication, authorisation and tenant isolation in application code.
7. **Testability:** Design components so their behaviour can be tested independently.
8. **Incremental development:** Implement the smallest complete, testable feature before expanding it.

Refer to `docs/ARCHITECTURE.md` and relevant ADRs for detailed architectural decisions.

## 4. Development priorities

Development follows these milestones:

### M1 — Functional MVP

- Authentication and organisation management.
- Knowledge base and document management.
- Asynchronous document ingestion.
- Text extraction, chunking and embedding generation.
- Semantic search using pgvector.
- AI assistants using RAG.
- Streaming chat responses with citations.

### M2 — Advanced platform

- Multiple configurable assistants.
- Hybrid retrieval.
- Controlled AI tool calling.
- Visual workflow editor.
- Persistent workflow execution.
- Human approvals and notifications.
- Usage and cost tracking.

### M3 — Production release

- Security and tenant isolation verification.
- Comprehensive automated testing.
- AI evaluation framework.
- Monitoring and observability.
- Backup and recovery.
- AWS production deployment.
- Operational documentation.

**Current milestone:** M1 — Functional MVP.

## 5. Engineering conventions

### General

- Prefer straightforward, maintainable solutions.
- Avoid unnecessary abstractions and premature optimisation.
- Keep business logic separate from infrastructure concerns.
- Use dependency injection where appropriate.
- Handle errors explicitly.
- Validate external inputs.
- Avoid duplicating existing functionality.
- Keep changes focused on the assigned task.

### Backend

- Follow established ASP.NET Core conventions.
- Use asynchronous operations for I/O.
- Use explicit request/response DTOs.
- Keep controllers/endpoints thin.
- Put business logic in appropriate application services.
- Use database migrations for schema changes.
- Enforce organisation and resource permissions at the application layer.

### Frontend

- Use TypeScript strictly.
- Build reusable components where there is genuine reuse.
- Keep API communication separate from presentation components.
- Use TanStack Query for server state.
- Provide loading, error and empty states.
- Ensure responsive and accessible interfaces.

### Python / AI service

- Use type hints.
- Separate orchestration, retrieval and document-processing responsibilities.
- Validate inputs and outputs.
- Keep model interactions behind reusable service interfaces where practical.
- Avoid coupling business logic directly to a specific LLM provider.
- Make AI operations observable and testable.

## 6. AI engineering requirements

These requirements apply throughout development:

- LLM output must never be treated as inherently trustworthy.
- Retrieved documents are untrusted input.
- AI tools must use validated schemas.
- Application permissions must be checked independently of model instructions.
- Tool execution must have appropriate limits and timeouts.
- RAG responses should retain source references.
- Handle insufficient retrieval context explicitly.
- Track model usage and estimated costs.
- Evaluate retrieval and answer quality using repeatable datasets.

## 7. Security requirements

- Enforce tenant isolation across all organisation-owned resources.
- Never rely on frontend checks for authorisation.
- Never expose API keys, secrets or credentials.
- Validate uploaded files and enforce size/type restrictions.
- Apply access controls before retrieving document content.
- Log security-sensitive operations.
- Define deletion behaviour for original documents and derived data.
- Consider prompt injection and malicious document content in AI workflows.

## 8. Testing requirements

Add appropriate tests alongside implementation.

| Component | Expected testing |
|---|---|
| .NET backend | Unit and integration tests |
| Python service | Unit and integration tests |
| Frontend | Component and integration tests |
| API | Contract and integration tests |
| RAG | Retrieval and answer evaluation |
| Workflows | Execution, failure and recovery tests |
| Platform | End-to-end and security tests |

Do not consider a feature complete simply because it works manually.

## 9. Documentation

Maintain the following project documentation:

| File | Responsibility |
|---|---|
| `PROJECT.md` | Project briefing and current development status |
| `docs/PRODUCT_SPEC.md` | Product requirements and intended behaviour |
| `docs/ARCHITECTURE.md` | System architecture and boundaries |
| `docs/DATA_MODEL.md` | Database entities and relationships |
| `docs/API.md` | API contracts and conventions |
| `docs/SECURITY.md` | Security requirements and threat model |
| `BACKLOG.md` | Epics, tickets, dependencies and status |
| `docs/ADRs/` | Architecture Decision Records |

Update documentation when implementation changes materially affect it.

## 10. Codex working instructions

Before starting a task:

1. Read this file.
2. Read the relevant section of the product specification.
3. Inspect the existing implementation and related tests.
4. Identify dependencies and relevant architectural decisions.
5. Confirm the task's acceptance criteria.

While implementing:

1. Work within the scope of the assigned ticket.
2. Follow established patterns unless there is a good reason to change them.
3. Avoid unrelated refactoring.
4. Add or update tests.
5. Do not silently introduce new dependencies or architectural decisions.
6. Ask for clarification when requirements are ambiguous or conflicting.

After implementing:

1. Run relevant tests and report their results.
2. Report files changed and important implementation decisions.
3. Identify outstanding issues or limitations.
4. Update relevant documentation.
5. Update the project status below when the task changes delivery progress.

Do not claim tests passed unless they were actually executed successfully.

---

# 11. Current project status

**Status:** Product discovery in progress

**Current milestone:** M1 — Functional MVP

**Current epic:** EPIC 00 — Product discovery

**Active ticket:** 00-01 — Finalise product requirements

**Completed:**
- Initial product specification.
- Initial architecture and technology selection.
- Initial engineering backlog.

**In progress:**
- Requirements consolidation and high-level journeys; decisions PD-01 through PD-06 remain open in `docs/PRODUCT_SPEC.md`.

**Next priorities:**
1. Resolve product decisions and complete EPIC 00.
2. Establish repository structure and architecture foundations in backlog dependency order.
3. Set up local development environment.
4. Begin authentication and organisation management.

**Known issues / decisions pending:**
- Resolve PD-01 through PD-06 before completing 00-01.
- Detailed architecture, data model, API, security and ADR documents do not yet exist; create them with their relevant tickets.
- Finalise authentication provider.
- Finalise detailed repository structure.
- Confirm local development and testing commands.
- Establish initial architecture decision records.

Update this section as the project progresses. Keep it concise and factual.