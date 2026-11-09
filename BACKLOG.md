# BACKLOG.md

# AI Knowledge & Workflow Platform

**Purpose:** Track engineering work, dependencies, priorities and delivery progress.

**Source of truth:** `docs/PRODUCT_SPEC.md` contains detailed product requirements and acceptance criteria. This file tracks the work required to implement them.

---

# 1. Backlog conventions

## Status

| Status | Meaning |
|---|---|
| `TODO` | Not started |
| `IN PROGRESS` | Currently being worked on |
| `BLOCKED` | Cannot proceed due to a dependency or issue |
| `REVIEW` | Implementation complete, awaiting review |
| `DONE` | Acceptance criteria satisfied |

## Priority

| Priority | Meaning |
|---|---|
| `P0` | Essential for MVP or production safety |
| `P1` | Important for the intended product |
| `P2` | Enhancement or later release |

## Ticket conventions

- Every ticket has a unique ID.
- Each ticket should represent a reasonably self-contained piece of work.
- Tickets should have clear acceptance criteria.
- Dependencies must be completed before implementation begins.
- Avoid implementing unrelated tickets together.
- Update ticket status when work progresses.
- Do not mark tickets complete until their acceptance criteria and relevant tests pass.

## Ticket format

```text
ID:
Title:
Priority:
Status:
Dependencies:

Description:

Acceptance criteria:
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3
```

---

# 2. Delivery overview

| Epic | Name | Priority | Status |
|---|---|---|---|
| 00 | Product discovery | P0 | IN PROGRESS |
| 01 | Architecture and foundations | P0 | TODO |
| 02 | Frontend foundation | P0 | TODO |
| 03 | Authentication and organisations | P0 | TODO |
| 04 | Knowledge management | P0 | TODO |
| 05 | Document processing | P0 | TODO |
| 06 | Search and retrieval | P0 | TODO |
| 07 | AI assistants and chat | P0 | TODO |
| 08 | AI tools and agents | P1 | TODO |
| 09 | Workflow engine | P1 | TODO |
| 10 | Approvals and notifications | P1 | TODO |
| 11 | Usage and costs | P1 | TODO |
| 12 | Security and data protection | P0 | TODO |
| 13 | Testing and AI quality | P0 | TODO |
| 14 | Observability and reliability | P0 | TODO |
| 15 | Cloud infrastructure and deployment | P0 | TODO |
| 16 | Production readiness and launch | P0 | TODO |

---

# 3. Engineering backlog

## EPIC 00 — Product discovery

**Goal:** Establish the requirements, scope and working conventions before implementation.

**Dependencies:** None.

### 00-01 — Finalise product requirements

- Priority: P0
- Status: IN PROGRESS
- Dependencies: None

Acceptance criteria:
- [ ] MVP capabilities and exclusions are documented.
- [ ] Primary user roles are defined.
- [ ] Core user journeys are documented.
- [ ] Requirements are reflected in `docs/PRODUCT_SPEC.md`.

Progress: canonical requirements consolidated and high-level journeys drafted. Decisions PD-01 through PD-06 remain open in the specification. Acceptance criteria remain unchecked pending resolution and review.

Scope: 00-01 establishes capability-level requirements; 00-02 defines detailed release commitments and success criteria; 00-03 expands UX interactions.

### 00-02 — Define MVP boundaries

- Priority: P0
- Status: TODO
- Dependencies: 00-01

Acceptance criteria:
- [ ] MVP scope is clearly separated from later releases.
- [ ] Non-essential features are explicitly deferred.
- [ ] Initial release success criteria are documented.

### 00-03 — Define UX journeys

- Priority: P0
- Status: TODO
- Dependencies: 00-01

Acceptance criteria:
- [ ] Registration and organisation creation flow defined.
- [ ] Knowledge base and document upload flow defined.
- [ ] Assistant creation and chat flow defined.
- [ ] Key error and empty states identified.

### 00-04 — Create initial risk register

- Priority: P1
- Status: TODO
- Dependencies: 00-01

Acceptance criteria:
- [ ] Technical and architectural risks identified.
- [ ] Security and privacy risks identified.
- [ ] AI quality and cost risks identified.
- [ ] Initial mitigations documented.

### 00-05 — Establish engineering conventions

- Priority: P0
- Status: TODO
- Dependencies: None

Acceptance criteria:
- [ ] Git branching and commit conventions documented.
- [ ] Code formatting and linting conventions defined.
- [ ] Testing expectations documented.
- [ ] Documentation conventions established.

---

## EPIC 01 — Architecture and foundations

**Goal:** Establish the repository, architecture and local development environment.

**Dependencies:** EPIC 00.

### 01-01 — Create repository structure

- Priority: P0
- Status: TODO
- Dependencies: 00-05

Acceptance criteria:
- [ ] Frontend, backend, AI service, infrastructure and documentation directories established.
- [ ] Appropriate project-level configuration files created.
- [ ] Repository structure documented.

### 01-02 — Document system architecture

- Priority: P0
- Status: TODO
- Dependencies: 00-01

Acceptance criteria:
- [ ] High-level architecture diagram created.
- [ ] Responsibilities of each service documented.
- [ ] Service communication boundaries documented.
- [ ] Data flow for document ingestion and RAG documented.

### 01-03 — Establish architecture decision records

- Priority: P0
- Status: TODO
- Dependencies: 01-02

Acceptance criteria:
- [ ] ADR template established.
- [ ] Initial architectural decisions recorded.
- [ ] Decision index created in `docs/ADRs/`.

### 01-04 — Configure local development environment

- Priority: P0
- Status: TODO
- Dependencies: 01-01

Acceptance criteria:
- [ ] Docker Compose configuration established.
- [ ] PostgreSQL available locally.
- [ ] Redis available locally if required.
- [ ] Frontend, backend and AI service can run locally.
- [ ] Setup instructions documented.

