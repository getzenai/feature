# Architecture Decision Record (ADR) Creation

As `rules-architect`, propose creating an Architecture Decision Record (ADR) for significant architectural decisions to document rationale and ensure team transparency. **ADRs should be saved in the `documentation/architecture_decision_record/` directory.**

## When to Create an ADR

Create an ADR if a decision:

- Significantly impacts system architecture.
- Requires justification among multiple viable options.
- Affects non-functional requirements (performance, security, etc.).
- Involves a long-term commitment to a technology or pattern.
- Is likely to be revisited or questioned.
- Involves an important trade-off.

## ADR Structure

Use this structure for ADRs. Filename: `NNN-short-title-for-adr.md` (e.g., `001-use-of-serverless-functions.md`).

```
# NNN. Title of the ADR

*   **Date**: YYYY-MM-DD
*   **Status**: Proposed | Accepted | Deprecated | Superseded by [ADR-XYZ](link-to-ADR-XYZ)

## Context

Briefly describe the problem or need driving this decision and its scope.

## Decision Drivers

Key requirements, constraints, and forces influencing the decision (e.g., business needs, technical limitations, quality attributes, project constraints).

## Considered Options

List and briefly describe considered options:

*   **Option 1: [Name]**
    *   Description, Pros, Cons.
*   **Option 2: [Name]**
    *   Description, Pros, Cons.
*   ... (etc.)

## Decision Outcome

*   **Chosen Option**: [Name of Chosen Option]
*   **Justification**: Why this option was selected, how it addresses drivers, and expected positive outcomes.

## Consequences

*   **Positive**: [List positive impacts]
*   **Negative (and Mitigation)**: [List negative impacts and mitigation strategies]
*   **Risks**: [Associated risks]

## Links / References (Optional)

*   [Relevant documents, discussions, prototypes]

## Stakeholders (Optional)

*   [Key stakeholders]
```
