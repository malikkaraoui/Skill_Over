# The BMAD Method: complete guide to AI-driven agile development

**BMAD (Breakthrough Method of Agile AI-Driven Development) is a structured, open-source framework that orchestrates specialized AI agent personas through the full software development lifecycle — from initial idea to production code.** It works by defining distinct AI "roles" (Analyst, Architect, PM, Developer, Scrum Master) each with dedicated prompts, tasks, templates, and checklists, coordinated by an Orchestrator meta-agent. The method produces a chain of professional planning documents — project brief → PRD → architecture → epics → stories — that give AI coding agents like Claude Code the rich, structured context they need to write high-quality code consistently. Designed for VS Code, Cursor, and chat-based AI tools, BMAD bridges the gap between "vibe coding" and disciplined software engineering by ensuring AI agents always have clear requirements, architecture boundaries, and acceptance criteria before writing a single line of code.

> **Note:** This report is compiled from extensive training knowledge of the BMAD-METHOD repository (github.com/bmad-code-org/BMAD-METHOD) through early 2025. The repository is actively maintained and may have evolved since. Verify details against the current repo before building production workflows.

---

## How BMAD structures AI-assisted development

BMAD operates on a core insight: **AI coding agents produce dramatically better output when given structured, interconnected planning documents rather than ad-hoc prompts.** The method enforces a phased document-driven workflow where each phase produces artifacts that feed the next, and validation checklists serve as quality gates between phases.

The framework ships in two modes. **IDE mode** is designed for VS Code, Cursor, Windsurf, and similar AI-integrated editors — it stores persona definitions, task files, templates, and checklists inside a `.bmad/` directory within your project repository. **Chat mode** provides combined persona files optimized for conversational AI tools like Claude.ai or ChatGPT, where you paste the full persona prompt to configure each role. For Claude Code specifically, a `CLAUDE.md` file at the project root tells Claude about BMAD conventions, pointing it toward the method assets and establishing behavioral expectations.

The development lifecycle follows a strict sequence with **five main phases**: Discovery (project brief creation), Requirements (PRD generation), Architecture (system design), Planning (epic and story breakdown), and Implementation (code writing against stories). Each phase has a designated persona, a task definition that guides the AI through the work, a template that structures the output, and a checklist that validates the result before progressing.

---

## The seven agent personas and the Orchestrator

BMAD defines specialized AI personas, each with a system prompt that establishes the agent's expertise, perspective, communication style, and constraints. These are not separate software programs — they are carefully crafted instruction sets that configure a single AI model to behave as a domain expert.

**The BMAD Orchestrator** is the entry point and meta-agent. It does not produce documents itself. Instead, it understands the full BMAD workflow, knows what phase the project is in, recommends which persona to engage next, and helps users navigate the method. In IDE mode, you typically start by asking the Orchestrator what to do next.

**The Analyst (Business Analyst)** handles the discovery phase. This persona excels at asking probing questions about the project vision, identifying stakeholders, clarifying scope, and producing the initial **project brief** — a concise document that captures the why, what, and high-level how of the project.

**The Product Manager (PM)** takes the project brief and transforms it into a rigorous **Product Requirements Document (PRD)**. The PM persona focuses on user personas, functional requirements, non-functional requirements, success metrics, and scope boundaries. This is one of the most critical phases because the PRD becomes the source of truth for all downstream work.

**The Architect** consumes the PRD and produces the **architecture document** and **tech stack specification**. This persona thinks in terms of system components, data models, API contracts, infrastructure, security, scalability, and deployment. The architecture document establishes technical constraints that all implementation must respect.

**The Design Architect** handles UI/UX concerns when the project has a frontend. This persona produces design system specifications, component hierarchies, user flow diagrams, and visual design guidelines.

**The Product Owner / Scrum Master (PO/SM)** breaks the PRD and architecture into **epics** and **stories**. This persona ensures each story is independently implementable, has clear acceptance criteria, and traces back to specific requirements. The story breakdown is what the Developer persona actually consumes during implementation.

**The Developer (Dev)** is the implementation persona. It works on one story at a time, reads the story's acceptance criteria and technical notes, references the architecture document for design constraints, and writes code that satisfies the story's definition of done.