### 01-05 — Configure PostgreSQL and migrations

- Priority: P0
- Status: TODO
- Dependencies: 01-04

Acceptance criteria:
- [ ] Backend connects to PostgreSQL.
- [ ] Database migration tooling configured.
- [ ] Initial migration executes successfully.
- [ ] Database connection and migration instructions documented.

### 01-06 — Establish configuration and secrets management

- Priority: P0
- Status: TODO
- Dependencies: 01-01

Acceptance criteria:
- [ ] Environment-specific configuration supported.
- [ ] Secrets are not committed to source control.
- [ ] Required environment variables documented.
- [ ] Application startup validates required configuration.

### 01-07 — Establish initial CI pipeline

- Priority: P1
- Status: TODO
- Dependencies: 01-01

Acceptance criteria:
- [ ] Pull requests trigger automated builds.
- [ ] Available automated tests execute in CI.
- [ ] Build and test failures prevent successful checks.
- [ ] CI instructions documented.

---

## EPIC 02 — Frontend foundation

**Goal:** Establish the React application and reusable UI infrastructure.

**Dependencies:** 01-01.

### 02-01 — Initialise React application

- Priority: P0
- Status: TODO
- Dependencies: 01-01

Acceptance criteria:
- [ ] React, TypeScript and Vite configured.
- [ ] Strict TypeScript configuration enabled.
- [ ] Development and production builds work.
- [ ] Linting and formatting configured.

### 02-02 — Configure UI design system

- Priority: P0
- Status: TODO
- Dependencies: 02-01

Acceptance criteria:
- [ ] Tailwind CSS configured.
- [ ] shadcn/ui configured.
- [ ] Base typography, colours and spacing established.
- [ ] Shared component conventions documented.

### 02-03 — Build application shell

- Priority: P0
- Status: TODO
- Dependencies: 02-02

Acceptance criteria:
- [ ] Main application layout implemented.
- [ ] Navigation and sidebar implemented.
- [ ] Responsive layout supported.
- [ ] Loading, error and empty states established.

### 02-04 — Configure routing

- Priority: P0
- Status: TODO
- Dependencies: 02-01

Acceptance criteria:
- [ ] React Router configured.
- [ ] Public and authenticated routes supported.
- [ ] Not-found route implemented.
- [ ] Route protection can be applied.

### 02-05 — Configure API client

- Priority: P0
- Status: TODO
- Dependencies: 02-01

Acceptance criteria:
- [ ] Centralised API client established.
- [ ] Base URL configurable by environment.
- [ ] Authentication headers supported.
- [ ] API errors handled consistently.

### 02-06 — Configure server-state management

- Priority: P1
- Status: TODO
- Dependencies: 02-05

Acceptance criteria:
- [ ] TanStack Query configured.
- [ ] Query and mutation conventions established.
- [ ] Cache invalidation patterns documented.

---

## EPIC 03 — Authentication and organisations

**Goal:** Establish identity, organisation management and tenant access control.

**Dependencies:** EPIC 01 and EPIC 02.

### 03-01 — Integrate OIDC authentication

- Priority: P0
- Status: TODO
- Dependencies: 01-06, 02-04

Acceptance criteria:
- [ ] Authentication provider configured.
- [ ] Users can sign in and sign out.
- [ ] Authentication state persists appropriately.
- [ ] Unauthenticated users cannot access protected routes.

### 03-02 — Implement user profiles

- Priority: P0
- Status: TODO
- Dependencies: 03-01, 01-05

Acceptance criteria:
- [ ] Application user model implemented.
- [ ] Authenticated identities mapped to application users.
- [ ] User profile can be retrieved and updated.

### 03-03 — Implement organisation management

- Priority: P0
- Status: TODO
- Dependencies: 03-02

Acceptance criteria:
- [ ] Organisation model implemented.
- [ ] Users can create organisations.
- [ ] Organisation ownership established.
- [ ] Users can access their organisations.

### 03-04 — Implement organisation memberships

- Priority: P0
- Status: TODO
- Dependencies: 03-03

Acceptance criteria:
- [ ] Organisation membership model implemented.
- [ ] Users can belong to organisations.
- [ ] Membership roles persisted.
- [ ] Membership status is enforced.

### 03-05 — Implement invitations

- Priority: P1
- Status: TODO
- Dependencies: 03-04

Acceptance criteria:
- [ ] Authorised users can invite members.
- [ ] Invitations have an expiry and status.
- [ ] Invitations can be accepted.
- [ ] Unauthorised users cannot invite members.

### 03-06 — Implement role-based access control

- Priority: P0
- Status: TODO
- Dependencies: 03-04

Acceptance criteria:
- [ ] Organisation roles defined.
- [ ] Permission checks implemented in backend.
- [ ] Protected operations reject unauthorised requests.
- [ ] Permission tests cover relevant roles.

### 03-07 — Implement tenant isolation

- Priority: P0
- Status: TODO
- Dependencies: 03-06

Acceptance criteria:
- [ ] Tenant ownership enforced on organisation-owned resources.
- [ ] Cross-tenant access tests implemented.
- [ ] API queries cannot expose another organisation's data.
- [ ] Tenant isolation rules documented.

---

## EPIC 04 — Knowledge management

**Goal:** Allow users to create knowledge bases and manage documents.

**Dependencies:** EPIC 03.

### 04-01 — Implement knowledge base data model

- Priority: P0
- Status: TODO
- Dependencies: 03-07

Acceptance criteria:
- [ ] Knowledge base entity implemented.
- [ ] Organisation relationship established.
- [ ] Migrations created.
- [ ] Ownership and permissions represented.

### 04-02 — Implement knowledge base API

- Priority: P0
- Status: TODO
- Dependencies: 04-01

