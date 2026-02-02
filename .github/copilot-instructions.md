# Copilot Instructions for SMS-BeamZ (BeamZ)

## Project Context
BeamZ is a cost-competitive SMS API platform targeting developers who need reliable messaging at better prices than Twilio.

## Key Principles
1. **Price-first**: Every feature decision should consider cost impact
2. **Developer experience**: Simple API, great docs, helpful errors
3. **Reliability**: Carrier failover, retries, delivery guarantees
4. **Type safety**: TypeScript strict mode, no `any` types

## Tech Stack Preferences
- **Backend**: Node.js/Bun with TypeScript, Express/Fastify
- **Database**: PostgreSQL with Prisma/Drizzle ORM
- **Frontend**: Next.js 14 App Router, Tailwind, shadcn/ui
- **Testing**: Vitest for unit, Supertest for integration
- **Monorepo**: Turborepo for package management

## Code Style
- Use `async/await` over callbacks/promises
- Prefer named exports over default exports
- Use Zod for runtime validation
- Error handling: Always throw typed errors with codes
- Logging: Structured JSON logs with correlation IDs

## API Design
- RESTful endpoints with consistent naming
- JSON:API-style responses with `data` wrapper
- Pagination: cursor-based for lists
- Versioning: URL path (`/v1/`)
- Rate limiting: Per API key, 429 with retry-after

## Database Patterns
- Use UUIDs with `msg_` prefixes for message IDs
- Soft deletes with `deleted_at` timestamps
- Audit columns: `created_at`, `updated_at`
- Index foreign keys and frequently queried columns

## Testing Requirements
- Every new feature needs unit tests
- API endpoints need integration tests
- Minimum 80% coverage for core packages
- Mock external carrier APIs in tests

## Carrier Integration
- Abstract all carrier calls through `CarrierService`
- Implement circuit breaker for carrier failures
- Log all carrier requests/responses
- Support multiple carriers with weighted routing

## Security
- Validate all input with Zod schemas
- Sanitize phone numbers (E.164 format)
- Rate limit by API key and IP
- Hash API keys, store only prefixes for display

## Documentation
- Update OpenAPI spec for API changes
- JSDoc comments on public functions
- README updates for new features
- Changelog entries for releases

## Commit Messages
Follow conventional commits:
- `feat:` new features
- `fix:` bug fixes
- `docs:` documentation
- `chore:` maintenance
- `test:` test additions/fixes

## File Organization
```
apps/api/src/
├── routes/          # Express/Fastify routes
├── services/        # Business logic
├── repositories/    # Database access
├── middleware/      # Auth, validation, logging
├── utils/           # Helpers
└── types/           # TypeScript types
```

## When Unsure
1. Check AGENTS.md for architecture decisions
2. Look at existing patterns in codebase
3. Prioritize simplicity over cleverness
4. Ask for clarification if requirements unclear
