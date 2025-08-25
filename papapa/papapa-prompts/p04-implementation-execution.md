# Phase 4: Execute Implementation Plan

After the user approves the Implementation Plan, you should execute the planned tasks in order, following the specifications from the requirements and design documents.

## Prerequisites
- Ensure the implementation plan document exists first
- Before executing any tasks, ALWAYS ensure you have read the specs 01-requirements.md, 02-design.md and 03-implementation-plan.md files
- Executing tasks without the requirements or design will lead to inaccurate implementations

## File Management
- Update 'specs/{feature_name}/03-implementation-plan.md' file to mark completed tasks
- Create 'specs/{feature_name}/04-changes-log.md' file if it doesn't exist
- Document plan deviations, manual changes, and ad-hoc modifications in changes log (not successful execution of planned tasks)
- Categorize changes: requirements, design, implementation, or new insights
- Include context about why changes were made
- Update changes log after each significant modification

## Phase Navigation Rules
- Return to implementation plan phase if user indicates plan changes are needed
- Return to design phase if user indicates design changes are needed
- Return to requirements phase if user indicates additional requirements are needed

## Task Execution Guidelines
- Distinguish between information requests and execution requests
- Provide task information without executing when user asks questions
- Only execute tasks when user explicitly requests implementation
- Answer questions about task details, progress, or next steps without starting execution
- Execute only ONE task at a time, do not proceed to next task automatically
- If task has sub-tasks, always start with the sub-tasks first
- Focus only on the requested task, do not implement functionality for other tasks
- Execute tasks in the order specified in the implementation plan
- Continue to next task only after current task is successfully completed
- Stop after completing each task and wait for user review
- Recommend next task to execute if user doesn't specify which one

## Task Progress Tracking
- Mark checkboxes as completed after successful task execution
- Add execution notes and timestamps under completed tasks
- Update task descriptions with execution status and any issues encountered
- Add completion timestamps to finished tasks
- Include brief notes about implementation details under completed tasks
- Preserve the original task structure while adding execution metadata

## Quality Assurance
- Handle errors gracefully and provide clear error messages
- Verify implementation against requirements before marking task complete
- Verify each completed task meets the requirements
- Test functionality after completing related tasks
- Ensure code follows the design specifications
- Validate that implementation matches the requirements

## Implementation Constraints
- Focus only on executing the planned tasks, not adding new features
- Follow the implementation plan strictly without deviation

## Workflow Completion
- Ask "Does the implementation look good?" after completing all tasks
- Update implementation if user requests changes
- Wait for explicit approval before considering implementation complete
- Continue feedback-revision cycle until explicit approval received
- Clearly communicate when all planned tasks are complete
