# SwiftUI ViewModel Guide

Use this file when reviewing or writing SwiftUI screens and deciding whether a view should own local state or delegate logic to a ViewModel.

## Core Rule

- Do not create a ViewModel for every view by default.
- Use a ViewModel when it improves state ownership, async coordination, testability, or presentation-specific transformation.
- Keep presentational and reusable leaf views simple when local state or passed-in data is enough.

## When a ViewModel Is a Good Fit

- The view loads or refreshes data asynchronously.
- The view owns screen-level state such as loading, error, and loaded content.
- The UI needs transformation logic that should be tested separately from rendering.
- The screen coordinates multiple dependencies or actions.

## When a ViewModel Is Usually Not Needed

- The view is a small reusable component that only renders provided data.
- The view only owns simple local UI state such as selection, expansion, or text field focus.
- Adding a ViewModel would only forward properties without real logic.

## Preferred Shape

- Keep UI-facing observable state on the main actor.
- Give the ViewModel one clear responsibility, usually one screen or flow.
- Keep networking, persistence, and domain logic in services rather than stuffing everything into the ViewModel.
- Let views focus on composition and rendering.

## Examples

```swift
// Good fit: screen-level state and async work
@MainActor
final class ProfileViewModel: ObservableObject {
    @Published private(set) var profile: Profile?
    @Published private(set) var isLoading = false

    private let client: APIClient

    init(client: APIClient) {
        self.client = client
    }

    func load() async {
        isLoading = true
        defer { isLoading = false }

        do {
            profile = try await client.fetchProfile()
        } catch {
            profile = nil
        }
    }
}
```

```swift
// No ViewModel needed: simple presentational component
struct StatusBadge: View {
    let title: String

    var body: some View {
        Text(title)
            .padding(.horizontal, 8)
            .padding(.vertical, 4)
            .background(.blue.opacity(0.1))
            .clipShape(Capsule())
    }
}
```

## Review Checklist

- [ ] A ViewModel exists for clear reasons, not by template
- [ ] Small presentational views stay lightweight
- [ ] Screen-level async work and state ownership are easy to follow
- [ ] UI-facing observable state stays on the main actor
- [ ] Services and domain logic are not unnecessarily collapsed into the ViewModel
