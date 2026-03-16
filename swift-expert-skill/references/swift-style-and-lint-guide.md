# Swift Style and Lint Guide

Use this file as the quick reference for SwiftLint-aligned formatting and cleanup concerns that are broadly useful across Swift projects. This is one part of the overall Swift skill, not the whole skill.

## High-Value Rules

### `trailing_whitespace`
- Remove spaces and tabs at the end of lines.
- This is usually safe to fix mechanically.

### `vertical_whitespace`
- Avoid excessive blank lines.
- Use blank lines to separate logical sections, not every statement.

### `line_length`
- Treat long lines as a readability warning.
- Wrap long calls, initializers, generic constraints, and conditions when scanning becomes harder.
- Teams may configure different thresholds, so prefer readability over chasing a single number.

### `force_unwrapping`
- Avoid `!` in ordinary production code.
- Prefer optional binding, `guard`, or explicit failure handling.

### `force_cast`
- Avoid `as!` unless the cast is guaranteed and failure is acceptable.
- Prefer safe casts with `as?` when the type is uncertain.

### `empty_count`
- Prefer `collection.isEmpty` over `collection.count == 0`.
- This reads more clearly and is the common SwiftLint preference.

### `redundant_nil_coalescing`
- Remove `?? nil` and similar no-op forms.

### `redundant_optional_initialization`
- Prefer `var value: String?` over `var value: String? = nil`.

### `unused_closure_parameter`
- Replace unused closure parameters with `_` when needed.
- Simplify closure signatures when possible.

### `operator_whitespace`
- Keep spacing around operators consistent.
- Avoid cramped or uneven expressions.

### `colon`
- Use consistent colon spacing in declarations, dictionaries, and type annotations.

### `comma`
- Use consistent comma spacing and multiline wrapping in lists and arguments.

### `control_statement`
- Avoid unnecessary parentheses in `if`, `guard`, `while`, and `switch` conditions.

## Judgment-Based Guidance

These are common style improvements, but they require some care:

- Prefer `let` over `var` when values do not change.
- Use `guard` when early exits make the function easier to read.
- Break apart very long chained expressions if the one-line form is hard to scan.
- Add explicit access control when API visibility is otherwise unclear.
- Do not rewrite large files purely for style if it creates unnecessary churn.

## Review Priorities

When reviewing or editing Swift code, use this order:
1. Mechanical formatting fixes
2. Unsafe patterns like `!` and `as!`
3. Redundant syntax cleanup
4. Readability improvements such as wrapping and simpler control flow