---

## Complete repository and project folder structure

The BMAD-METHOD repository itself is organized to provide all the assets needed to bootstrap the method into any project. Here is the representative structure:

```
BMAD-METHOD/
├── README.md                          # Full methodology overview and setup guide
├── CLAUDE.md                          # Claude Code integration instructions
├── LICENSE
│
├── ide/                               # IDE mode assets (VS Code, Cursor, etc.)
│   ├── .bmad/                         # Drop this folder into your project root
│   │   ├── personas/                  # AI agent persona definitions
│   │   │   ├── orchestrator.md
│   │   │   ├── analyst.md
│   │   │   ├── pm.md
│   │   │   ├── architect.md
│   │   │   ├── design-architect.md
│   │   │   ├── dev.md
│   │   │   └── sm.md
│   │   │
│   │   ├── tasks/                     # Task definitions for each workflow step
│   │   │   ├── create-project-brief.md
│   │   │   ├── create-prd.md
│   │   │   ├── create-architecture.md
│   │   │   ├── create-front-end-architecture.md
│   │   │   ├── create-epic.md
│   │   │   ├── create-next-story.md
│   │   │   ├── create-doc.md
│   │   │   └── correct-course.md
│   │   │
│   │   ├── templates/                 # Document templates
│   │   │   ├── project-brief-template.md
│   │   │   ├── prd-template.md
│   │   │   ├── architecture-template.md
│   │   │   ├── front-end-architecture-template.md
│   │   │   ├── epic-template.md
│   │   │   ├── story-template.md
│   │   │   └── tech-stack-template.md
│   │   │
│   │   └── checklists/               # Validation checklists (quality gates)
│   │       ├── prd-checklist.md
│   │       ├── architecture-checklist.md
│   │       ├── story-draft-checklist.md
│   │       └── change-checklist.md
│   │
│   └── setup/                         # Setup scripts/guides for IDE integration
│
├── chat/                              # Chat mode assets (Claude.ai, ChatGPT)
│   └── personas/                      # Combined single-file personas for chat
│       ├── bmad-orchestrator.md
│       ├── bmad-analyst.md
│       ├── bmad-pm.md
│       ├── bmad-architect.md
│       └── bmad-dev.md
│
└── docs/                              # Additional documentation
    ├── getting-started.md
    └── workflow-guide.md
```

**When you set up a project using BMAD**, your project repo gets the `.bmad/` directory and a structured output directory. The target project structure looks like:

```
your-project/
├── .bmad/                             # BMAD method assets (copied from repo)
│   ├── personas/
│   ├── tasks/
│   ├── templates/
│   └── checklists/
│
├── bmad-output/                       # All generated planning documents
│   ├── project-brief.md              # Phase 1 output
│   ├── prd.md                        # Phase 2 output
│   ├── architecture.md               # Phase 3 output
│   ├── front-end-architecture.md     # Phase 3 output (if applicable)
│   ├── tech-stack.md                 # Phase 3 output
│   ├── epics/                        # Phase 4 output
│   │   ├── epic-1.md
│   │   ├── epic-2.md
│   │   └── epic-3.md
│   └── stories/                      # Phase 4-5 output
│       ├── epic-1/
│       │   ├── story-1.1.md
│       │   ├── story-1.2.md
│       │   └── story-1.3.md
│       └── epic-2/
│           ├── story-2.1.md
│           └── story-2.2.md
│
├── CLAUDE.md                          # Claude Code project instructions
├── package.json                       # Your actual project files
├── tsconfig.json
├── src/
└── ...
```

The `bmad-output/` directory (sometimes `_bmad-output/` or `docs/planning/`) is the canonical location for all generated planning artifacts. Stories are organized by epic in subdirectories.

---

## Document templates in full detail

### The PRD template

The PRD is BMAD's most critical planning document. It serves as the single source of truth for what the product does and why. The template structure:

```markdown
# Product Requirements Document (PRD)

## 1. Title and Overview
### 1.1 Product Name
### 1.2 Document Version & Status
### 1.3 Executive Summary
[2-3 paragraph overview of what this product is, who it serves, and why it matters]

## 2. Problem Statement
### 2.1 Current State
[Description of the current situation and its pain points]
### 2.2 Pain Points
[Specific problems users face today]
### 2.3 Desired Outcome
[What success looks like]

## 3. Goals and Objectives
### 3.1 Business Goals
[What the business achieves — revenue, efficiency, market position]
### 3.2 User Goals
[What users can accomplish that they couldn't before]
### 3.3 Non-Goals / Out of Scope
[Explicitly what this product will NOT do in this version]

## 4. Target Users
### 4.1 Primary User Persona(s)
[Name, role, demographics, goals, frustrations, technical proficiency]
### 4.2 Secondary User Persona(s)
### 4.3 User Journey Map
[High-level journey from discovery to regular usage]

## 5. Functional Requirements
### 5.1 Core Features
[Feature Name] — [Description] — [Priority: Must/Should/Could]
### 5.2 Feature Details
[For each core feature: detailed description, user stories, business rules]
### 5.3 User Interaction Flows
[Step-by-step flows for key interactions]

## 6. Non-Functional Requirements
### 6.1 Performance
[Response times, throughput, concurrent users]
### 6.2 Security
[Authentication, authorization, data protection requirements]
### 6.3 Scalability
[Growth expectations, scaling requirements]
### 6.4 Reliability & Availability
[Uptime targets, disaster recovery, data backup]
### 6.5 Accessibility
[WCAG level, i18n/l10n requirements]

## 7. Technical Constraints
[Platform constraints, integration requirements, technology mandates]

## 8. Assumptions and Dependencies
### 8.1 Assumptions
### 8.2 Dependencies
[External services, APIs, third-party tools]

## 9. Success Metrics / KPIs
[Measurable criteria to determine if the product is successful]

## 10. Risks and Mitigations
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|

## 11. Timeline and Milestones
[High-level phases and target dates]

## 12. Appendices
[Glossary, references, related documents]
```

### The architecture template

The architecture document translates PRD requirements into technical design:

```markdown
# Architecture Document

## 1. System Overview
### 1.1 Purpose
[What this system does from a technical perspective]
### 1.2 Architecture Style
[Monolith, microservices, serverless, event-driven, etc.]
### 1.3 High-Level Architecture Diagram
[ASCII diagram or description of the major system components and their relationships]

## 2. Technology Stack
### 2.1 Core Technologies
| Layer | Technology | Version | Rationale |
|-------|-----------|---------|-----------|
| Language | | | |
| Runtime | | | |
| Framework | | | |
| Database | | | |
| Cache | | | |
| Message Queue | | | |

### 2.2 Development Tools
[Build tools, linting, testing frameworks, CI/CD]
### 2.3 Infrastructure
[Cloud provider, containerization, orchestration]

## 3. Component Architecture
### 3.1 Component Diagram
### 3.2 Component Descriptions
[For each major component: purpose, responsibilities, interfaces, dependencies]
### 3.3 Component Interaction Patterns
[How components communicate: REST, gRPC, events, etc.]

## 4. Data Architecture
### 4.1 Data Models
[Entity descriptions with key fields, relationships, constraints]
### 4.2 Database Schema
[Table/collection definitions]
### 4.3 Data Flow Diagrams
### 4.4 Data Migration Strategy

## 5. API Design
### 5.1 API Style
[REST, GraphQL, gRPC, WebSocket]
### 5.2 Endpoint Definitions
[Key endpoints with methods, paths, request/response shapes]
### 5.3 Authentication & Authorization
[Auth mechanism, token management, role-based access]
### 5.4 Error Handling
[Standard error response format, error codes]

## 6. Infrastructure & Deployment
### 6.1 Deployment Architecture
### 6.2 Environment Strategy
[Development, staging, production]
### 6.3 CI/CD Pipeline
### 6.4 Containerization
### 6.5 Monitoring & Observability
[Logging, metrics, tracing, alerting]

## 7. Security Architecture
### 7.1 Authentication
### 7.2 Authorization
### 7.3 Data Encryption
[At rest, in transit]
### 7.4 Security Headers & Best Practices
### 7.5 Vulnerability Management

## 8. Performance & Scalability
### 8.1 Performance Targets
### 8.2 Scaling Strategy
[Horizontal/vertical, auto-scaling rules]
### 8.3 Caching Strategy
### 8.4 Load Balancing

## 9. Development Guidelines
### 9.1 Coding Standards
### 9.2 Project Structure
[Source code folder layout]
### 9.3 Testing Strategy
[Unit, integration, e2e — coverage targets]
### 9.4 Error Handling Patterns
### 9.5 Logging Standards

## 10. Cross-Cutting Concerns
### 10.1 Configuration Management
### 10.2 Feature Flags
### 10.3 Internationalization
### 10.4 Versioning Strategy

## 11. Risks and Technical Debt
[Known risks, accepted trade-offs, planned debt]

## 12. Decision Log
| Decision | Alternatives Considered | Rationale | Date |
|----------|------------------------|-----------|------|
```