Acceptance criteria:
- [ ] Create, read, update and delete endpoints implemented.
- [ ] Tenant and permission checks enforced.
- [ ] Validation and error handling implemented.
- [ ] Integration tests added.

### 04-03 — Build knowledge base UI

- Priority: P0
- Status: TODO
- Dependencies: 04-02, 02-03

Acceptance criteria:
- [ ] Users can list knowledge bases.
- [ ] Users can create and edit knowledge bases.
- [ ] Users can delete knowledge bases.
- [ ] Loading, empty and error states implemented.

### 04-04 — Implement document data model

- Priority: P0
- Status: TODO
- Dependencies: 04-01

Acceptance criteria:
- [ ] Document entity implemented.
- [ ] Document version entity implemented.
- [ ] Knowledge base relationship established.
- [ ] Processing status and metadata represented.
- [ ] Migrations created.

### 04-05 — Configure S3 document storage

- Priority: P0
- Status: TODO
- Dependencies: 01-06

Acceptance criteria:
- [ ] S3 bucket configuration established.
- [ ] Application can securely upload and retrieve files.
- [ ] Object keys do not expose sensitive information.
- [ ] Storage permissions are restricted.

### 04-06 — Implement secure document uploads

- Priority: P0
- Status: TODO
- Dependencies: 04-04, 04-05

Acceptance criteria:
- [ ] File type and size validated.
- [ ] Upload permissions checked.
- [ ] Document metadata persisted.
- [ ] Original file stored in S3.
- [ ] Upload failures handled correctly.

### 04-07 — Build document management UI

- Priority: P0
- Status: TODO
- Dependencies: 04-06

Acceptance criteria:
- [ ] Users can upload documents.
- [ ] Documents listed within knowledge bases.
- [ ] Document metadata and processing status displayed.
- [ ] Users can delete documents.
- [ ] Loading and error states implemented.

### 04-08 — Implement document versioning

- Priority: P1
- Status: TODO
- Dependencies: 04-04, 04-06

Acceptance criteria:
- [ ] New uploads can create document versions.
- [ ] Previous versions are identifiable.
- [ ] Current version is clearly defined.
- [ ] Version relationships are preserved.

---

## EPIC 05 — Document processing

**Goal:** Convert uploaded documents into searchable, embedded knowledge.

**Dependencies:** EPIC 04.

### 05-01 — Configure SQS processing queue

- Priority: P0
- Status: TODO
- Dependencies: 01-06

Acceptance criteria:
- [ ] Queue configuration established.
- [ ] Backend can publish processing jobs.
- [ ] Worker can consume messages.
- [ ] Failed message handling configured.

### 05-02 — Implement document processing worker

- Priority: P0
- Status: TODO
- Dependencies: 05-01, 04-06

Acceptance criteria:
- [ ] Worker consumes document processing jobs.
- [ ] Worker retrieves documents securely.
- [ ] Processing errors are captured.
- [ ] Jobs are retryable and idempotent.

### 05-03 — Implement text extraction

- Priority: P0
- Status: TODO
- Dependencies: 05-02

Acceptance criteria:
- [ ] PDF extraction supported.
- [ ] DOCX extraction supported.
- [ ] TXT and Markdown extraction supported.
- [ ] CSV extraction supported.
- [ ] Unsupported or corrupted files handled gracefully.

### 05-04 — Implement text preprocessing

- Priority: P0
- Status: TODO
- Dependencies: 05-03

Acceptance criteria:
- [ ] Extracted text cleaned and normalised.
- [ ] Empty or unusable documents identified.
- [ ] Relevant document metadata preserved.

### 05-05 — Implement document chunking

- Priority: P0
- Status: TODO
- Dependencies: 05-04

Acceptance criteria:
- [ ] Configurable chunking strategy implemented.
- [ ] Chunk size and overlap configurable.
- [ ] Source document references preserved.
- [ ] Chunk metadata persisted.

### 05-06 — Implement embedding generation

- Priority: P0
- Status: TODO
- Dependencies: 05-05, 01-06

Acceptance criteria:
- [ ] Embedding provider integrated.
- [ ] Embeddings generated for document chunks.
- [ ] Model and dimension metadata recorded.
- [ ] API failures and rate limits handled.

### 05-07 — Persist document chunks and vectors

- Priority: P0
- Status: TODO
- Dependencies: 05-06, 01-05

Acceptance criteria:
- [ ] pgvector extension configured.
- [ ] Chunk and embedding records persisted.
- [ ] Document and organisation relationships preserved.
- [ ] Appropriate indexes created.

### 05-08 — Implement processing status and error reporting

- Priority: P0
- Status: TODO
- Dependencies: 05-02, 05-07

Acceptance criteria:
- [ ] Processing status updated throughout lifecycle.
- [ ] Processing failures recorded.
- [ ] API exposes processing status.
- [ ] Frontend displays processing state.

### 05-09 — Implement document deletion cleanup

- Priority: P0
- Status: TODO
- Dependencies: 05-07

Acceptance criteria:
- [ ] Original S3 object deleted.
- [ ] Associated chunks and embeddings deleted.
- [ ] Document metadata removed or retained according to audit requirements.
- [ ] Partial failures handled safely.

### 05-10 — Implement retry and idempotency

- Priority: P0
- Status: TODO
- Dependencies: 05-02, 05-07

Acceptance criteria:
- [ ] Duplicate processing jobs do not create duplicate chunks.
- [ ] Transient failures can be retried.
- [ ] Permanent failures are recorded.
- [ ] Retry behaviour is observable.

---

## EPIC 06 — Search and retrieval

**Goal:** Retrieve relevant document content while respecting permissions.

**Dependencies:** EPIC 05 and EPIC 03.

### 06-01 — Implement semantic search

- Priority: P0
- Status: TODO
- Dependencies: 05-07

