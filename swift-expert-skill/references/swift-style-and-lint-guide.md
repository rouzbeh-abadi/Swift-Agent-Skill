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

## Function Declarations and Comments

- For long function signatures, keep the function name and first parameter on the same line.
- Align wrapped parameters vertically for easier scanning.
- Keep the return type and opening brace on the final signature line when the declaration still reads clearly.
- In multi-line function bodies, prefer a single blank line after the opening brace when that matches the project or house style.
- Add a short `///` summary for public APIs and non-obvious functions.
- Mention important side effects, async or throwing behavior, or assumptions when that context helps.
- Avoid comments that only restate the function name.

```swift
/// Calculates the final total after tax and discount are applied.
func calculateTotal(for subtotal: Decimal,
                    taxRate: Decimal,
                    discountRate: Decimal) -> Decimal {

    let taxedAmount = subtotal + (subtotal * taxRate)
    let finalAmount = taxedAmount - (taxedAmount * discountRate)
    return finalAmount
}
```

## Debug Output

- Avoid leaving ad hoc `print` calls in production app code.
- Prefer `Logger` for application logging that should remain in the codebase.
- If temporary console debugging is needed during development, prefer `debugPrint` over `print` for developer-focused inspection.
- `print` is still reasonable for simple scripts, playgrounds, or intentional CLI output.

## Review Priorities

When reviewing or editing Swift code, use this order:
1. Mechanical formatting fixes
2. Unsafe patterns like `!` and `as!`
3. Redundant syntax cleanup
4. Readability improvements such as wrapping and simpler control flow
5. Function declarations and comments that are hard to scan or lack needed context
6. Temporary debug output that should be removed or upgraded to real logging
