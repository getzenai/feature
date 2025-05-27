# GitHub Issue Specification

After gathering requirements through clarification process, print issue draft to user. If approved, create GitHub issue using GitHub MCP tool. If MCP tool errors, fix root cause. Do not write to file instead.

## Issue Title Format

- "Add [feature] to enable [primary benefit]"
- "Implement [feature] for [user role]"

## Labels

Do not add any labels to the issue.

## Issue Body Format

```
As a [ROLE] I want [FEATURE], so that [BENEFIT]

## Acceptance Criteria

Observable outcomes and verifiable behaviors from ROLE perspective. Focus on what user can do or experience, not internal technical details. Must be specific and testable.

- When [condition/action by ROLE], [observable outcome for ROLE]
- [ROLE] can [action] and observe [result]

## Description

[Detailed description including context, motivation, and background]

## Technical Considerations

- **Dependencies**: [List dependencies or prerequisite features]
- **Affected Components**: [List components to be modified]
- **Potential Risks**: [Identify risks or challenges]

## Test Plan

[Describe testing approach with automated unit tests or end-to-end tests]

### Test Cases

1. **Verify [expected behavior] when [condition]**
   - **Setup**: [Initial state or preconditions]
   - **Action**: [Action triggering behavior]
   - **Expected Result**: [What should happen]

## Implementation Plan

1. [First major implementation step]
2. [Second major implementation step]
3. [Third major implementation step]
```
