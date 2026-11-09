# AI Knowledge & Workflow Platform

**Product requirements · Target architecture · Delivery roadmap**

Discovery draft under 00-01. This document describes intended behaviour; no application capabilities are implemented. The root `BACKLOG.md` is the sole source of ticket status and acceptance criteria.

| Attribute | Decision |
|---|---|
| Product | Multi-tenant AI knowledge and workflow platform |
| Architecture | Modular monolith + separate AI service |
| Backend | ASP.NET Core / C# |
| AI service | Python / FastAPI |
| Frontend | React / TypeScript |
| Database | PostgreSQL + pgvector |
| Infrastructure | AWS |
| Delivery approach | Incremental, test-driven, production-oriented |

---

# 1. Product overview

## Vision

Build a multi-tenant SaaS platform that allows businesses to centralise internal knowledge, interact with it through AI assistants, and automate business processes using configurable AI-powered workflows.

The platform should prioritise **useful, trustworthy AI grounded in company data**, with appropriate permissions, visibility and human oversight.

## Core capabilities

1. **Knowledge management** — Upload, organise, version and manage business documents.
2. **AI assistants** — Create assistants that answer questions using approved knowledge sources, with citations.
3. **AI tools** — Allow assistants to use controlled application capabilities.
4. **Workflow automation** — Build and execute workflows combining retrieval, AI generation, conditions and tools.
5. **Human approval** — Require human review before sensitive or consequential actions.
6. **Administration** — Manage organisations, users, permissions, usage and costs.

## Users and roles

| Role | Responsibilities |
|---|---|
| Owner | Organisation settings, billing and administration |
| Admin | Users, permissions and knowledge management |
| Member | Use assistants and permitted workflows |
| Workflow manager | Create and manage workflows |
| Reviewer | Review and approve workflow actions |

An individual may hold multiple roles.

## MVP boundaries

**MVP:**
- Authentication and organisation management.
- Knowledge bases and document uploads.
- Background document processing and vector indexing.
- AI assistant with RAG-based answers and citations.
- Conversation history and basic assistant configuration.

**Subsequent releases:**
- Multiple assistants and advanced retrieval.
- Tool calling and agent capabilities.
- Visual workflow builder and execution engine.
- Human approvals and notifications.
- Usage and cost management.

Do not attempt to build the entire platform before validating the document-to-answer experience.


## Primary roles and release applicability

Owner, Admin and Member are the initial organisation roles. Workflow manager and Reviewer apply to the later workflow/approval release. The responsibilities above are a starting point; the detailed permission matrix remains open. Billing responsibility does not commit M1 to implementing billing.

## Core user journeys — 00-01

These capability-level journeys are expanded into detailed interactions and recovery states by 00-03.

| Journey | Main steps and expected outcome | Principal failure cases |
|---|---|---|
| Registration and organisation creation | A new user authenticates, creates an organisation and receives its ownership membership. The user enters that organisation context. | Authentication or creation failure must not grant access or leave a usable organisation without an owner. Registration policy remains open. |
| Knowledge base and document upload | An authorised user creates/selects a knowledge base and uploads a supported file. Access and file constraints are checked before asynchronous processing. | Invalid files and unauthorised requests are rejected. An empty collection is distinguishable from a failed request. |
| Document processing | An authorised user follows processing status through extraction, chunking and indexing. | Failures expose actionable status without marking incomplete content ready for retrieval. Processing tickets define retries. |
| Assistant setup | An authorised user configures an assistant and selects permitted knowledge bases; configuration is persisted. | Configuration cannot grant access beyond the user's permissions. Empty sources and invalid settings need clear handling. Assistant count and configuration permissions remain open. |
| Question and citations | An authorised user asks a question, receives a streamed grounded answer and inspects accessible source documents/sections. | Insufficient evidence is explicit. Access denial and model/stream failure must be distinguishable from a successful answer. |
| Conversation history | A user reopens a persisted conversation they are authorised to access. | Current permissions still apply. Visibility, retention and handling of unavailable sources remain open decisions. |

## Open product decisions — required to complete 00-01

Existing MVP capabilities and later-release exclusions remain the baseline. These questions are unresolved, not approved product behaviour.

