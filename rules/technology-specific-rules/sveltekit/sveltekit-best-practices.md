# SvelteKit Best Practices

## Project Architecture

- Route organization: Use route groups `(protected)`, `(auth)`, `(admin)` to organize related pages
- API structure: Place backend logic in `src/routes/api/...` for clear separation
- Server-side logic: Keep external API calls and sensitive operations in server-side files (`+page.server.ts`, API routes)
- Component organization: Structure components by feature rather than type

## Route Organization and Protection

### Route Groups

- Protected routes: Use `+layout.server.ts` in `(protected)` group to enforce authentication
- Public routes: Use `+page.server.ts` to redirect authenticated users from auth pages
- Admin routes: Create separate `(admin)` group with role-based access checks

### Route Protection Patterns

- Layout-level protection: Use `+layout.server.ts` for route group authentication
- Page-level checks: Use `+page.server.ts` for specific page requirements
- API protection: Implement authentication middleware in `hooks.server.ts`

## Load Functions

### Server Load Functions (`+page.server.ts`, `+layout.server.ts`)

- Use for: Authentication checks, database queries, server-side data fetching
- Benefits: Available during SSR, access to request headers and cookies
- Security: Handle redirects and sensitive operations server-side
- Performance: Reduce client-side API calls by pre-loading data

### Universal Load Functions (`+page.ts`, `+layout.ts`)

- Use for: Client-side data transformations and non-sensitive fetching
- Behavior: Run on both server and client environments
- Limitations: Avoid sensitive authentication logic or server-only operations

## Authentication and Security

### Server-Side Authentication

- Always verify on server: Use `+page.server.ts` or `+layout.server.ts` for authentication checks
- Never trust client-side: Client-side checks are for UX only, not security
- Session verification: Use [`auth.api.getSession({ headers: requestHeaders })`](src/lib/auth.ts) in server load functions
- Prevent bypass: Server-side checks cannot be disabled or manipulated

### Secure Redirect Patterns

- Server-side redirects: Use [`throw redirect(303, '/target-url')`](<src/routes/(protected)/+layout.server.ts:25>) for authentication flows
- Security advantage: Cannot be bypassed by disabling JavaScript
- Client redirects: Use only for UX enhancements, never for security

### Security Principles

- Defense in depth: Layer server-side security with client-side UX
- Fail secure: Default to denying access when authentication is unclear
- Minimize exposure: Keep sensitive logic and secrets server-side only
- Validate inputs: Sanitize and validate all user inputs on the server

## API Design

### API Route Structure

- RESTful patterns: Use HTTP methods appropriately (GET, POST, PUT, DELETE)
- Error handling: Return consistent error responses with proper status codes
- Input validation: Validate request bodies and parameters server-side
- Response format: Use consistent JSON response structures

### API Security

- Authentication: Verify user sessions in API route handlers
- Authorization: Check user permissions for specific operations
- Rate limiting: Implement rate limiting for API endpoints
- CORS handling: Configure CORS appropriately for your deployment
