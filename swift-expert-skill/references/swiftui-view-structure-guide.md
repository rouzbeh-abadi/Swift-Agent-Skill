# SwiftUI View Structure Guide

Use this file when reviewing or writing SwiftUI screens that are starting to collect too many view fragments directly inside one `body`.

## Core Rule

- Keep the main `body` readable by composing it from named sections.
- Prefer extracting meaningful sections instead of letting one large `body` absorb every `VStack`, `HStack`, and conditional branch.
- Do not extract every single line mechanically; extract at the level of real sections and responsibilities.

## Preferred Extraction Order

- For a small local section, use a private computed view property.
- For a small conditional or parameterized local section, use a private `@ViewBuilder` function when it improves clarity.
- For complex, reusable, or stateful UI, extract a separate subview `struct`.

## Preferred File Layout

- Keep stored properties on the main type declaration.
- Put the main `View` conformance and `body` in the first extension, usually under `// MARK: - View`.
- Put extracted sections, helpers, and local view-building logic in a separate `private extension` under a clear MARK such as `// MARK: - Sections`.
- Prefer a few categorized extensions such as `View`, `Sections`, `Actions`, or `Helpers` rather than one extension per property or function.
- Use additional MARK sections only when they reflect real responsibilities.

```swift
struct CheckoutScreen {
    let title: String
    let total: Decimal
    @State private var canCheckout = false
}

// MARK: - View
extension CheckoutScreen: View {
    var body: some View {
        ScrollView {
            VStack(spacing: 24) {
                headerSection
                actionsSection
            }
            .padding()
        }
    }
}

// MARK: - Sections
private extension CheckoutScreen {
    var headerSection: some View {
        VStack(alignment: .leading, spacing: 8) {
            Text(title)
            Text(total.formatted(.currency(code: "USD")))
        }
    }

    @ViewBuilder
    var actionsSection: some View {
        if canCheckout {
            checkoutButton
        } else {
            unavailableNotice
        }
    }
}
```

## When a Computed View Property Is a Good Fit

- The section is short and easy to understand.
- The section only depends on a small amount of local state.
- The section is local to the parent view and does not need reuse elsewhere.

```swift
private var headerSection: some View {
    VStack(alignment: .leading, spacing: 8) {
        Text(title)
            .font(.title2.bold())
        Text(subtitle)
            .foregroundStyle(.secondary)
    }
}
```

## When an `@ViewBuilder` Function Is a Good Fit

- The section needs parameters.
- The section has a little conditional composition.
- The section is still small enough that a full subview would add more ceremony than value.

```swift
@ViewBuilder
private func amountRow(title: String,
                       amount: Decimal,
                       highlight: Bool) -> some View {

    HStack {
        Text(title)
        Spacer()
        Text(amount.formatted(.currency(code: "USD")))
            .fontWeight(highlight ? .semibold : .regular)
    }
}
```

## When to Prefer a Separate Subview

- The section is large or visually complex.
- The section is reused in multiple screens.
- The section has its own state, bindings, or interaction logic.
- The parent `body` is still hard to scan after smaller extractions.

```swift
struct SummaryCard: View {
    let title: String
    let total: Decimal

    var body: some View {
        VStack(alignment: .leading, spacing: 12) {
            Text(title)
                .font(.headline)
            Text(total.formatted(.currency(code: "USD")))
                .font(.title3.bold())
        }
        .padding()
        .background(.thinMaterial)
        .clipShape(RoundedRectangle(cornerRadius: 16))
    }
}
```

## Example Composition

```swift
var body: some View {
    ScrollView {
        VStack(spacing: 24) {
            headerSection
            summarySection
            actionsSection
        }
        .padding()
    }
}

private var summarySection: some View {
    SummaryCard(title: "Total", total: total)
}

@ViewBuilder
private var actionsSection: some View {
    if canCheckout {
        checkoutButton
    } else {
        unavailableNotice
    }
}
```

## Review Checklist

- [ ] The main `body` stays readable and focused on composition
- [ ] Large screens are broken into named sections instead of one long `body`
- [ ] SwiftUI files are organized with clear `// MARK: -` sections and focused extensions when that improves readability
- [ ] Small local sections use computed vars or `@ViewBuilder` only when that improves readability
- [ ] Complex, reusable, or stateful sections are extracted into separate subviews
- [ ] Extraction improves clarity rather than adding arbitrary indirection
