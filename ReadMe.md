# Customer Management API — Requirements

## Suggested Use Cases
- Add Update endpoint/service.
- Enforce unique email.
- Add search by name/email.
- Add unit tests.
- Add FluentValidation.
- Log create/delete.
- Introduce `ICustomerService` via DI.
- Improve Swagger docs.

## DI + SOLID
- Constructor injection only.
- Depend on interfaces (no concrete coupling).
- No `AppDbContext` in controllers.
- Scoped lifetimes for DbContext/repositories.
- No static mutable state.

## Repository Pattern
- Use repository interfaces for all persistence.
- Async methods with `CancellationToken`.
- Do not expose `IQueryable`.
- Keep business rules out of repositories.

## CQRS
- Separate Commands (writes) and Queries (reads).
- One handler per request.
- Controllers delegate via mediator/application service.
- Commands side-effecting; Queries read-only.

## FluentValidation
- Validator per API input/command/query.
- Auto-run validation.
- 400 for invalid input; 409 for conflicts.

## Controllers
- Thin actions; no persistence/business logic.
- Accept `CancellationToken`.
- Consistent routing/naming.

## Logging & Errors
- Structured logs with `ILogger<T>`.
- Global exception handling → Problem Details (400/404/409/500).
- Include correlation where available.

## Testing
- Unit tests: validators, handlers, repos (mock/in-memory).
- Integration tests: critical API paths and error mapping.
- Deterministic and isolated.