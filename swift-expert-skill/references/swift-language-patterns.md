# Swift Language Patterns Reference

Use this file when reviewing or writing everyday Swift code that is not primarily about UI frameworks.

## Core Principles

- Prefer clarity over cleverness.
- Keep types and functions focused.
- Make ownership, mutability, failure, and asynchrony obvious from the API.

## Optionals

- Prefer safe unwrapping with `guard` or `if let`.
- Avoid force unwraps unless the invariant is explicit and local.
- Return optionals when absence is expected; throw errors when failure needs explanation.

## Errors

- Use `throws` when callers need meaningful failure information.
- Prefer domain-specific error types over opaque generic errors.
- Keep error surfaces proportional to the API: do not over-engineer tiny helpers.

## Mutability

- Prefer `let` by default.
- Use `mutating` deliberately on value types.
- Avoid shared mutable state unless synchronization is clear and intentional.

## API Shape

- Use argument labels to make call sites read clearly.
- Prefer specific types over `Any` or loosely typed dictionaries.
- Use generics when they improve reuse without making the API harder to understand.
- Use protocols to define boundaries, not just to pre-emptively abstract everything.

## Collections and Control Flow

- Prefer `isEmpty` when emptiness is the real question.
- Use higher-order functions when they are readable; do not force chained functional style.
- Prefer early exits over deep nesting when it simplifies the happy path.

## Review Checklist

- [ ] Optional handling is safe and clear
- [ ] Errors communicate useful failure information
- [ ] Mutation is intentional and minimal
- [ ] APIs read clearly at the call site
- [ ] Control flow is easy to scan
