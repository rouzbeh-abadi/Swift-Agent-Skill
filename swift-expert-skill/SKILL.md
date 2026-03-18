---
name: swift-expert-skill
description: Write, review, refactor, or maintain Swift code across apps, packages, and libraries. Use for Swift language patterns, optionals and errors, concurrency, Swift Package Manager, tests, and SwiftLint-backed style cleanup.
license: MIT
compatibility: Designed for Agent Skills-compatible coding agents working in local Swift projects. SwiftLint and Swift Package Manager commands are optional when available.
---

# Swift Expert Skill

## Overview
Use this skill to write, review, or improve Swift code across language design, concurrency, package management, testing, and style guidance. SwiftLint support is part of the skill, not the whole skill.

## Workflow Decision Tree

### 1) Review existing Swift code
- Start with `references/swift-language-patterns.md` for optionals, errors, naming, and API shape
- Review task and actor usage against `references/swift-concurrency-guide.md`
- Check package layout and manifest choices with `references/swift-package-manager-guide.md`
- Review tests using `references/swift-testing-guide.md`
- Use `references/swift-style-and-lint-guide.md` for formatting, linting, and safe mechanical cleanup
- Flag unsafe patterns such as force unwraps, force casts, detached tasks without justification, and weak error handling
- Suggest local improvements first before proposing broad redesigns

### 2) Improve existing Swift code
- Apply low-risk lint and readability fixes first
- Simplify optional handling and error propagation when behavior stays the same
- Tighten concurrency boundaries: `@MainActor`, task ownership, cancellation, and isolation
- Improve package manifests and target boundaries when structure is unclear or brittle
- Strengthen tests around touched behavior
- Keep edits local unless the user explicitly wants a broader refactor

### 3) Implement new Swift code
- Start from clear APIs and obvious ownership
- Prefer safe optionals, explicit error handling, and focused types
- Use structured concurrency rather than ad hoc background work
- Keep package boundaries and dependencies intentional
- Add tests where the new behavior has meaningful logic
- Use the style guide for final cleanup

### 4) Maintain or package a Swift project
- Review `Package.swift` and target structure using `references/swift-package-manager-guide.md`
- Keep dependencies minimal and clearly scoped
- Prefer deterministic test and lint workflows
- Use `assets/swiftlint.yml` as a starting point when a project needs a basic SwiftLint configuration

## Core Guidelines

### Language and API Design
- Prefer small, focused types with clear ownership
- Use `let` by default and opt into mutation deliberately
- Keep public APIs explicit about failure, mutability, and async behavior
- Prefer descriptive argument labels when they improve call-site clarity
- Use protocols when they improve boundaries, not by default

### Optionals and Errors
- Avoid force unwraps and force casts unless the invariant is explicit and failure is acceptable
- Prefer `guard` and focused optional binding when they reduce nesting
- Surface meaningful errors rather than collapsing everything to `nil`
- Use `Result` only when it improves API clarity beyond `throws`

### Concurrency
- Prefer structured concurrency over unmanaged background work
- Use `@MainActor` for UI-facing state and main-thread-bound code
- Respect cancellation in long-running async work
- Avoid detached tasks unless independence is required and understood
- Keep actor boundaries and sendable expectations explicit

### Swift Package Manager
- Keep target boundaries focused and dependency graphs easy to reason about
- Avoid unnecessary package dependencies when standard library or Foundation is enough
- Use target-specific test targets and keep package manifests readable
- Prefer stable package products and clear platform declarations

### Testing
- Add or update tests when behavior changes in meaningful ways
- Prefer deterministic tests with clear setup and assertions
- Keep test helpers simple and local to the behavior they support
- Test async behavior with clear expectations around cancellation, ordering, and failure

### Style and Linting
- Use `references/swift-style-and-lint-guide.md` for SwiftLint-aligned formatting and cleanup
- Prefer mechanical lint fixes before judgment-heavy style rewrites
- Do not assume every project uses the exact same lint config
- Use `assets/swiftlint.yml` as a starter, not a rulebook

## Quick Reference

### Topic Map
| Topic | Reference |
|------|-----------|
| Language patterns | `references/swift-language-patterns.md` |
| Concurrency | `references/swift-concurrency-guide.md` |
| Package management | `references/swift-package-manager-guide.md` |
| Testing | `references/swift-testing-guide.md` |
| Style and linting | `references/swift-style-and-lint-guide.md` |

### Typical Examples
```swift
// Prefer a focused early exit for optionals
guard let url = URL(string: value) else {
    throw NetworkError.invalidURL(value)
}

// Prefer structured concurrency
let data = try await client.fetchProfile(id: userID)

// Prefer isEmpty when emptiness is the real question
if items.isEmpty {
    return []
}
```

## Review Checklist

- [ ] APIs communicate ownership, async behavior, and failure clearly
- [ ] Optionals and errors are handled safely and readably
- [ ] Concurrency uses structured tasks, clear isolation, and cancellation awareness
- [ ] Package manifests and target boundaries are intentional
- [ ] Tests cover touched behavior where logic changed
- [ ] Formatting and linting issues are cleaned up without unnecessary churn
- [ ] Force unwraps and force casts are avoided or clearly justified
- [ ] `let` is used where mutation is not needed
- [ ] `isEmpty` and other common readability improvements are applied where appropriate

## References
- `references/swift-language-patterns.md` - Core Swift language, optionals, errors, and API-shape guidance
- `references/swift-concurrency-guide.md` - Structured concurrency, isolation, and cancellation guidance
- `references/swift-package-manager-guide.md` - Package manifests, target boundaries, and dependency hygiene
- `references/swift-testing-guide.md` - Testing structure and practical review guidance
- `references/swift-style-and-lint-guide.md` - SwiftLint-aligned formatting and cleanup guidance
