# AGENTS.md

# Project instructions — AI Knowledge & Workflow Platform

## 1. Purpose

You are working on a multi-tenant AI knowledge and workflow platform.

Your responsibility is to help implement the product incrementally, following the established requirements, architecture and engineering standards.

These instructions apply to the entire repository unless a more specific nested `AGENTS.md` provides additional guidance.

## 2. Project documentation

## Documentation management

The documentation structure may be incomplete during early development.
Do not assume that every referenced document already exists.

Use the following conventions:

- `PROJECT.md`: High-level project overview, technology stack,
  architecture principles and current development status.
- `docs/PRODUCT_SPEC.md`: Product requirements, feature behaviour
  and functional scope.
- `BACKLOG.md`: Engineering epics, tickets, dependencies,
  acceptance criteria and task status.
- `docs/ARCHITECTURE.md`: System architecture, component
  responsibilities, integrations and data flows.
- `docs/DATA_MODEL.md`: Domain entities, database schema,
  relationships, constraints and data ownership.
- `docs/SECURITY.md`: Authentication, authorisation, tenant
  isolation, data protection, threat considerations and security
  controls.
- `docs/ADRs/`: Architecture Decision Records documenting
  significant technical and architectural decisions.

### Rules

1. Before consulting a documentation file, check whether it exists.
2. If a relevant document does not exist, determine whether the
   current task requires it.
3. Create missing documentation when it is necessary to support
   the current task or when a significant decision or design
   needs to be recorded.
4. Do not create empty placeholder documents or unnecessary
   documentation simply because a file is referenced here.
5. When implementing a feature that changes the data model,
   update `docs/DATA_MODEL.md` where appropriate.
6. When implementing or changing security-sensitive behaviour,
   update `docs/SECURITY.md` where appropriate.
7. When making a significant architectural decision, create an
   ADR in `docs/ADRs/` and reference it from
   `docs/ARCHITECTURE.md` where appropriate.
8. Keep documentation consistent with the actual implementation.
   Clearly distinguish implemented behaviour from planned
   architecture or future requirements.
9. If documentation conflicts with the existing implementation,
   investigate the discrepancy rather than silently assuming
   either is correct.

## 3. Task and backlog workflow

All implementation work should be associated with a backlog ticket wherever possible.

When asked to implement a ticket:

1. Identify the ticket using its ID in `BACKLOG.md`.
2. Read its description, priority, dependencies and acceptance criteria.
3. Consult the relevant sections of `PRODUCT_SPEC.md`.
4. Review relevant architecture documentation and ADRs.
5. Inspect the existing implementation and tests.
6. Identify the files and components likely to require changes.
7. Implement only the agreed scope.

### Scope control

- Do not implement unrelated backlog tickets without permission.
- Do not expand the scope of a ticket unnecessarily.
- Identify missing dependencies before beginning implementation.
- If a ticket is too large, propose smaller implementation steps.
- Do not mark work complete simply because code has been written.

### Backlog maintenance

Until GitHub Issues becomes the project tracking source of truth:

- Keep `BACKLOG.md` updated with ticket status.
- Mark tickets `IN PROGRESS` when implementation begins.
- Mark tickets `REVIEW` when implementation and initial verification are complete.
- Mark tickets `DONE` only when acceptance criteria have been satisfied.
- Record newly discovered work as separate tickets rather than silently expanding the current task.
- Preserve existing ticket IDs.

Once GitHub Issues is adopted as the source of truth, use it for ticket status rather than maintaining competing status records in Markdown.

## 4. Architecture and technology

Follow the technology choices and architectural principles defined in `PROJECT.md` and `docs/ARCHITECTURE.md`.

Key boundaries:

- React / TypeScript frontend.
- ASP.NET Core / C# main application backend.
- Python / FastAPI AI service.
- PostgreSQL / pgvector database.
- AWS S3 document storage.
- AWS SQS background processing.
- AWS infrastructure managed through Terraform.

Architectural rules:

- Keep the main backend a modular monolith unless an accepted decision establishes otherwise.
- Keep AI-specific processing within the Python service.
- Maintain explicit interfaces between services.
- Keep important application and workflow state persistent.
- Avoid unnecessary dependencies and premature abstractions.
- Do not introduce new technologies or materially change architectural boundaries without explaining the rationale and seeking approval.
- Record significant architectural decisions in `docs/ADRs/`.

## 5. Security and AI requirements

Security and tenant isolation must be considered in every relevant implementation task.

- Enforce authorisation in backend/application code.
- Never rely exclusively on frontend checks.
- Never allow access across organisation boundaries without explicit authorisation.
- Treat uploaded documents and retrieved content as untrusted input.
- Never treat LLM output as inherently trustworthy.
- Validate AI tool inputs and outputs.
- Enforce permissions independently of model instructions.
- Apply appropriate execution limits and timeouts to AI operations.
- Never expose credentials, API keys or sensitive information.
- Consider data retention and deletion when implementing document-related features.

Consult `docs/SECURITY.md` for detailed requirements.

## 6. Engineering standards

### General

- Prefer clear, maintainable and straightforward implementations.
- Follow existing project conventions.
- Keep responsibilities separated.
- Handle errors explicitly.
- Validate external inputs.
- Avoid unrelated refactoring.
- Do not introduce unnecessary dependencies.
- Do not duplicate existing functionality.

### Backend

- Use asynchronous operations for I/O.
- Keep API endpoints and controllers thin.
- Use explicit request and response DTOs.
- Keep business logic in appropriate application services.
- Use dependency injection.
- Use database migrations for schema changes.
- Enforce resource ownership and permissions.

### Frontend

- Use TypeScript strictly.
- Keep API communication separate from presentation components.
- Use TanStack Query for server state.
- Provide appropriate loading, error and empty states.
- Build accessible and responsive interfaces.

### Python / AI service

- Use type hints.
- Separate document processing, retrieval and AI orchestration responsibilities.
- Validate inputs and outputs.
- Keep external model interactions appropriately encapsulated.
- Make AI operations testable and observable.

## 7. Testing and verification

Tests must be added or updated alongside implementation.

Use the relevant testing framework for each component:

- .NET: xUnit.
- Python: pytest.
- Frontend: Vitest.
- End-to-end: Playwright.

Before considering a task complete:

1. Run relevant automated tests.
2. Run applicable linting, formatting and build checks.
3. Investigate and resolve failures introduced by the changes.
4. Report any checks that could not be executed.
5. Never claim a test or build passed unless it was actually executed successfully.

Do not weaken existing tests or remove validation merely to make a build pass.

## 8. Implementation workflow

For substantial tasks:

**Before implementation**
- Understand the requirements.
- Inspect the relevant code.
- Identify dependencies and risks.
- Explain the proposed approach when the task is complex or ambiguous.

**During implementation**
- Work incrementally.
- Keep changes focused.
- Follow existing patterns.
- Add tests alongside functionality.
- Avoid changing unrelated files.

**After implementation**
- Summarise what was implemented.
- Identify important files changed.
- Report tests and verification results.
- Identify remaining limitations or follow-up work.
- Update relevant documentation and backlog status where appropriate.

## 9. Communication

Be explicit about assumptions and uncertainties.

When a requirement is unclear, do not invent product behaviour.

When an architectural change appears necessary:

1. Explain the limitation of the existing design.
2. Present the proposed change and alternatives.
3. Explain its trade-offs.
4. Seek approval before making significant changes.
5. Record the accepted decision in an ADR.

Prioritise correctness, maintainability and understanding over implementation speed.