Acceptance criteria:
- [ ] Query embeddings generated.
- [ ] Vector similarity search implemented.
- [ ] Configurable top-K results supported.
- [ ] Source metadata returned with results.

### 06-02 — Implement retrieval permission filters

- Priority: P0
- Status: TODO
- Dependencies: 06-01, 03-07

Acceptance criteria:
- [ ] Search results restricted to authorised knowledge bases.
- [ ] Tenant filtering enforced.
- [ ] Permission tests added.
- [ ] Unauthorised document content cannot enter LLM context.

### 06-03 — Implement metadata filtering

- Priority: P1
- Status: TODO
- Dependencies: 06-01

Acceptance criteria:
- [ ] Search supports knowledge base filters.
- [ ] Search supports document filters.
- [ ] Filters can be combined.

### 06-04 — Implement hybrid retrieval

- Priority: P1
- Status: TODO
- Dependencies: 06-01

Acceptance criteria:
- [ ] Keyword retrieval implemented.
- [ ] Semantic and keyword results combined.
- [ ] Ranking strategy configurable.
- [ ] Retrieval quality compared with semantic-only search.

### 06-05 — Create retrieval evaluation dataset

- Priority: P0
- Status: TODO
- Dependencies: 06-01

Acceptance criteria:
- [ ] At least 30 representative questions created.
- [ ] Expected relevant documents or chunks identified.
- [ ] Evaluation dataset version controlled.
- [ ] Repeatable evaluation procedure documented.

### 06-06 — Measure retrieval quality

- Priority: P0
- Status: TODO
- Dependencies: 06-05

Acceptance criteria:
- [ ] Recall@K calculated.
- [ ] Precision@K calculated.
- [ ] MRR calculated.
- [ ] Evaluation results documented.
- [ ] Weak retrieval cases identified.

---

## EPIC 07 — AI assistants and chat

**Goal:** Enable users to ask questions and receive grounded AI responses.

**Dependencies:** EPIC 06 and EPIC 03.

### 07-01 — Implement assistant data model

- Priority: P0
- Status: TODO
- Dependencies: 03-07

Acceptance criteria:
- [ ] Assistant entity implemented.
- [ ] Assistant configuration persisted.
- [ ] Organisation ownership enforced.
- [ ] Knowledge base relationships supported.

### 07-02 — Implement assistant API

- Priority: P0
- Status: TODO
- Dependencies: 07-01

Acceptance criteria:
- [ ] Assistant CRUD implemented.
- [ ] Assistant configuration validated.
- [ ] Access permissions enforced.
- [ ] Integration tests added.

### 07-03 — Build assistant management UI

- Priority: P0
- Status: TODO
- Dependencies: 07-02

Acceptance criteria:
- [ ] Users can create assistants.
- [ ] Users can configure assistant instructions.
- [ ] Users can select knowledge bases.
- [ ] Users can edit and delete assistants.

### 07-04 — Implement conversation persistence

- Priority: P0
- Status: TODO
- Dependencies: 01-05, 07-01

Acceptance criteria:
- [ ] Conversation model implemented.
- [ ] Message model implemented.
- [ ] Conversations linked to users and assistants.
- [ ] Organisation permissions enforced.

### 07-05 — Implement RAG orchestration

- Priority: P0
- Status: TODO
- Dependencies: 06-02, 07-04

Acceptance criteria:
- [ ] User question passed to retrieval pipeline.
- [ ] Relevant authorised chunks retrieved.
- [ ] Context assembled for LLM.
- [ ] LLM response generated using retrieved context.
- [ ] Insufficient context handled explicitly.

### 07-06 — Implement streaming responses

- Priority: P0
- Status: TODO
- Dependencies: 07-05

Acceptance criteria:
- [ ] Backend streams model responses.
- [ ] Frontend consumes streamed responses.
- [ ] Stream errors handled.
- [ ] Incomplete responses are not incorrectly persisted as complete.

### 07-07 — Implement source citations

- Priority: P0
- Status: TODO
- Dependencies: 07-05

Acceptance criteria:
- [ ] Relevant sources associated with answers.
- [ ] Citations identify source documents.
- [ ] Citation metadata includes relevant sections or chunks.
- [ ] Users can navigate to source information.

### 07-08 — Build chat interface

- Priority: P0
- Status: TODO
- Dependencies: 07-06, 07-07

Acceptance criteria:
- [ ] Users can send messages.
- [ ] Responses stream into the UI.
- [ ] Citations are displayed.
- [ ] Loading and error states implemented.

### 07-09 — Implement conversation history

- Priority: P1
- Status: TODO
- Dependencies: 07-04, 07-08

Acceptance criteria:
- [ ] Previous conversations can be listed.
- [ ] Conversations can be reopened.
- [ ] Message history displayed.
- [ ] Access restrictions enforced.

### 07-10 — Implement answer feedback

- Priority: P1
- Status: TODO
- Dependencies: 07-08

Acceptance criteria:
- [ ] Users can submit feedback.
- [ ] Feedback associated with the relevant response.
- [ ] Feedback can be inspected by authorised administrators.

---

## EPIC 08 — AI tools and agents

**Goal:** Give assistants controlled access to application capabilities.

**Dependencies:** EPIC 07.

### 08-01 — Define tool architecture

- Priority: P0
- Status: TODO
- Dependencies: 07-05

Acceptance criteria:
- [ ] Tool interface defined.
- [ ] Tool execution lifecycle documented.
- [ ] Input and output contracts defined.
- [ ] Permission model documented.

### 08-02 — Implement tool registry

- Priority: P0
- Status: TODO
- Dependencies: 08-01

Acceptance criteria:
- [ ] Tools can be registered.
- [ ] Tool schemas validated.
- [ ] Tool availability can be restricted.
- [ ] Invalid tool calls rejected.

