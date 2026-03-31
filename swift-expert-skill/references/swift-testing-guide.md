# Swift Testing Guide

Use this file when reviewing or writing tests for Swift code.

## Testing Principles

- Test behavior, not implementation trivia.
- Keep setup obvious and assertions specific.
- Prefer deterministic tests that do not depend on timing, order, or shared state unless the behavior itself requires it.
- When meaningful logic is extracted into a smaller function, add or update tests so the new behavior is directly covered.

## Unit Tests

- Keep the subject under test clear in each case.
- Use small helpers to reduce duplication, but keep them local and readable.
- Prefer descriptive test names that explain the scenario and expected result.
- Add tests to the most relevant existing test file when one already matches the type or feature.
- Create a new test file when the behavior has no clear existing test home.
- Do not add low-value tests for trivial wrappers, delegate forwarding, or framework glue with no meaningful logic.

## Async Tests

- Make async expectations explicit.
- Test failure, cancellation, and success paths when they matter.
- Avoid sleeps and timing guesses when stronger coordination is available.

## Review Checklist

- [ ] Tests cover meaningful behavior changes
- [ ] Extracted logic with real behavior is directly tested when appropriate
- [ ] Setup and assertions are easy to read
- [ ] Async tests are deterministic
- [ ] Helpers do not hide the intent of the test
