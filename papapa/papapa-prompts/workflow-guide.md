# How to Use the 5-Phase Development Workflow

## Overview

This workflow provides a structured approach to software development using LLMs across 5 distinct phases. Each phase has its own focused prompt that builds upon previous phases.

## Workflow Structure

### Phase 1: Requirements Gathering

**Include:** `@base-prompt.md` + `@01-requirements-phase.md`

**Purpose:** Define what the feature should do

- LLM generates initial requirements based on your idea
- Iterate with user feedback until requirements are complete
- Creates `specs/{feature_name}/01-requirements.md`

**Example:**

```
User: "I want to build an Excel processor that converts xlsx to JSON"
→ LLM generates requirements, iterates until approval
```

### Phase 2: Design Document Creation

**Include:** `@base-prompt.md` + `@02-design-phase.md`

**Purpose:** Design how the feature will be built

- Based on approved requirements
- Conducts research and creates comprehensive design
- Creates `specs/{feature_name}/02-design.md`
- Includes architecture, components, data models, testing strategy
- For GUI features: adds UI/UX design, responsive design, accessibility

**Example:**

```
User: "Requirements are approved, let's design it"
→ LLM creates design document, iterates until approval
```

### Phase 3: Implementation Plan Creation

**Include:** `@base-prompt.md` + `@03-implementation-plan-phase.md`

**Purpose:** Break down work into manageable coding tasks

- Based on approved design
- Creates numbered checkbox list of implementation tasks
- Focuses only on code writing, modifying, and testing tasks
- Creates `specs/{feature_name}/03-implementation-plan.md`

**Example:**

```
User: "Design is approved, create implementation plan"
→ LLM creates task list, iterates until approval
```

### Phase 4: Implementation Plan Execution

**Include:** `@base-prompt.md` + `@04-implementation-plan-execution.md`

**Purpose:** Execute the planned tasks and generate code

- Based on approved implementation plan
- Executes tasks one at a time with user review
- Updates `03-implementation-plan.md` with progress
- Creates `specs/{feature_name}/04-changes-log.md` for tracking changes
- Distinguishes between information requests and execution requests

**Example:**

```
User: "Plan is approved, let's start implementing"
→ LLM executes tasks one by one, updates progress
```

### Phase 5: Documentation Update

**Include:** `@base-prompt.md` + `@05-documentation-update.md`

**Purpose:** Update all documentation to reflect actual implementation

- Reviews all changes made during Phase 4
- Merges changes from `04-changes-log.md` back into main docs
- Updates `01-requirements.md`, `02-design.md`, `03-implementation-plan.md`
- Ensures all documentation reflects current implementation

**Example:**

```
User: "Let's update the documentation with all our changes"
→ LLM updates all docs to match actual implementation
```

## Key Workflow Principles

### 1. Phase Progression

- Each phase builds on the previous
- Wait for explicit approval before moving to next phase
- Can return to previous phases if major changes are needed

### 2. Iterative Development

- Complete all 5 phases for initial feature
- Start new iteration by returning to Phase 1 with enhancements
- Each iteration builds on previous work

### 3. Change Management

- Quick fixes during Phase 4: stay in Phase 4
- Major changes: return to appropriate previous phase
- Document all changes in `04-changes-log.md` during Phase 4
- Merge changes back to main docs in Phase 5

### 4. User Control

- LLM executes one task at a time
- Stops after each task for user review
- Distinguishes between information requests and execution requests
- Waits for explicit approval at each phase

## Manual Change Reporting Discipline

### Why Report Manual Changes

**Critical for workflow success:** You must report all manual code changes to the LLM during Phase 4.

### What to Report

**Code Changes:**

```
"I manually refactored the user authentication logic"
"I added error handling to the file upload function"
"I optimized the database query for better performance"
```

**Architecture Changes:**

```
"I changed the folder structure to separate concerns"
"I moved the API endpoints to a different module"
"I restructured the component hierarchy"
```

**Dependencies/Config:**

```
"I added a new npm package for date formatting"
"I updated the database configuration"
"I changed the build process"
```

### How to Report

**Every time you make a significant change:**

1. **Tell the LLM** what you changed
2. **Explain why** you made the change
3. **Let the LLM document** it in `04-changes-log.md`

### Benefits of Reporting

- **Context Preservation:** LLM maintains understanding of actual code
- **Documentation Accuracy:** Phase 5 can update docs correctly
- **Future Iterations:** Next iterations have accurate context
- **Complete Audit Trail:** Full history of what changed and why

## Real-World Examples

### Excel Processor Example

**Phase 1:** Requirements for xlsx → JSON conversion
**Phase 2:** Design with test strategy (manual xlsx fixtures needed)
**Phase 3:** Implementation plan with specific task for user to create test files
**Phase 4:** Execute tasks, pause for user to create xlsx files, continue
**Phase 5:** Update docs with actual implementation details

### Handling Manual Dependencies

- Acknowledge LLM limitations upfront (e.g., can't generate xlsx files)
- Plan for user involvement in implementation plan
- Create clear handoff points where user action is needed
- Resume execution after user provides required input

### Bug Fixes and Refactoring

- Document changes immediately in `04-changes-log.md`
- Categorize changes: requirements, design, implementation, insights
- Include context about why changes were made
- Merge all changes back to main docs in Phase 5

## Best Practices

1. **Start Simple:** Begin with core functionality, add complexity iteratively
2. **Document Changes:** Track all modifications during development
3. **User Review:** Always wait for approval before proceeding
4. **Clear Scope:** Each phase has focused responsibilities
5. **Flexible Transitions:** Can move between phases as needed
6. **Complete Documentation:** Keep all docs current and accurate
7. **Report Manual Changes:** Always tell LLM about your code modifications

## File Structure

```
specs/{feature_name}/
├── 01-requirements.md
├── 02-design.md
├── 03-implementation-plan.md
├── 04-changes-log.md (created during Phase 4)
└── 05-documentation-update.md (Phase 5 output)
```

This workflow provides a structured, iterative approach to software development that maintains quality, user control, and comprehensive documentation throughout the process.