### 08-03 — Implement knowledge search tool

- Priority: P0
- Status: TODO
- Dependencies: 08-02, 06-02

Acceptance criteria:
- [ ] Assistant can invoke knowledge search.
- [ ] User permissions enforced.
- [ ] Results retain source metadata.

### 08-04 — Implement model tool calling

- Priority: P1
- Status: TODO
- Dependencies: 08-03

Acceptance criteria:
- [ ] Model can request registered tools.
- [ ] Tool arguments validated.
- [ ] Results returned to model.
- [ ] Tool execution limits enforced.

### 08-05 — Implement execution controls

- Priority: P0
- Status: TODO
- Dependencies: 08-02

Acceptance criteria:
- [ ] Tool permissions enforced independently of model instructions.
- [ ] Timeouts and execution limits configured.
- [ ] Failure behaviour defined.
- [ ] Potentially consequential actions require appropriate safeguards.

### 08-06 — Implement tool tracing

- Priority: P1
- Status: TODO
- Dependencies: 08-04

Acceptance criteria:
- [ ] Tool invocations recorded.
- [ ] Execution duration and outcome recorded.
- [ ] Errors can be inspected.
- [ ] Sensitive values are not exposed in logs.

---

## EPIC 09 — Workflow engine

**Goal:** Allow users to construct and execute persistent AI-powered workflows.

**Dependencies:** EPIC 07 and EPIC 08.

### 09-01 — Define workflow schema

- Priority: P0
- Status: TODO
- Dependencies: 08-01

Acceptance criteria:
- [ ] Workflow node schema defined.
- [ ] Workflow edge schema defined.
- [ ] Node configuration validation defined.
- [ ] Versioning strategy documented.

### 09-02 — Implement workflow data models

- Priority: P0
- Status: TODO
- Dependencies: 09-01

Acceptance criteria:
- [ ] Workflow entity implemented.
- [ ] Workflow version entity implemented.
- [ ] Workflow execution entity implemented.
- [ ] Step execution entity implemented.
- [ ] Migrations created.

### 09-03 — Implement workflow API

- Priority: P0
- Status: TODO
- Dependencies: 09-02

Acceptance criteria:
- [ ] Workflow CRUD implemented.
- [ ] Workflow versions persisted.
- [ ] Execution history accessible.
- [ ] Permissions enforced.

### 09-04 — Build visual workflow editor

- Priority: P1
- Status: TODO
- Dependencies: 09-03, 02-02

Acceptance criteria:
- [ ] React Flow integrated.
- [ ] Nodes can be added and configured.
- [ ] Nodes can be connected.
- [ ] Workflow definitions can be saved and loaded.
- [ ] Invalid connections can be identified.

### 09-05 — Implement workflow validation

- Priority: P0
- Status: TODO
- Dependencies: 09-01

Acceptance criteria:
- [ ] Required start and output conditions validated.
- [ ] Node configuration validated.
- [ ] Invalid graph structures rejected.
- [ ] Validation errors identify relevant nodes.

### 09-06 — Implement workflow execution engine

- Priority: P0
- Status: TODO
- Dependencies: 09-02, 09-05

Acceptance criteria:
- [ ] Workflow executions persisted.
- [ ] Step state persisted.
- [ ] Execution can resume after interruption.
- [ ] Errors and execution outcomes recorded.
- [ ] Duplicate execution is controlled.

### 09-07 — Implement core workflow nodes

- Priority: P0
- Status: TODO
- Dependencies: 09-06

Acceptance criteria:
- [ ] Input node implemented.
- [ ] Retrieval node implemented.
- [ ] LLM node implemented.
- [ ] Condition node implemented.
- [ ] Output node implemented.
- [ ] Node failures handled consistently.

### 09-08 — Implement tool execution node

- Priority: P1
- Status: TODO
- Dependencies: 09-07, 08-05

Acceptance criteria:
- [ ] Workflow can invoke registered tools.
- [ ] Permissions are enforced.
- [ ] Execution results are persisted.
- [ ] Failures are handled safely.

### 09-09 — Implement approval node

- Priority: P1
- Status: TODO
- Dependencies: 09-07, EPIC 10

Acceptance criteria:
- [ ] Workflow pauses at approval node.
- [ ] Execution state persisted.
- [ ] Workflow can resume after approval.
- [ ] Rejection terminates or redirects execution appropriately.

### 09-10 — Implement execution history

- Priority: P0
- Status: TODO
- Dependencies: 09-06

Acceptance criteria:
- [ ] Workflow runs can be inspected.
- [ ] Individual step status visible.
- [ ] Errors and outputs inspectable.
- [ ] Execution timestamps recorded.

### 09-11 — Implement retry and cancellation

- Priority: P1
- Status: TODO
- Dependencies: 09-06

Acceptance criteria:
- [ ] Eligible failed steps can retry.
- [ ] Workflow execution can be cancelled.
- [ ] Retry does not duplicate unsafe side effects.
- [ ] Cancellation state is persisted.

### 09-12 — Implement workflow scheduling

- Priority: P2
- Status: TODO
- Dependencies: 09-06

Acceptance criteria:
- [ ] Workflow schedules can be configured.
- [ ] Scheduled executions are persisted.
- [ ] Duplicate scheduled runs are prevented.

---

## EPIC 10 — Approvals and notifications

**Goal:** Introduce human oversight into workflow execution.

**Dependencies:** EPIC 09.

### 10-01 — Implement approval data model

- Priority: P1
- Status: TODO
- Dependencies: 09-02

Acceptance criteria:
- [ ] Approval request model implemented.
- [ ] Reviewer and workflow relationships established.
- [ ] Decision and timestamp persisted.

### 10-02 — Implement approval API

- Priority: P1
- Status: TODO
- Dependencies: 10-01