| ID | Decision required | Reason |
|---|---|---|
| PD-01 | Identify the initial customer/user group, concrete knowledge-question use case and representative non-sensitive documents/questions. | Grounds requirements and subsequent retrieval evaluation in a practical scenario. |
| PD-02 | Confirm registration/joining policy, invitations and role/resource permissions, including assistant creation, uploads, knowledge access and conversation visibility. | Defines who may perform each operation. |
| PD-03 | Confirm one assistant per organisation versus multiple assistants in M1. | MVP exclusions defer multiple assistants while management tickets and the roadmap use plural assistants. |
| PD-04 | Confirm M1 file formats from PDF, DOCX, TXT, Markdown and CSV; upload limits; scanned-PDF/OCR handling; and versioning scope. | The under-10MB performance target is not an upload limit. Versioning is separately tracked in 04-08. |
| PD-05 | Confirm minimum M1 usage metering and expense limits versus later user-facing usage/cost management. | PROJECT.md requires tracking throughout development while milestone descriptions defer the feature. |
| PD-06 | Confirm retention/deletion for documents, derived data, conversations, users and organisations, and acceptable external model-provider data handling. | Establishes privacy expectations and deletion behaviour. |

Record decisions here before completing 00-01. Ticket 00-02 defines detailed release commitments and measurable success criteria; 00-03 details UX; 00-04 records risks and mitigations. Architecture, schema and threat modelling remain in their own tickets. Security, tests and observability apply throughout M1; M3 groups production verification, not the start of those controls.

---

# 2. Architecture and technology

## Technology choices

| Layer | Technology | Purpose |
|---|---|---|
| Frontend | React, TypeScript, Vite | Application UI |
| Styling | Tailwind CSS, shadcn/ui | Design system |
| Data fetching | TanStack Query | Server state |
| Routing | React Router | Navigation |
| Workflow UI | React Flow | Visual workflow editor |
| Main API | ASP.NET Core / C# | Business logic and application API |
| AI service | Python / FastAPI | AI orchestration and document processing |
| AI orchestration | LangGraph, where useful | Stateful agent execution |
| LLM / embeddings | OpenAI API | Generation and embeddings |
| Database | PostgreSQL | Application and workflow data |
| Vector search | pgvector | Semantic retrieval |
| File storage | AWS S3 | Original documents |
| Messaging | AWS SQS | Durable background jobs |
| Cache | Redis | Caching and short-lived coordination |
| Authentication | Cognito / OIDC | Identity |
| Hosting | AWS ECS Fargate | Containerised services |
| Infrastructure | Terraform | Infrastructure as code |
| CI/CD | GitHub Actions | Build, test and deployment |
| Monitoring | OpenTelemetry, CloudWatch | Logs, metrics and tracing |

## Logical architecture

```text
                    React Frontend
                          |
                    ASP.NET Core API
                          |
          +---------------+----------------+
          |               |                |
      PostgreSQL       AWS S3          AI Service
      + pgvector       Documents       FastAPI
          |                                |
          |                         OpenAI API
          |                                |
          +---------- AWS SQS -------------+
                          |
                 Background Workers
                 - Document processing
                 - Workflow execution
                 - Notifications
```

## Architectural principles

- Use a **modular monolith** for the main .NET application. Avoid premature microservice decomposition.
- Keep AI-specific processing in a separate Python service.
- Use SQS for durable asynchronous jobs; Redis must not be the source of truth for workflow state.
- Store application data and vector embeddings in PostgreSQL.
- Store original documents in S3.
- Keep workflow execution state persistent and recoverable.
- Enforce permissions in the application, not through AI prompts.
- Use interfaces and clear service boundaries to make future changes possible.

## Suggested repository structure

```text
/
├── frontend/
├── backend/
│   ├── Api/
│   ├── Modules/
│   ├── Infrastructure/
│   └── Tests/
├── ai-service/
│   ├── app/
│   ├── workers/
│   └── tests/
├── infrastructure/
│   └── terraform/
├── docs/
│   ├── ARCHITECTURE.md
│   ├── DATA_MODEL.md
│   ├── API.md
│   ├── SECURITY.md
│   └── ADRs/
└── docker-compose.yml
```

This is a proposed starting structure, not a requirement to create every directory immediately.

---

# 3. Core system design

## 3.1 Document ingestion

Documents must be processed asynchronously.

```text
Upload
  ↓
Validate permissions and file
  ↓
Store original in S3
  ↓
Create processing job
  ↓
Publish job to SQS
  ↓
Extract text
  ↓
Clean and normalise
  ↓
Split into chunks
  ↓
Generate embeddings
  ↓
Store chunks + vectors in PostgreSQL
  ↓
Mark document as processed
```

Initial supported formats:
- PDF
- DOCX
- TXT
- Markdown
- CSV

Requirements:
- Track processing status and errors.
- Support document versioning.
- Prevent duplicate processing where appropriate.
- Make processing jobs retryable and idempotent.
- Delete associated chunks and vectors when a document is deleted.
- Preserve document and chunk metadata for citations.

## 3.2 Retrieval-augmented generation (RAG)

