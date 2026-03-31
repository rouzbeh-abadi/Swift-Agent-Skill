# Swift Language Patterns Reference

Use this file when reviewing or writing everyday Swift code that is not primarily about UI frameworks.

## Core Principles

- Prefer clarity over cleverness.
- Keep types and functions focused.
- Make ownership, mutability, failure, and asynchrony obvious from the API.
- Prefer smaller, cohesive functions when they make logic easier to read, reuse, and test.

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

## Reusable Helpers and Extensions

- When logic is general-purpose or reused in multiple places, extract it into a focused helper, utility type, or extension instead of rewriting it inline.
- Prefer an extension when the behavior naturally belongs to an existing type.
- Prefer a small helper type or wrapper when the behavior needs configuration, state, or lifecycle management.
- Avoid vague catch-all utility files when a more focused abstraction would be clearer.
- For expensive shared objects such as formatters, prefer a reusable cached instance rather than recreating it repeatedly.
- When a reusable helper or extension contains meaningful behavior, treat it as logic that should usually receive direct unit tests.

```swift
extension DateFormatter {
    static let displayDate: DateFormatter = {
        let formatter = DateFormatter()
        formatter.dateStyle = .medium
        formatter.timeStyle = .none
        return formatter
    }()
}
```

## UserDefaults

- Avoid scattering raw `UserDefaults` keys across the codebase.
- Centralize keys in a dedicated namespace type so reads, writes, and removals stay consistent.
- Wrap related `UserDefaults` access in a focused store type instead of repeating string-based calls everywhere.
- Inject the `UserDefaults` instance when possible so the store can be tested with an isolated suite.
- If a reset-all operation is needed, clear only the keys owned by that store rather than wiping unrelated defaults.

```swift
private enum DefaultsKey {
    static let hasSeenOnboarding = "hasSeenOnboarding"
    static let preferredTheme = "preferredTheme"

    static let all = [
        hasSeenOnboarding,
        preferredTheme
    ]
}

final class AppSettingsStore {
    private let defaults: UserDefaults

    init(defaults: UserDefaults = .standard) {
        self.defaults = defaults
    }

    func setHasSeenOnboarding(_ value: Bool) {
        defaults.set(value, forKey: DefaultsKey.hasSeenOnboarding)
    }

    func hasSeenOnboarding() -> Bool {
        defaults.bool(forKey: DefaultsKey.hasSeenOnboarding)
    }

    func removeHasSeenOnboarding() {
        defaults.removeObject(forKey: DefaultsKey.hasSeenOnboarding)
    }

    func removeAll() {
        for key in DefaultsKey.all {
            defaults.removeObject(forKey: key)
        }
    }
}
```

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
- [ ] Functions stay focused when splitting logic improves clarity or testability
- [ ] Reusable cross-cutting logic is extracted into focused helpers or extensions when appropriate
- [ ] Reusable helpers and extensions with real behavior are supported by direct unit tests when appropriate
- [ ] `UserDefaults` usage is centralized, focused, and avoids scattered raw keys