Acceptance criteria:
- [ ] Pending requests can be retrieved.
- [ ] Authorised reviewers can approve or reject.
- [ ] Decisions are recorded.
- [ ] Duplicate decisions prevented.

### 10-03 — Build approval UI

- Priority: P1
- Status: TODO
- Dependencies: 10-02

Acceptance criteria:
- [ ] Pending approvals listed.
- [ ] Relevant workflow context displayed.
- [ ] Reviewers can approve or reject.
- [ ] Decision status displayed.

### 10-04 — Implement workflow resumption

- Priority: P1
- Status: TODO
- Dependencies: 10-02, 09-09

Acceptance criteria:
- [ ] Approved workflows resume.
- [ ] Rejected workflows follow defined rejection behaviour.
- [ ] Approval state remains consistent after interruptions.
- [ ] Resumption is idempotent.

### 10-05 — Implement in-app notifications

- Priority: P1
- Status: TODO
- Dependencies: 10-01

Acceptance criteria:
- [ ] Notification model implemented.
- [ ] Approval requests generate notifications.
- [ ] Users can view notifications.
- [ ] Read/unread state supported.

---

## EPIC 11 — Usage and costs

**Goal:** Track and control platform consumption.

**Dependencies:** EPIC 07 and EPIC 05.

### 11-01 — Implement usage tracking

- Priority: P1
- Status: TODO
- Dependencies: 07-05, 05-06

Acceptance criteria:
- [ ] LLM token usage recorded.
- [ ] Embedding usage recorded.
- [ ] Document processing usage recorded.
- [ ] Usage associated with organisation.

### 11-02 — Implement cost calculation

- Priority: P1
- Status: TODO
- Dependencies: 11-01

Acceptance criteria:
- [ ] Model-specific pricing configuration maintained.
- [ ] Estimated costs calculated.
- [ ] Usage records retain model and pricing information.

### 11-03 — Implement usage limits

- Priority: P1
- Status: TODO
- Dependencies: 11-01

Acceptance criteria:
- [ ] Organisation usage limits configurable.
- [ ] Limits checked before expensive operations.
- [ ] Limit violations handled predictably.

### 11-04 — Build usage dashboard

- Priority: P1
- Status: TODO
- Dependencies: 11-02

Acceptance criteria:
- [ ] Organisation usage displayed.
- [ ] Estimated costs displayed.
- [ ] Usage breakdown by operation available.

---

## EPIC 12 — Security and data protection

**Goal:** Protect user data and prevent unauthorised access or execution.

**Dependencies:** Security controls begin in EPIC 03 and continue throughout development.

### 12-01 — Complete threat model

- Priority: P0
- Status: TODO
- Dependencies: 01-02

Acceptance criteria:
- [ ] Main assets and trust boundaries identified.
- [ ] Threats documented.
- [ ] Mitigations prioritised.
- [ ] Threat model stored in `docs/SECURITY.md` or linked documentation.

### 12-02 — Secure document processing

- Priority: P0
- Status: TODO
- Dependencies: 05-02

Acceptance criteria:
- [ ] Upload validation implemented.
- [ ] Unsafe file handling mitigated.
- [ ] Processing failures cannot expose other tenants' data.
- [ ] File processing has appropriate resource limits.

### 12-03 — Address prompt injection

- Priority: P0
- Status: TODO
- Dependencies: 07-05

Acceptance criteria:
- [ ] Retrieved content treated as untrusted.
- [ ] Instructions from documents cannot grant permissions.
- [ ] Prompt injection test cases implemented.
- [ ] Mitigations documented.

### 12-04 — Secure AI tool execution

- Priority: P0
- Status: TODO
- Dependencies: 08-05

Acceptance criteria:
- [ ] Authorisation enforced in application code.
- [ ] Tool inputs validated.
- [ ] Tool execution restricted to permitted operations.
- [ ] Sensitive operations appropriately safeguarded.

### 12-05 — Implement audit logging

- Priority: P0
- Status: TODO
- Dependencies: 03-06

Acceptance criteria:
- [ ] Security-sensitive operations recorded.
- [ ] Actor, action, resource and timestamp captured.
- [ ] Audit records protected against ordinary modification.
- [ ] Sensitive values excluded.

### 12-06 — Implement data retention and deletion

- Priority: P0
- Status: TODO
- Dependencies: 04-04, 05-07

Acceptance criteria:
- [ ] Document deletion behaviour defined.
- [ ] User and organisation deletion behaviour defined.
- [ ] Derived data and embeddings included.
- [ ] Retention requirements documented.

### 12-07 — Conduct security testing

- Priority: P0
- Status: TODO
- Dependencies: 12-01, 12-02, 12-03, 12-04

Acceptance criteria:
- [ ] Authentication and authorisation tested.
- [ ] Tenant isolation tested.
- [ ] File handling tested.
- [ ] AI tool permissions tested.
- [ ] Critical vulnerabilities resolved.

---

## EPIC 13 — Testing and AI quality

**Goal:** Establish confidence in software behaviour and AI output quality.

**Dependencies:** Testing begins with each implementation epic.

### 13-01 — Backend unit tests

- Priority: P0
- Status: TODO
- Dependencies: 01-01

Acceptance criteria:
- [ ] Core business logic has unit tests.
- [ ] Permission logic tested.
- [ ] Error handling tested.

### 13-02 — Backend integration tests

- Priority: P0
- Status: TODO
- Dependencies: 01-05

Acceptance criteria:
- [ ] Database integration tested.
- [ ] API behaviour tested.
- [ ] Authentication and permission scenarios tested.

### 13-03 — AI service tests

- Priority: P0
- Status: TODO
- Dependencies: 05-03

Acceptance criteria:
- [ ] Extraction tests implemented.
- [ ] Chunking tests implemented.
- [ ] Embedding integration tested.
- [ ] AI orchestration tested.

