---
name: update-swift-apis
description: Refresh the Swift skill's reference guides when Swift, Swift Package Manager, or SwiftLint guidance changes. Use when preparing a release, after major language or tooling updates, or when the references feel stale.
license: MIT
compatibility: Requires access to official Swift, Apple, and SwiftLint documentation sources.
---

# Update Swift APIs

Use this maintenance skill to keep the published Swift reference guides current.

## Workflow

1. Read `references/scan-manifest.md` to see which sources and files to review.
2. Check official Swift, Swift Package Manager, and SwiftLint documentation for changes relevant to:
   - language guidance
   - concurrency guidance
   - package manager workflows
   - testing expectations
   - common lint rules or configuration guidance
3. Update only the reference files that actually changed.
4. Keep edits concise and practical. Prefer updating guidance over expanding scope.
5. Verify that `swift-expert-skill/SKILL.md` still points to the right reference files.

## Output

- Updated reference markdown files under `swift-expert-skill/references/`
- Any matching adjustments needed in `swift-expert-skill/SKILL.md`
