You are responsible for breaking down the brain/project.md into small, structured steps.

Your goal is to create a step-by-step plan to guide the code generation for a full stack application based on a provided specification.

Each step should be concrete enough for the AI to implement in a single iteration. Mix frontend and backend tasks if it makes sense.

When creating your plan:

1. Start with the project structure.
2. Define the backend, including data schema and API.
3. Define the frontend, including identifying the pages you will need.
4. Break down frontend from pages into smaller, focused steps.
5. Include steps for connecting frontend and backend.
6. Ensure that each step builds upon the previous one in a logical planner.

Present your plan for implementing using the following format:
```
# Implementation Plan

## [Section Name]
- [ ] Step 1: [Brief title]
  - **Task**: [Detailed explanation of what needs to be implemented]
  - **Files**: [Maximum of 20 files, ideally less]
    - `path/to/file1.ts`: [Description of changes]
  - **Step Dependencies**: [Step Dependencies]
  - **User Instructions**: [Instructions for User]
```

After presenting your plan, provide a brief summary of the overall approach and any key considerations for the implementation process.

Remember to:

1. Ensure that your plan covers all aspects of the technical specification.
2. Break down complex features into smaller, manageable tasks.
3. Consider the logical order of implementation, ensuring that dependencies are addressed in the correct sequence.

Next, output a markdown file that contains the architecture. Sample format:

```
# Architecture
## Overall Technical Approach
-Describe the techincal approach and stack at a high level
-Include mermaid diagrams if necessary

## Frontend
-Provide an overview of how the frontend is architected, including user UI flows
-Describe the various pages and components in src/frontend and what they do

## Backend
-Provide an overview of how the backend is architected, including data flows
-Describe the various pages and components in src/backend and what they do
```