### 13-04 — AI evaluation tests

- Priority: P0
- Status: TODO
- Dependencies: 06-05, 07-05

Acceptance criteria:
- [ ] Retrieval quality evaluated.
- [ ] Answer relevance evaluated.
- [ ] Citation correctness evaluated.
- [ ] Evaluation results repeatable.

### 13-05 — Frontend tests

- Priority: P1
- Status: TODO
- Dependencies: 02-01

Acceptance criteria:
- [ ] Critical components tested.
- [ ] Key interaction flows tested.
- [ ] Error and loading states tested.

### 13-06 — End-to-end tests

- Priority: P0
- Status: TODO
- Dependencies: 07-08

Acceptance criteria:
- [ ] Registration and organisation flow tested.
- [ ] Document upload and processing flow tested.
- [ ] Assistant creation and chat flow tested.
- [ ] Citation display tested.

### 13-07 — Load and performance testing

- Priority: P1
- Status: TODO
- Dependencies: 07-08, 14-03

Acceptance criteria:
- [ ] Representative load scenarios defined.
- [ ] API performance measured.
- [ ] Document processing performance measured.
- [ ] Bottlenecks documented.

---

## EPIC 14 — Observability and reliability

**Goal:** Make the system diagnosable, measurable and recoverable.

**Dependencies:** EPIC 01. Implement incrementally.

### 14-01 — Implement structured logging

- Priority: P0
- Status: TODO
- Dependencies: 01-01

Acceptance criteria:
- [ ] Services emit structured logs.
- [ ] Correlation identifiers supported.
- [ ] Sensitive data excluded.

### 14-02 — Implement distributed tracing

- Priority: P1
- Status: TODO
- Dependencies: 14-01

Acceptance criteria:
- [ ] OpenTelemetry configured.
- [ ] Trace context propagated between services.
- [ ] External calls and background jobs traceable.

### 14-03 — Implement application metrics

- Priority: P1
- Status: TODO
- Dependencies: 14-01

Acceptance criteria:
- [ ] Request latency and error metrics available.
- [ ] Queue and worker metrics available.
- [ ] AI usage metrics available.

### 14-04 — Configure alerting

- Priority: P1
- Status: TODO
- Dependencies: 14-03

Acceptance criteria:
- [ ] Critical service failures trigger alerts.
- [ ] Queue processing failures monitored.
- [ ] Alert thresholds documented.

### 14-05 — Implement health checks

- Priority: P0
- Status: TODO
- Dependencies: 01-01

Acceptance criteria:
- [ ] API health endpoint available.
- [ ] Dependency health checks implemented.
- [ ] Worker health observable.

### 14-06 — Implement backup and recovery

- Priority: P0
- Status: TODO
- Dependencies: 15-05

Acceptance criteria:
- [ ] Database backups configured.
- [ ] Recovery procedure documented.
- [ ] Restore process tested.
- [ ] File storage recovery considerations documented.

---

## EPIC 15 — Cloud infrastructure and deployment

**Goal:** Deploy the application to a production AWS environment.

**Dependencies:** EPIC 01. Production deployment follows MVP implementation.

### 15-01 — Define production AWS architecture

- Priority: P0
- Status: TODO
- Dependencies: 01-02

Acceptance criteria:
- [ ] Production architecture documented.
- [ ] Network and security boundaries defined.
- [ ] Required AWS services identified.
- [ ] Environment separation defined.

### 15-02 — Implement Terraform infrastructure

- Priority: P0
- Status: TODO
- Dependencies: 15-01

Acceptance criteria:
- [ ] Terraform project configured.
- [ ] Infrastructure resources defined as code.
- [ ] Configuration separated by environment.
- [ ] Secrets handled securely.

### 15-03 — Containerise services

- Priority: P0
- Status: TODO
- Dependencies: 01-04

Acceptance criteria:
- [ ] Frontend deployment image or hosting artefact produced.
- [ ] .NET API containerised.
- [ ] Python service containerised.
- [ ] Containers build reproducibly.

### 15-04 — Deploy ECS services

- Priority: P0
- Status: TODO
- Dependencies: 15-02, 15-03

Acceptance criteria:
- [ ] API deployed to ECS.
- [ ] AI service deployed to ECS.
- [ ] Health checks configured.
- [ ] Service logs accessible.

### 15-05 — Configure production database

- Priority: P0
- Status: TODO
- Dependencies: 15-02

Acceptance criteria:
- [ ] Managed PostgreSQL provisioned.
- [ ] pgvector supported.
- [ ] Database access restricted.
- [ ] Backups configured.

### 15-06 — Configure production S3 and SQS

- Priority: P0
- Status: TODO
- Dependencies: 15-02

Acceptance criteria:
- [ ] S3 storage provisioned.
- [ ] SQS queues provisioned.
- [ ] IAM permissions restricted.
- [ ] Application connectivity verified.

### 15-07 — Implement deployment pipeline

- Priority: P0
- Status: TODO
- Dependencies: 15-04

Acceptance criteria:
- [ ] CI builds and tests services.
- [ ] Deployment triggered through controlled pipeline.
- [ ] Deployment failures are visible.
- [ ] Rollback procedure documented.

### 15-08 — Configure domain and HTTPS

- Priority: P0
- Status: TODO
- Dependencies: 15-04

Acceptance criteria:
- [ ] Application domain configured.
- [ ] HTTPS enabled.
- [ ] API endpoints accessible securely.
- [ ] Environment configuration verified.

---

## EPIC 16 — Production readiness and launch

**Goal:** Verify the platform before production release.

**Dependencies:** EPICs 12–15 and MVP functionality.

### 16-01 — Complete acceptance testing

- Priority: P0
- Status: TODO
- Dependencies: 13-06

