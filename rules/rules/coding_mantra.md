# Coding Mantra

## Core Principle

Ship fast. Everything else serves this goal. Quality enables speed by making changes easier and safer.

## Pragmatic Principles

Be pragmatic over dogmatic. Don't strictly follow SOLID or DRY if it hurts the codebase. Apply DRY only after multiple repetitions, not at the second occurrence. Introduce abstractions only when their absence becomes painful.

## Code Quality

Write clear, simple code. Keep things minimal - implement only what's truly needed. Favor readability over cleverness. Name things precisely. Use consistent style. Keep functions small and focused on one thing at one abstraction level. Don't mix abstraction levels within functions. Avoid deep nesting and very long functions.

## Testing Strategy

Test critical paths that are complex or error-prone. Tests should help developers ensure their code works. If you don't need the safety net, don't write the test. No code coverage targets - 0% is bad, 100% is bad, something in between is optimal.

## Documentation

Avoid comments in code. Code should be self-explanatory. Comments go out of sync and become problems. Only comment what isn't obvious or would take minutes to understand.

## Development Practices

Handle errors explicitly. Validate inputs and sanitize outputs. Minimize attack surface. Prefer safe defaults. Run builds and tests regularly. Refactor mercilessly. Optimize last. Commit incrementally. Prefer removing code to adding code. The slimmer the codebase, the better.

## Quality Alignment

Align quality with software criticality. Mission-critical systems demand near-perfect quality. Test applications with few users can tolerate lower quality for faster iteration. Adjust quality standards and shipping speed accordingly.
