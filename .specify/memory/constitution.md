<!--
================================================================================
SYNC IMPACT REPORT
================================================================================
Version Change: Initial → 1.0.0 (MINOR - new constitution created)
Modified Principles: N/A (initial creation)
Added Sections:
  - Core Philosophy (SDD-RI)
  - Architectural Principles
  - Workflow Standards
  - Tech Stack Guidelines
  - Code Quality Gates
  - Definition of Done
Removed Sections: N/A
Templates Requiring Updates:
  ✅ plan-template.md - reviewed, compatible with Constitution Check section
  ✅ spec-template.md - reviewed, compatible with requirements-driven approach
  ✅ tasks-template.md - reviewed, compatible with TDD and checkpoint patterns
Follow-up TODOs: None
================================================================================
-->

# Hackathon II: Evolution of Todo — Project Constitution

**This constitution governs the 5-phase evolution from Console App to Cloud-Native Distributed System. It is designed to remain stable regardless of phase additions, modifications, or removals.**

---

## Core Philosophy (SDD-RI)

### I. Spec-First Development

**Principle**: No implementation without specification. Every feature follows the workflow: Constitution → Spec → Plan → Tasks → Implement.

**Rules**:
- MUST create specification document before any code
- MUST define acceptance criteria before implementation
- MUST document architectural decisions before coding
- Specifications MUST be version-controlled alongside code

**Rationale**: Specifications serve as contracts, ensure shared understanding, and enable AI-driven implementation. Without specs, implementations drift from intent and become unmaintainable.

---

### II. No Manual Code

**Principle**: Human as Architect; Agent as Implementer. All production code is AI-generated via Spec-Kit Plus.

**Rules**:
- Humans MUST NOT write production code manually
- Humans design; agents implement from specifications
- All code generation MUST be traceable to specifications
- Manual edits for debugging are permitted but MUST be re-specified afterward

**Rationale**: Consistency, scalability, and quality are maximized when implementation follows rigorous specification. Human expertise is better applied to architecture than typing.

---

### III. Reusable Intelligence

**Principle**: Prioritize capturing intelligence over code. Document architectural decisions (ADRs), preserve prompt histories (PHRs), and build reusable subagents.

**Rules**:
- MUST create ADR for every significant architectural decision
- MUST create PHR for every user interaction and implementation session
- MUST build subagents for repeated patterns (e.g., CRUD, auth, testing)
- Intelligence artifacts MUST be versioned and discoverable

**Rationale**: Code is disposable; intelligence is permanent. Capturing decisions, rationale, and patterns enables rapid evolution and onboarding.

---

## Architectural Principles

### IV. Evolutionary Architecture

**Principle**: Design for the future, implement for the present. Current phase code MUST use interfaces that enable seamless swapping in future phases.

**Rules**:
- MUST define interfaces/contracts for all cross-boundary communication
- Implementation details MUST be hidden behind abstractions
- MUST design for phase independence (each phase is self-contained)
- Future phases MUST extend, not rewrite, prior phases
- Phase transitions MUST preserve backward compatibility where feasible

**Rationale**: A 5-phase evolution requires architecture that adapts without wholesale rewrites. Interfaces decouple phases, allowing independent evolution.

**Phase-Agnostic Design**:
- Regardless of phase count, all boundaries (storage, auth, communication) use abstractions
- Adding Phase 6 or removing Phase 3 MUST NOT break existing contracts
- Each phase builds on stable interfaces from previous phases

---

### V. Single Responsibility Principle (SRP)

**Principle**: Each module, class, and function has one clear purpose. Business logic MUST be separated from I/O and UI.

**Rules**:
- One module = one concern (e.g., TodoService handles todo logic only)
- Business logic MUST NOT depend on I/O implementations (console, web, API)
- UI/presentation layers MUST NOT contain business logic
- Each function MUST do one thing well

**Rationale**: SRP enables reuse across phases (Phase I console → Phase II web reuses the same business logic) and testability.

---

### VI. User Experience First

**Principle**: All interfaces MUST be intuitive and helpful, with graceful error handling.

**Rules**:
- Error messages MUST be actionable (tell user what to do)
- MUST provide examples and help text for all commands/APIs
- MUST validate inputs early and provide clear feedback
- MUST handle edge cases gracefully (no crashes, no silent failures)
- User feedback MUST guide design decisions

**Rationale**: Technical excellence is meaningless without user satisfaction. Systems are built for humans, not machines.

---

## Workflow Standards

### VII. The Checkpoint Pattern

**Principle**: Implementation proceeds atomically: Generate → Review → Commit → Next Task.

**Rules**:
- Each task MUST be independently completable
- MUST commit after each task or logical unit
- MUST NOT merge multiple concerns in one commit
- MUST tag commits with task IDs for traceability
- MUST validate at checkpoints before proceeding

**Rationale**: Atomic commits enable rollback, debugging, and parallel work. Large changesets obscure intent and introduce bugs.

---

### VIII. Test-Driven Development (TDD)

**Principle**: Tests MUST be defined in Spec/Plan and implemented before or alongside features.

**Rules**:
- MUST write tests before implementation (Red-Green-Refactor)
- Tests MUST fail first, then implementation makes them pass
- MUST include unit, integration, and contract tests as specified
- Test coverage MUST align with acceptance criteria
- MUST NOT skip tests to "move faster"