### The epic template

```markdown
# Epic: [Epic Title]

## Epic ID
[EPIC-001]

## Description
[Comprehensive description of what this epic achieves]

## Business Value
[Why this epic matters — what user/business problem it solves]

## Goals
- [Goal 1]
- [Goal 2]

## User Stories
| Story ID | Title | Priority | Status |
|----------|-------|----------|--------|
| STORY-1.1 | | Must | Draft |
| STORY-1.2 | | Must | Draft |
| STORY-1.3 | | Should | Draft |

## Acceptance Criteria
- [ ] [Criterion 1 — measurable, testable]
- [ ] [Criterion 2]

## Dependencies
- [Other epics, external services, or decisions this depends on]

## Risks
- [Risk and mitigation]

## Notes
[Technical notes, design considerations, open questions]
```

### The story template

The story template is the most implementation-critical artifact, as Developer agents consume these directly:

```markdown
# Story: [Story Title]

## Story ID
[STORY-X.Y]

## Epic
[Reference to parent epic — EPIC-XXX: Epic Title]

## Status
[Draft | Ready | In Progress | Done]

## Priority
[Must | Should | Could | Won't]

## Story Description
As a [type of user],
I want [goal/desire],
So that [benefit/value].

## Acceptance Criteria

### AC1: [Criterion Name]
**Given** [precondition]
**When** [action]
**Then** [expected result]

### AC2: [Criterion Name]
**Given** [precondition]
**When** [action]
**Then** [expected result]

### AC3: [Criterion Name]
**Given** [precondition]
**When** [action]
**Then** [expected result]

## Technical Implementation Notes
[Specific guidance for the developer: which files to modify, patterns to follow,
architectural constraints to respect, API contracts to implement]

### Affected Components
- [Component 1]
- [Component 2]

### Data Model Changes
[Any schema changes needed]

### API Changes
[Any new/modified endpoints]

## Tasks / Subtasks
- [ ] [Implementation subtask 1]
- [ ] [Implementation subtask 2]
- [ ] [Write unit tests]
- [ ] [Write integration tests]
- [ ] [Update documentation]

## Dependencies
- [Other stories, services, or infrastructure this depends on]

## Testing Requirements
### Unit Tests
[What specifically to test at the unit level]
### Integration Tests
[What to test at the integration level]
### Manual Testing
[Any manual verification steps]

## Definition of Done
- [ ] All acceptance criteria met
- [ ] Tests written and passing
- [ ] Code reviewed (or self-reviewed against standards)
- [ ] No linting errors
- [ ] Documentation updated
- [ ] Deployed to staging/preview
```

### The project brief template

```markdown
# Project Brief: [Project Name]

## Vision Statement
[One sentence describing the ultimate vision]

## Problem
[What problem does this solve? For whom?]

## Proposed Solution
[High-level description of the solution approach]

## Target Users
[Who are the primary users?]

## Key Features (High-Level)
- [Feature 1]
- [Feature 2]
- [Feature 3]

## Success Criteria
[How will you know this project succeeded?]

## Technical Considerations
[Any known technical constraints, preferences, or requirements]

## Scope
### In Scope
### Out of Scope

## Timeline
[Expected timeline or urgency level]
```

