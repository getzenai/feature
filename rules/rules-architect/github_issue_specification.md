# GitHub Issue Specification Format

After gathering requirements through the clarification process, print out the issue draft to the user. If the user is ok with that, create a GitHub issue using the following format and the GitHub MCP tool. If the MCP tool errors, try to fix the root cause. Do not write to a file instead.

## Issue Title Format

Use a clear, concise title that summarizes the feature:

- "Add [feature] to enable [primary benefit]"
- "Implement [feature] for [user role]"

## Labels

Do not add any labels to the issue.

## Issue Body Format

<issue_body>
As a [ROLE] I want [FEATURE], so that [BENEFIT]

> Example: As a developer I want automatic code formatting on save, so that I can maintain consistent code style without manual effort.

## Acceptance Criteria

A checklist describing the **observable outcomes and verifiable behaviors** from the perspective of the ROLE. These criteria should focus on **what the user can do or experience**, rather than internal technical implementation details. They should be specific and testable. Non-functional requirements (like performance) can be included if they directly impact user experience.

- Strive for clear and concise statements.
- Example format: "When [condition/action by ROLE], [observable outcome for ROLE]."
- Or: "[ROLE] can [action] and observe [result]."

> Example (for a feature: "Automatic Code Formatting on Save"):
>
> - [ ] When a developer saves a code file, its content is automatically reformatted according to the project's style guide.
> - [ ] Developers can disable auto-formatting for specific files (e.g., via a comment), preventing changes on save for those files.
> - [ ] Auto-formatting on save completes without noticeable delay to the developer's workflow (e.g., under 500ms for typical files).
> - [ ] If auto-formatting encounters an error during save, the developer receives a clear and non-disruptive notification about the issue.

## Description

[Detailed description of the feature, including context, motivation, and any relevant background information]

## Technical Considerations

- **Dependencies**: [List any dependencies or prerequisite features]
- **Affected Components**: [List components that will be modified]
- **Potential Risks**: [Identify potential risks or challenges]

## Test Plan

[Describe how this feature should be tested with automated unit tests or end-to-end tests]

### Test Cases

Use natural language to describe test scenarios:

1. **Verify [expected behavior] when [condition]**
   - **Setup**: [Describe the initial state or preconditions]
   - **Action**: [Describe the action that triggers the behavior]
   - **Expected Result**: [Describe what should happen]

> Example:
>
> 1. **Verify code is formatted when file is saved**
>    - **Setup**: Open a JavaScript file with formatting issues
>    - **Action**: Save the file
>    - **Expected Result**: File content is automatically reformatted according to style rules

## Implementation Plan

Use the following natural language format to describe the implementation approach:

Step-by-Step Approach

1. [First major implementation step in natural language]
2. [Second major implementation step in natural language]
3. [Third major implementation step in natural language]

> Example:
>
> 1. Add a file save event listener to the editor component
> 2. Integrate with the existing code formatter library
> 3. Add user configuration options for enabling/disabling the feature

</issue_body>
