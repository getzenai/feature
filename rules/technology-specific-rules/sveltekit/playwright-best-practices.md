# Playwright Best Practices

See: https://playwright.dev/docs/best-practices

## Test User-Visible Behavior

- Focus on testing what users see and interact with
- Avoid testing implementation details
- Test against rendered output rather than internal state
- Avoid testing third-party dependencies

## Test Isolation

- Each test should be completely independent
- Use [`beforeEach`](https://playwright.dev/docs/api/class-test#test-before-each) hooks for common setup
- Avoid test dependencies
- Consider using setup projects for shared state (e.g., authentication)
- Ensure tests have their own local storage, session storage, data, and cookies

## Locator Best Practices

- Use built-in locators with auto-waiting capabilities
- Prefer user-facing attributes over CSS/XPath selectors
- Chain and filter locators for precise element selection
- Note: Shadcn [`button`](https://ui.shadcn.com/docs/components/button) components automatically render as `a` elements when provided with [`href`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href) prop

## Assertions

- Use web-first assertions that auto-wait for conditions
- Implement soft assertions for non-critical checks
- Focus on user-visible outcomes
- Use assertions that wait until expected condition is met

## Test Configuration

- Configure browser projects in Playwright config
- Use TypeScript for better type safety
- Implement proper test isolation in configuration
- Configure proper timeouts and retries

## Debugging

- Use trace viewer for CI failures instead of videos/screenshots
- Configure traces in Playwright config file

## Cross-Browser Testing

- Test across all major browsers (Chromium, Firefox, WebKit)
- Keep Playwright dependencies up to date

## Performance Optimization

- Use parallelism and sharding for faster test execution
- Configure test projects for different browsers