---

## The five-phase workflow from idea to code

**Phase 1 — Discovery (Analyst persona).** You begin by engaging the Analyst/BA persona with your project idea. The Analyst asks structured questions about your vision, target users, core problems, and constraints. The output is a **project brief** — a concise, 1-2 page document capturing the project's essence. This phase typically takes one focused AI session. The Analyst validates the brief against a completeness checklist before declaring it ready.

**Phase 2 — Requirements (PM persona).** The PM persona consumes the project brief and produces the full **PRD**. This is the most document-intensive phase. The PM methodically works through functional requirements, non-functional requirements, user personas, and scope boundaries. The PRD is validated against the **PRD checklist**, which verifies that all sections are complete, requirements are testable, and scope is clearly bounded. **The PRD checklist serves as the quality gate** — work does not proceed to architecture until the PRD passes.

**Phase 3 — Architecture (Architect persona).** The Architect reads both the project brief and PRD, then produces the **architecture document** and **tech stack specification**. The architect makes critical technology decisions, defines component boundaries, specifies data models, and establishes API contracts. The **architecture checklist** validates that the design addresses all PRD requirements, identifies deployment strategy, specifies security approach, and includes a testing strategy. This is the hardest gate — a weak architecture undermines all downstream work.

**Phase 4 — Planning (SM/PO persona).** The Scrum Master persona breaks the PRD into **epics**, then decomposes each epic into **stories**. Stories must be independently implementable, small enough to complete in a single development session, and equipped with clear Given/When/Then acceptance criteria. The **story draft checklist** validates that each story has complete acceptance criteria, technical notes referencing architecture decisions, defined dependencies, and a testable definition of done.

**Phase 5 — Implementation (Dev persona).** The Developer persona picks up stories one at a time, reads the story along with the architecture document for context, and implements the code. **BMAD strongly recommends single-story implementation** — the Dev should complete one story fully (including tests) before moving to the next. This prevents the AI from losing context across multiple partially-implemented features.

---

## How BMAD works with Claude Code in VS Code

Claude Code integration is **the primary design target** for BMAD's IDE mode. The integration works through three mechanisms.

**The CLAUDE.md file** sits at the project root and serves as persistent instructions that Claude Code reads automatically whenever it starts a session in your project. A BMAD-compatible CLAUDE.md typically contains:

```markdown
# CLAUDE.md

## Project Overview
[Brief description of the project]

## BMAD Method
This project follows the BMAD (Breakthrough Method of Agile AI-Driven Development) methodology.
All planning documents are in `bmad-output/`. Method assets are in `.bmad/`.

## Key Documents
- Project Brief: bmad-output/project-brief.md
- PRD: bmad-output/prd.md
- Architecture: bmad-output/architecture.md
- Current Stories: bmad-output/stories/

## Development Rules
- Always read the relevant story file before implementing
- Follow the architecture document for all technical decisions
- Reference the tech stack — do not introduce unauthorized dependencies
- Implement one story at a time
- Run tests after each implementation
- Follow the coding standards defined in the architecture doc

## Tech Stack
[Key technology choices so Claude knows immediately]

## Project Structure
[Source code layout explanation]
```

**Persona invocation** works by referencing the persona files stored in `.bmad/personas/`. When you want to switch modes in Claude Code, you can tell Claude to read a persona file: "Read `.bmad/personas/architect.md` and adopt that role." Alternatively, you can paste persona content directly. The Orchestrator persona is particularly useful for starting sessions — it helps you determine which persona and task to engage based on current project state.

**Task execution** follows a pattern: you tell Claude which persona to adopt, point it to the relevant task file in `.bmad/tasks/`, and it follows the task's step-by-step instructions. For example: "Acting as the PM persona (`.bmad/personas/pm.md`), execute the create-prd task (`.bmad/tasks/create-prd.md`) using the project brief at `bmad-output/project-brief.md`."

---

## Checklists as quality gates

BMAD's checklist system is what transforms the workflow from a loose guideline into a disciplined process. Each checklist is a markdown file containing validation criteria that must be satisfied before proceeding to the next phase.

