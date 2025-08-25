# Phase 2: Create Feature Design Document

After the user approves the Requirements, you should develop a comprehensive design document based on the feature requirements, conducting necessary research during the design process.

## Prerequisites
- Ensure the requirements document exists first
- Create 'specs/{feature_name}/02-design.md' file if it doesn't exist

## Research and Context Building
- Identify areas where research is needed based on the feature requirements
- Conduct research and build up context in the conversation thread
- Use research as context for design, not separate research files
- Summarize key findings that will inform the feature design
- Cite sources and include relevant links in the conversation

## Design Document Structure
The design document should include these core sections:
- **Overview**
- **Architecture**
- **Components and Interfaces**
- **Data Models**
- **Error Handling**
- **Testing Strategy**

### Additional Sections for GUI Features
- **UI/UX Design**
- **Responsive Design**
- **Accessibility**

## Design Process Guidelines
- Focus on design documentation only
- Ensure the design addresses all feature requirements identified during the clarification process
- Incorporate research findings directly into the design process
- Highlight design decisions and their rationales
- Ask for user input on specific technical decisions during the design process
- Offer to return to requirements clarification if gaps are identified during design

## Visual Elements
- Use ASCII art and emojis to create wireframes in the design document
- Include diagrams or visual representations when appropriate (use Mermaid for diagrams)

## Documentation and Testing Focus
- Skip JSDoc generation throughout the phase cycle - focus on implementation over documentation
- If JSDoc is needed in the future, user will provide adhoc request
- Focus test cases on runtime behavior, not compile-time validation (TypeScript handles syntax errors)

## Iteration and Approval Process
- Update design document when user requests changes
- Ask "Does the design look good? If so, we can move on to the implementation plan" after updates
- Wait for explicit approval before moving to implementation plan
- Continue feedback-revision cycle until explicit approval received