```text
User question
     ↓
Authenticate and check permissions
     ↓
Generate query embedding
     ↓
Retrieve relevant chunks
     ↓
Apply access and metadata filters
     ↓
Construct grounded context
     ↓
Call LLM
     ↓
Return answer + citations
```

Requirements:
- Semantic retrieval using pgvector.
- Metadata filtering.
- Hybrid search (keyword + semantic) in a later iteration.
- Configurable retrieval parameters.
- Citations linked to source documents and relevant sections.
- No access to documents outside the user's permissions.
- Explicit handling of insufficient evidence.

Build a retrieval evaluation dataset of at least 30 representative questions. Measure Recall@K, Precision@K and MRR before tuning retrieval.

## 3.3 AI assistants

Each assistant should have:
- Name, description and instructions.
- Configured LLM and generation settings.
- Access to selected knowledge bases.
- Optional enabled tools.
- Conversation history.
- Usage tracking.

Chat requirements:
- Streaming responses.
- Persistent conversations and messages.
- Source citations.
- Feedback on answers.
- Context management and configurable conversation limits.

## 3.4 AI tools and agents

Assistants may use a controlled registry of application tools.

Initial tools:
- Search knowledge bases.
- Retrieve document content.
- Other explicitly authorised application operations.

Requirements:
- Define tools with validated input/output schemas.
- Check permissions before execution.
- Restrict tool access by assistant and user.
- Apply execution limits and timeouts.
- Log tool calls and results.
- Treat document content and retrieved information as untrusted input.
- Do not allow the model to bypass application permissions.

## 3.5 Workflow engine

Workflows combine predefined nodes into executable processes.

Initial node types:

| Node | Purpose |
|---|---|
| Start | Workflow entry point |
| Input | Accept user or external data |
| Retrieval | Search knowledge bases |
| LLM | Generate or transform content |
| Condition | Branch based on an expression |
| Approval | Pause for human review |
| Tool | Execute an authorised tool |
| Output | Return or store results |

Requirements:
- Visual workflow editor using React Flow.
- Versioned workflow definitions.
- Validation before execution.
- Persistent execution and step state.
- Execution history and logs.
- Retry failed steps where safe.
- Cancellation support.
- Error handling and timeouts.
- Resume execution after approval.

Scheduled and event-triggered workflows are later enhancements.

## 3.6 Human approval

Certain workflow actions must pause for review.

Requirements:
- Create approval requests with relevant context.
- Allow authorised reviewers to approve or reject.
- Record reviewer, decision and timestamp.
- Resume or terminate the workflow appropriately.
- Notify relevant users.
- Maintain an audit trail.

## 3.7 Usage and cost management

Track:
- LLM model and token usage.
- Embedding usage.
- Estimated AI costs.
- Document processing usage.
- Workflow execution counts.

Provide organisation-level usage summaries and configurable limits.

---

# 4. Data model

Initial logical entities:

| Entity | Responsibility |
|---|---|
| User | User identity |
| Organisation | Tenant |
| OrganisationMember | User membership and role |
| KnowledgeBase | Document collection |
| KnowledgeBaseMember | Knowledge base permissions |
| Document | Logical document |
| DocumentVersion | Uploaded versions and metadata |
| DocumentChunk | Extracted text and embedding |
| Assistant | Assistant configuration |
| AssistantKnowledgeBase | Assistant data access |
| Conversation | Chat session |
| Message | Conversation message |
| MessageSource | Citations |
| Workflow | Workflow identity |
| WorkflowVersion | Versioned workflow definition |
| WorkflowExecution | Workflow run |
| WorkflowStepExecution | Individual step state |
| ApprovalRequest | Human approval |
| UsageRecord | Consumption and cost |
| AuditLog | Security-sensitive actions |

## Data design rules

- Use UUID primary keys.
- Include `OrganisationId` on tenant-owned records.
- Enforce tenant isolation on every relevant query and operation.
- Consider PostgreSQL Row-Level Security as defence in depth.
- Use explicit relationships and foreign keys.
- Store embedding model and dimensions as metadata.
- Keep workflow definitions versioned and execution records immutable where practical.
- Define retention and deletion behaviour for uploaded files and derived data.

---

# 5. Non-functional requirements

| Area | Requirement |
|---|---|
| Security | Authentication, authorisation, tenant isolation |
| Privacy | Controlled document access and data deletion |
| Reliability | Retryable background jobs and recoverable workflows |
| Performance | API p95 under 500ms, excluding external AI processing |
| AI responsiveness | Target first token under 3 seconds under normal conditions |
| Document processing | Target ordinary documents under 10MB processed within 60 seconds |
| Availability | Initial production target of 99.5% |
| Observability | Structured logs, metrics and distributed tracing |
| Accessibility | Keyboard navigation and accessible UI components |
| Maintainability | Modular code, automated tests and documented decisions |
| Cost | Track and limit expensive AI operations |

