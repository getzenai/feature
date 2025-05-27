# Feature Specification Clarification Process

When a user requests a new feature specification that lacks sufficient detail, use this structured approach to gather requirements and uncover blind spots:

## 1. Core Requirements Gathering

Ask questions about:

- Primary user goals and expected outcomes
- Key functionality requirements
- Integration points with existing features
- Performance expectations
- Priority level and timeline constraints

## 2. Edge Case Exploration

Ask questions about:

- Error handling and recovery
- Unusual usage patterns
- Resource constraints (memory, processing, storage)
- Security implications
- Accessibility requirements

## 3. Implementation Considerations

Ask questions about:

- Technical dependencies
- Potential architectural impacts
- Deployment considerations
- Maintenance requirements
- Testing approach

## Question Guidelines

- Ask one question at a time using the `ask_followup_question` tool
- Provide 2-4 suggested answers to make responding easier
- Make questions specific and actionable
- Avoid yes/no questions; prefer open-ended questions
- Acknowledge and build upon previous answers
- **Do not ask questions with obvious answers or information that can be retrieved from the project context**
- **Provide multiple detailed suggestions with each question to guide the user and demonstrate your understanding**
- When suggesting answers, make them comprehensive enough that the user can select one without needing to add significant additional information

## Example Questions

- "Who are the primary users of this feature and what problem does it solve for them?"
- "What specific actions should users be able to perform with this feature?"
- "How should the system handle [specific edge case]?"
- "What existing components will this feature interact with?"
- "What metrics would indicate this feature is successful?"

## Example Suggestions

When asking about implementation approach:

```
<suggest>
We should implement this as a standalone module in the strategies/ directory that follows the Strategy pattern like our existing analyzer strategies. This would include creating a new strategy class that extends AnalyzerStrategy, adding it to the strategy factory, and updating the CLI to support the new mode.
</suggest>

<suggest>
We could integrate this directly into the existing CapabilitiesStrategy class by adding a new analysis mode parameter that toggles between the current behavior and the new feature. This would require minimal changes to the existing architecture but might make the class more complex.
</suggest>
```

After gathering sufficient information, synthesize the responses into a comprehensive specification following the GitHub issue format.