The **PRD checklist** verifies: all sections are populated, requirements are specific and testable (not vague), user personas are realistic and detailed, non-functional requirements include measurable targets, scope boundaries are explicitly stated, success metrics are quantifiable, and risks have mitigation strategies.

The **Architecture checklist** verifies: every functional requirement from the PRD maps to at least one component, the tech stack rationale is justified against requirements, data models cover all entities implied by the PRD, API design supports all user-facing features, security requirements are addressed, deployment strategy is defined, and testing strategy covers unit/integration/e2e levels.

The **Story draft checklist** verifies: each story follows the "As a / I want / So that" format, acceptance criteria use Given/When/Then structure, stories are independently implementable, technical implementation notes reference architecture decisions, dependencies are explicitly listed, and the definition of done is testable.

The **change checklist** handles mid-project requirement changes. When requirements shift, this checklist ensures all impacted documents are updated in cascade — PRD changes propagate to architecture, which propagate to affected stories.

---

## Putting it together for your OpenClaw project

For your TypeScript/Node.js OpenClaw skills suite (local-llm, task-auction, guardian, tom-transport), here is how you would bootstrap BMAD:

**Step 1**: Clone or copy the `.bmad/` directory from the BMAD-METHOD repo into your project root. Set up your `CLAUDE.md` referencing your tech stack (TypeScript, Node.js), the four skill modules, and the BMAD output directory.

**Step 2**: Start with the Analyst persona. Describe your OpenClaw vision — what each skill does, how they compose, who uses them, and what problem they solve. Produce a project brief at `bmad-output/project-brief.md`.

**Step 3**: Switch to the PM persona and execute the create-prd task. The PRD should define each skill (local-llm, task-auction, guardian, tom-transport) as a major feature area with specific functional requirements. Run the PRD checklist.

**Step 4**: Engage the Architect persona. The architecture document should define the monorepo or multi-package structure, shared interfaces between skills, the Node.js runtime configuration, TypeScript configuration, testing framework (likely Vitest or Jest), and how skills communicate. Run the architecture checklist.

**Step 5**: The SM persona creates epics — likely one per skill module, plus cross-cutting epics for shared infrastructure, CI/CD, and testing. Each epic breaks into **3-8 stories** that represent independently implementable chunks.

**Step 6**: Implement stories with the Dev persona in Claude Code, one at a time, referencing the architecture document constantly to maintain consistency across the four skill modules.

Your target folder structure would be:

```
openclaw-skills/
├── .bmad/
│   ├── personas/
│   ├── tasks/
│   ├── templates/
│   └── checklists/
├── bmad-output/
│   ├── project-brief.md
│   ├── prd.md
│   ├── architecture.md
│   ├── tech-stack.md
│   ├── epics/
│   │   ├── epic-1-local-llm.md
│   │   ├── epic-2-task-auction.md
│   │   ├── epic-3-guardian.md
│   │   ├── epic-4-tom-transport.md
│   │   └── epic-5-shared-infra.md
│   └── stories/
│       ├── epic-1/
│       ├── epic-2/
│       ├── epic-3/
│       ├── epic-4/
│       └── epic-5/
├── CLAUDE.md
├── package.json
├── tsconfig.json
├── packages/
│   ├── local-llm/
│   ├── task-auction/
│   ├── guardian/
│   └── tom-transport/
└── shared/
```

## Conclusion

BMAD's power lies not in any single template but in the **enforced sequence and validation chain** connecting discovery through implementation. The method ensures AI agents never operate in a context vacuum — every Developer session has a story with acceptance criteria tracing back through architecture to requirements to business goals. The most critical elements for your OpenClaw project are: getting the PRD right (it drives everything downstream), building an architecture document that clearly defines inter-skill interfaces, and writing stories small enough that Claude Code can complete each one in a single session without losing coherence. Start with the Orchestrator, follow the phase gates religiously, and validate each document against its checklist before progressing. The `CLAUDE.md` file is your persistent link between the method and your AI coding agent — invest time making it specific and actionable, and Claude Code will consistently produce code that aligns with your planning artifacts.