These are initial targets, to be validated through testing rather than assumed guarantees.

---

# 6. Engineering backlog

See [BACKLOG.md](../BACKLOG.md) for ticket IDs, priorities, dependencies, acceptance criteria and status. Priority alone does not determine MVP inclusion.

---

# 7. Delivery roadmap

Implement in dependency order rather than starting all epics simultaneously.

| Phase | Scope | Outcome |
|---|---|---|
| 1. Inception | EPIC 00–01 | Requirements and development foundations |
| 2. Application foundation | EPIC 02–03 | Running application with authentication and organisations |
| 3. Knowledge platform | EPIC 04–06 | Upload, process and search documents |
| 4. AI assistant | EPIC 07–08 | Grounded AI conversations and controlled tools |
| 5. Workflow platform | EPIC 09–10 | Visual workflows and human approval |
| 6. Administration | EPIC 11 | Usage and cost visibility |
| 7. Hardening | EPIC 12–14 | Security, quality and reliability |
| 8. Release | EPIC 15–16 | Production deployment |

## Milestones

**M1 — Functional MVP**
- Users can register and create organisations.
- Users can create knowledge bases and upload documents.
- Documents are processed and indexed.
- Users can create assistants and ask questions.
- Answers include citations.

**M2 — Advanced platform**
- Multiple assistants and advanced retrieval.
- Controlled tool calling.
- Visual workflow creation and execution.
- Human approval and workflow resumption.
- Usage tracking.

**M3 — Production release**
- Tenant isolation and security controls verified.
- Automated tests and AI evaluation in place.
- Monitoring, backups and CI/CD operational.
- Production deployment and documentation complete.

---

# 8. Definition of Done

A ticket is complete when:

- [ ] Acceptance criteria are satisfied.
- [ ] Relevant automated tests pass.
- [ ] Permissions and tenant isolation are considered.
- [ ] Errors and edge cases are handled.
- [ ] No secrets or sensitive data are exposed.
- [ ] Code follows established conventions.
- [ ] API or architecture documentation is updated where necessary.
- [ ] Changes are reviewed and integrated.

Production-critical work also requires appropriate monitoring, logging and operational considerations.

---

# 9. Portfolio deliverables

Maintain these artefacts throughout development:

| Deliverable | Purpose |
|---|---|
| Product specification | Requirements and scope |
| Architecture diagram | System structure and data flow |
| ADRs | Significant technical decisions |
| ERD | Database relationships |
| OpenAPI specification | API contracts |
| RAG architecture | Retrieval and generation flow |
| Evaluation report | Retrieval and answer quality |
| Threat model | Security risks and mitigations |
| Test strategy | Quality assurance approach |
| Deployment documentation | Infrastructure and release process |
| Operational runbook | Troubleshooting and recovery |
| Demo recording | Demonstrable end-to-end product |

---

# 10. Engineering guidance for Codex

Use this document as the high-level source of truth for the project. It describes intended behaviour and architecture, not permission to implement every feature at once.

## Implementation rules

1. Read the relevant project documentation before making changes.
2. Work on one ticket or a small, explicitly agreed group of tickets at a time.
3. Check dependencies before starting a ticket.
4. Inspect the existing codebase before proposing structural changes.
5. Follow established architectural boundaries and conventions.
6. Prefer simple, maintainable implementations over premature abstraction.
7. Add or update tests alongside implementation.
8. Do not silently change architectural decisions or technology choices.
9. Record significant changes in ADRs.
10. Update documentation when implementation changes the intended design.

## AI-specific rules

- Never treat LLM output as inherently trustworthy.
- Enforce permissions in application code.
- Treat retrieved documents as untrusted input.
- Validate tool inputs and outputs.
- Track model usage and costs.
- Make AI behaviour measurable through evaluation tests.
- Preserve source references for generated answers.

## Project documentation locations

Repository-relative canonical paths:

- `PROJECT.md`: overview, technology and current status.
- `BACKLOG.md`: tickets, dependencies, acceptance criteria and status.
- `docs/PRODUCT_SPEC.md`: product requirements (this document).
- `docs/ARCHITECTURE.md`, `docs/DATA_MODEL.md`, `docs/API.md`, `docs/SECURITY.md`: detailed documents created when their tickets require them.
- `docs/ADRs/`: architectural decisions, established by 01-03.

Detailed design documents are planned and do not yet exist. Do not create empty placeholders.

**Important:** This specification is the target design. The implementation should evolve incrementally, with actual decisions and constraints documented as they emerge.