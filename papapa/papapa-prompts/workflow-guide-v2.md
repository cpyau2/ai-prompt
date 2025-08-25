# 5-Phase Development Workflow

## Overview

A structured approach to software development using LLMs across 5 distinct phases. Each phase builds on previous phases and requires including both the phase prompt AND generated documentation to maintain context.

## Commonly Used Prompts

- **"Need clarification?"** - Ask LLM to identify and request clarification on unclear aspects
- **"Update 01-requirements.md with new requirements found."** - Update requirements document with discoveries from design phase
- **"Update 02-design.md if design changes are needed."** - Update design document when implementation reveals design issues
- **"ALWAYS wait for approval between task executions."** - Remind LLM to pause for approval between Phase 4 tasks
- **"We're in iteration X, phase X."** - Indicate iteration cycles when returning to previous phases (iteration = scoped feature)
- **"Add numbers to subtasks."** - Request LLM to add numbering system to implementation plan subtasks
- **"Remember to mark tasks as complete during Phase 4 execution."** - Remind LLM to update implementation plan checkboxes

## Phase Structure

---

### Phase 1: Requirements Gathering

- **Include:** `@base-prompt.md` + `@p01-requirements-gathering.md`
- **Purpose:** Define what the feature should do
- **Output:** `specs/{feature_name}/01-requirements.md`

---

### Phase 2: Design Creation

- **Include:** `@base-prompt.md` + `@p02-design-creation.md` + `@specs/{feature_name}/01-requirements.md`
- **Purpose:** Design how the feature will be built
- **Output:** `specs/{feature_name}/02-design.md`
- **Note:** Ask LLM for code snippets if you need confidence in the design approach

---

### Phase 3: Implementation Planning

- **Include:** `@base-prompt.md` + `@p03-implementation-planning.md` + `@specs/{feature_name}/01-requirements.md` + `@specs/{feature_name}/02-design.md`
- **Purpose:** Break down work into manageable coding tasks
- **Output:** `specs/{feature_name}/03-implementation-plan.md`

---

### Phase 4: Implementation Execution

- **Include:** `@base-prompt.md` + `@p04-implementation-execution.md` + `@specs/{feature_name}/01-requirements.md` + `@specs/{feature_name}/02-design.md` + `@specs/{feature_name}/03-implementation-plan.md`
- **Purpose:** Execute planned tasks one by one
- **Output:** `specs/{feature_name}/04-changes-log.md` (only if adhoc changes occur)

---

### Phase 5: Documentation Update

- **Include:** `@base-prompt.md` + `@p05-documentation-update.md` + `@specs/{feature_name}/01-requirements.md` + `@specs/{feature_name}/02-design.md` + `@specs/{feature_name}/03-implementation-plan.md` + `@specs/{feature_name}/04-changes-log.md` (if exists)
- **Purpose:** Update all documentation to reflect actual implementation
- **Output:** Updated main documentation files
- **Note:** Optional in practice - many projects stop at Phase 4

## Key Principles

### Document Accumulation
- Each phase includes ALL previous generated documents
- Include both phase prompts AND generated docs
- This prevents LLM context loss and hallucination

### Phase Progression
- Wait for explicit approval before moving to next phase
- Can return to previous phases if major changes needed
- Each phase builds on accumulated context
- Use "We're in iteration X, phase X" to indicate iteration cycles
- Each iteration = scoped feature that goes through phases 1-5

### Implementation Control
- Execute one task at a time during Phase 4
- Stop after each task for user review (bullet point numbers are pause points)
- Document all changes in `04-changes-log.md`
- Update requirements/design docs in Phase 5, not during implementation
- Immediately stop and suggest resolution if design flaws discovered
- Fix all errors (especially TypeScript) before proceeding to next subtask

## File Structure

```
specs/{feature_name}/
├── 01-requirements.md
├── 02-design.md
├── 03-implementation-plan.md
├── 04-changes-log.md (optional, only if adhoc changes occur)
└── Updated main docs (Phase 5 output)
```

### File Management Guidelines
- **Use kebab-case for feature names** (e.g., `excel-processor`, `user-authentication`)
- **Keep:** `01-requirements.md` and `02-design.md` (permanent documentation)
- **Scrap:** `03-implementation-plan.md`, `04-changes-log.md` (temporary working files)
- **Test Cases:** Generate test documentation in Phase 2 (markdown), add JS comments during Phase 4 implementation
- **Excel Fixtures:** LLM can only describe content - you must manually create Excel files and document the process
- **Note:** Test documentation workflow is "to be confirmed" - not intensively verified
- **Note:** Numbered tasks/subtasks require explicit approval - numbers = pause points

## Task Execution Examples

### Unnumbered Subtasks (Execute as 1 Unit)
```
- [ ] **11.2** Test mutation hooks
  - Test user creation with useCreateUser hook
  - Verify user updates with useUpdateUser hook
  - Test user deletion with useDeleteUser hook
  - Check cache invalidation strategies
```

### Numbered Subtasks (Execute as 4 Units with Approval Between Each)
```
- [ ] **11.2** Test mutation hooks
  - [ ] 11.2.1 Test user creation with useCreateUser hook
  - [ ] 11.2.2 Verify user updates with useUpdateUser hook
  - [ ] 11.2.3 Test user deletion with useDeleteUser hook
  - [ ] 11.2.4 Check cache invalidation strategies
```

## Why Include Generated Docs?

**Critical for workflow success:** Including generated documentation prevents the LLM from:
- Losing context between phases
- Starting fresh and hallucinating solutions
- Forgetting previous decisions and requirements
- Repeating work already completed

**Always include:** Phase prompt + All generated docs from previous phases
