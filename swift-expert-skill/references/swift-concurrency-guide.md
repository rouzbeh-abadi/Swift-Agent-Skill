# Swift Concurrency Guide

Use this file when reviewing or writing async Swift code.

## Structured Concurrency First

- Prefer `async` functions, task groups, and child tasks over unmanaged concurrency.
- Avoid `Task.detached` unless independence from the current actor and task tree is explicitly required.
- Keep async ownership obvious: who starts the task, who awaits it, and who can cancel it.

## Isolation

- Use `@MainActor` for UI-facing state and main-thread-bound behavior.
- Use actors when they protect truly shared mutable state.
- Avoid crossing actor boundaries more than needed in hot paths.

## Cancellation

- Treat cancellation as part of the API contract for long-running async work.
- Check cancellation in loops or before expensive follow-up work when appropriate.
- Avoid swallowing cancellation unless you are intentionally translating it.

## Sendability and Captures

- Keep captured state small and explicit in concurrent closures.
- Watch for non-sendable reference types crossing concurrency boundaries.
- Prefer passing values over sharing mutable references.

## Common Review Concerns

- Fire-and-forget tasks with unclear lifetime
- Detached tasks used where structured tasks would work
- UI state mutated off the main actor
- Async APIs that never mention cancellation or error behavior

## Review Checklist

- [ ] Task ownership and lifetime are clear
- [ ] Isolation is explicit where needed
- [ ] Cancellation is respected in long-running work
- [ ] Shared mutable state is protected appropriately