**Rationale**: Tests are executable specifications. Writing tests first ensures clarity of intent and prevents over-engineering.

---

## Tech Stack Guidelines

### IX. Core Technologies

**Languages & Runtimes**:
- Python 3.13+ (uv for package management)
- TypeScript (strict mode required)

**Frameworks**:
- Backend: FastAPI, SQLModel
- Frontend: Next.js 15+, Tailwind CSS
- Authentication: Better Auth (JWT-based)
- AI/Agents: OpenAI Agents SDK
- MCP: Model Context Protocol for tooling

**Infrastructure**:
- Database: Neon PostgreSQL
- Containers: Docker
- Orchestration: Kubernetes
- Messaging: Kafka
- Distributed Runtime: Dapr

**Rationale**: This stack supports all 5 phases (console, web, API, distributed, cloud-native) with minimal rework. Each technology is production-grade and well-documented.

**Phase-Agnostic Stack**:
- Stack selections MUST support current and future phases
- Adding new phases (e.g., Phase 6: Mobile) MUST leverage existing stack where possible
- Technology changes MUST be justified via ADR and Constitution amendment

---

## Code Quality Gates

### X. Type Safety (NON-NEGOTIABLE)

**Principle**: All code MUST pass strict type checking.

**Rules**:
- Python: `mypy --strict` MUST pass with no errors
- TypeScript: `tsc --strict` MUST pass with no errors
- No `any` types or `type: ignore` without explicit justification in comments
- MUST use type annotations for all public interfaces

**Rationale**: Type safety catches bugs at compile time, improves IDE support, and serves as inline documentation.

---

### XI. Error Handling

**Principle**: No silent failures. All errors MUST be handled gracefully with user-friendly structured responses.

**Rules**:
- MUST NOT use bare `except:` or `catch (e) {}` without logging
- Errors MUST be logged with context (user, action, timestamp)
- User-facing errors MUST include actionable guidance
- MUST distinguish between recoverable and non-recoverable errors
- MUST define error taxonomies for each service

**Rationale**: Silent failures destroy trust. Structured error handling enables debugging and improves UX.

---

### XII. Configuration Management

**Principle**: Follow 12-Factor App methodology. All configuration MUST use environment variables; secrets MUST use `.env` files (not committed).

**Rules**:
- MUST NOT hardcode URLs, credentials, or feature flags
- MUST use `.env` for local development (with `.env.example` committed)
- Production MUST use secure secret management (e.g., Kubernetes secrets)
- Configuration MUST be validated at startup
- MUST document all required environment variables

**Rationale**: Configuration as code enables portability across environments (dev, staging, prod) and prevents accidental secret exposure.

---

## Definition of Done

Every deliverable (feature, phase, task) MUST meet these criteria before being considered complete:

### XIII. Done Checklist

1. **Constitutional Compliance**:
   - [ ] Adheres to all applicable principles in this constitution
   - [ ] Justified exceptions documented in ADR if applicable
   - [ ] No principle violations without explicit approval

2. **Spec Alignment**:
   - [ ] Implementation matches specification exactly
   - [ ] All acceptance criteria met and verified
   - [ ] Edge cases handled as specified

3. **Clean Build**:
   - [ ] Type checking passes (`mypy --strict`, `tsc --strict`)
   - [ ] All tests pass (unit, integration, contract as specified)
   - [ ] Linting passes with no errors
   - [ ] No warnings in build output

4. **Reproducibility**:
   - [ ] Fresh clone builds successfully
   - [ ] All dependencies documented in lock files
   - [ ] Environment setup documented in README or quickstart
   - [ ] No "works on my machine" scenarios

5. **Documentation**:
   - [ ] PHR created for implementation session
   - [ ] ADR created for significant decisions
   - [ ] Code comments explain "why", not "what"
   - [ ] Public APIs have docstrings/JSDoc

6. **Phase Independence** (for phase deliverables):
   - [ ] Phase can be demonstrated independently
   - [ ] Interfaces allow future phase integration
   - [ ] No hardcoded assumptions about next phases

**Rationale**: Done means truly done—shippable, maintainable, and documented. Partial completion accumulates technical debt.

---

## Governance

### Amendment Process

**Authority**: This constitution supersedes all other practices, patterns, and conventions.

**Amendments**:
- MUST be proposed via documented rationale (ADR or issue)
- MUST include impact analysis (which phases/features affected)
- MUST receive explicit approval before adoption
- MUST include migration plan if existing code affected
- MUST update constitution version following semantic versioning:
  - **MAJOR**: Backward-incompatible principle removals or redefinitions
  - **MINOR**: New principles, sections, or material expansions
  - **PATCH**: Clarifications, wording, typo fixes

**Compliance**:
- All PRs/commits MUST verify constitutional compliance
- Reviewers MUST check alignment with principles
- Complexity MUST be justified (see plan-template.md Complexity Tracking section)
- Violations MUST be rejected or documented as exceptions in ADR

**Phase Evolution**:
- Adding, removing, or modifying phases MUST NOT require constitutional amendments
- This constitution is phase-agnostic by design
- Phase-specific rules (if needed) MUST be documented in phase specs, not here

**Rationale**: Constitutions provide stability; amendments ensure evolution. Governance prevents drift and ensures discipline.

---

**Version**: 1.0.0 | **Ratified**: 2025-12-07 | **Last Amended**: 2025-12-07
