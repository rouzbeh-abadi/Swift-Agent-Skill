# Swift Package Manager Guide

Use this file when working with `Package.swift`, package structure, targets, dependencies, and publishing concerns.

## Package Design

- Keep target boundaries focused and easy to explain.
- Prefer small dependency surfaces between targets.
- Separate production and test dependencies cleanly.

## Manifest Guidance

- Keep platform declarations explicit when they matter.
- Use product, target, and dependency names that match the package structure clearly.
- Avoid overly dynamic manifest logic when a straightforward declaration is enough.

## Dependencies

- Add external packages deliberately; prefer fewer dependencies when the value is small.
- Scope dependencies to the targets that need them.
- Keep version requirements intentional and understandable.

## Tests and Fixtures

- Give each production target the test target it needs.
- Keep fixtures close to the tests that use them.
- Avoid package-level complexity when a simple local helper is enough.

## Review Checklist

- [ ] Manifest is readable and explicit
- [ ] Target boundaries are sensible
- [ ] Dependencies are minimal and scoped
- [ ] Test targets and fixtures are organized clearly