Acceptance criteria:
- [ ] All MVP user journeys pass.
- [ ] Critical defects resolved.
- [ ] Release acceptance documented.

### 16-02 — Complete production security review

- Priority: P0
- Status: TODO
- Dependencies: 12-07

Acceptance criteria:
- [ ] Critical security issues resolved.
- [ ] Tenant isolation verified.
- [ ] Production secrets and access reviewed.
- [ ] Security sign-off documented.

### 16-03 — Verify performance targets

- Priority: P0
- Status: TODO
- Dependencies: 13-07

Acceptance criteria:
- [ ] API performance measured.
- [ ] AI response performance measured.
- [ ] Document processing performance measured.
- [ ] Performance limitations documented.

### 16-04 — Verify monitoring and alerting

- Priority: P0
- Status: TODO
- Dependencies: 14-04

Acceptance criteria:
- [ ] Critical services monitored.
- [ ] Alerts tested.
- [ ] Operational dashboards available.

### 16-05 — Complete operational documentation

- Priority: P0
- Status: TODO
- Dependencies: 14-06

Acceptance criteria:
- [ ] Deployment instructions complete.
- [ ] Recovery instructions complete.
- [ ] Troubleshooting guide available.
- [ ] Known limitations documented.

### 16-06 — Production launch

- Priority: P0
- Status: TODO
- Dependencies: 16-01, 16-02, 16-03, 16-04, 16-05

Acceptance criteria:
- [ ] Production deployment successful.
- [ ] Critical user journeys verified.
- [ ] Monitoring operational.
- [ ] Release documented.

### 16-07 — Post-launch review

- Priority: P1
- Status: TODO
- Dependencies: 16-06

Acceptance criteria:
- [ ] Initial operational issues reviewed.
- [ ] Performance and usage reviewed.
- [ ] Improvements prioritised.
- [ ] Next development milestone agreed.

---

# 4. Dependency and delivery order

The backlog is organised by epic, but implementation should follow the dependencies below.

```text
EPIC 00 — Product discovery
       |
EPIC 01 — Architecture and foundations
       |
       +-------------------+
       |                   |
EPIC 02 — Frontend     EPIC 03 — Authentication
       |                   |
       +---------+---------+
                 |
       EPIC 04 — Knowledge management
                 |
       EPIC 05 — Document processing
                 |
       EPIC 06 — Search and retrieval
                 |
       EPIC 07 — AI assistants and chat
                 |
       EPIC 08 — AI tools and agents
                 |
       EPIC 09 — Workflow engine
                 |
       EPIC 10 — Approvals and notifications
```

Supporting work runs alongside implementation:

- EPIC 12: Security.
- EPIC 13: Testing and AI quality.
- EPIC 14: Observability and reliability.
- EPIC 15: Infrastructure and deployment.
- EPIC 11: Usage and costs.

EPIC 16 begins when the release scope is implemented and the production prerequisites are satisfied.

Dependencies are not a reason to postpone security, testing or observability until the end. These should be incorporated into each relevant implementation task.

---

# 5. Initial implementation sequence

The first development cycle should focus on establishing a working foundation.

| Order | Ticket | Work |
|---|---|---|
| 1 | 00-01 | Finalise product requirements |
| 2 | 00-02 | Define MVP boundaries |
| 3 | 00-03 | Define UX journeys |
| 4 | 00-04 | Create initial risk register |
| 5 | 00-05 | Establish engineering conventions |
| 6 | 01-01 | Create repository structure |
| 7 | 01-02 | Document system architecture |
| 8 | 01-03 | Establish ADRs |
| 9 | 01-04 | Configure local development |
| 10 | 01-05 | Configure PostgreSQL and migrations |
| 11 | 01-06 | Configure settings and secrets |
| 12 | 02-01 | Initialise React application |
| 13 | 02-02 | Configure UI design system |
| 14 | 02-03 | Build application shell |
| 15 | 02-04 | Configure routing |
| 16 | 02-05 | Configure API client |
| 17 | 03-01 | Integrate authentication |

Complete EPIC 00 before EPIC 01, as required by the epic dependency. Ticket 00-05 has no dependency and can be completed independently; this sequence does not add a new dependency.

Do not start all these tickets simultaneously. Complete the foundational work in manageable increments.

---

# 6. Current project status

**Current milestone:** M1 — Functional MVP

**Current epic:** EPIC 00 — Product discovery

**Active ticket:** 00-01 — Finalise product requirements

**Project status:** Product discovery in progress

## Completed

- [x] Initial product specification created.
- [x] Initial technology stack selected.
- [x] High-level architecture proposed.
- [x] Initial engineering backlog established.

## In progress

- 00-01: requirements and high-level journeys drafted; product decisions pending.

## Next actions

1. Complete EPIC 00.
2. Establish the repository and documentation structure.
3. Complete the architecture foundations.
4. Configure the local development environment.
5. Begin authentication and organisation management.

## Blockers

No technical prerequisite blocks discovery. Product decisions PD-01 through PD-06 must be resolved before 00-01 can be completed. Detailed design documents will be created by the relevant foundation/security tickets.

---

# 7. Backlog maintenance rules

1. Keep this file aligned with the actual implementation.
2. Update status when ticket progress changes.
3. Add newly discovered work as tickets rather than burying it in notes.
4. Record architectural changes in ADRs.
5. Do not silently remove or rewrite existing ticket IDs.
6. Split tickets that become too large or contain unrelated work.
7. Add dependencies when new implementation requirements emerge.
8. Keep completed work in the backlog for traceability.
9. Keep implementation-specific details in code, tests and relevant documentation.
10. Review the backlog at milestone boundaries.

**Codex instruction:** Treat ticket IDs as stable references. When asked to implement a ticket, read its acceptance criteria, inspect dependencies and relevant documentation, and work only within its scope unless explicitly instructed otherwise.