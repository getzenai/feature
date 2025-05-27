# Feature Specification Clarification Process

When a user requests a new feature specification that lacks sufficient detail, use this structured approach to gather requirements and uncover blind spots:

## Requirements Gathering

- Primary user goals and expected outcomes
- Key functionality requirements
- Integration points with existing features
- Performance expectations
- Priority level and timeline constraints

## Edge Case Exploration

- Error handling and recovery
- Unusual usage patterns
- Resource constraints (memory, processing, storage)
- Security implications
- Accessibility requirements

## Implementation Considerations

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
- Do not ask questions with obvious answers or information retrievable from project context
- Provide multiple detailed suggestions demonstrating understanding
- Make suggestions comprehensive enough for user selection without additional information

## Example Questions

- "Who are the primary users of this feature and what problem does it solve for them?"
- "What specific actions should users be able to perform with this feature?"
- "How should the system handle [specific edge case]?"
- "What existing components will this feature interact with?"
- "What metrics would indicate this feature is successful?"

After gathering sufficient information, synthesize responses into comprehensive specification.
