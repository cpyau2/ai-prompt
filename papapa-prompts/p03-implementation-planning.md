# Phase 3: Create Implementation Plan

After the user approves the Design, you should create a detailed implementation plan based on the design document, breaking down the work into manageable tasks and providing clear implementation guidance.
The implementation plan should be based on the design document, so ensure it exists first.

- Create 'specs/{feature_name}/03-implementation-plan.md' file if it doesn't exist
- Return to design phase if user indicates design changes are needed
- Return to requirements phase if user indicates additional requirements are needed
- Convert design into test-driven implementation prompts for code generation
- Prioritize incremental progress with no big complexity jumps
- Ensure each step builds on previous steps with no orphaned code
- Focus only on code writing, modifying, and testing tasks
- Format implementation plan as numbered checkbox list with maximum two levels
- Use top-level items (epics) only when needed
- Number sub-tasks with decimal notation (e.g., 1.1, 1.2, 2.1)
- Make each item a checkbox for progress tracking
- Prefer simple structure over complex hierarchies
- Ensure each task includes clear objective involving code writing, modifying, or testing
- Add additional information as sub-bullets under each task
- Reference specific requirements from requirements document (granular sub-requirements)
- Ensure implementation plan consists of discrete, manageable coding steps
- Avoid excessive implementation details already covered in design document
- Assume all context documents (requirements, design) will be available during implementation
- Prioritize test-driven development where appropriate
- Ensure the plan covers all aspects of the design that can be implemented through code
- Sequence steps to validate core functionality early through code
- Ensure all requirements are covered by the implementation tasks
- Offer to return to previous phases (requirements or design) if gaps are identified during implementation planning
- Include only tasks that can be performed by a coding agent (writing code, creating tests, etc.)
- Exclude non-coding activities (user testing, deployment, performance metrics, etc.)
- Ensure each task is actionable by a coding agent with specific file/component targets
- Make tasks concrete enough for execution without additional clarification
- Focus on implementation details rather than high-level concepts
- Scope tasks to specific coding activities (e.g., "Implement X function" not "Support X feature")
- Explicitly exclude non-coding tasks: user testing, deployment, performance analysis, end-to-end testing, user training, business changes, marketing activities
- Include only tasks that can be completed through writing, modifying, or testing code
- Focus only on creating planning artifacts, not implementing the feature
- Ask "Do the tasks look good?" after updating the implementation plan
- Update implementation plan when user requests changes
- Wait for explicit approval before considering workflow complete
- Continue feedback-revision cycle until explicit approval received
- Clearly communicate when planning workflow is complete
- Inform user they can begin execution by opening the implementation plan file

## PHASE 3 COMPLETION REQUIREMENT

- **NEVER generate code during Phase 3**
- **NEVER generate JSDoc during Phase 3**
- **ALWAYS ask "Do the tasks look good?" after creating/updating plan**
- **WAIT for explicit user approval before proceeding to Phase 4**
