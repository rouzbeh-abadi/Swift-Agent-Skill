# Agent Guidelines for Swift Expert Skill

This document guides AI agents working with this repository so the published skill stays broad, practical, and trustworthy for real Swift development work.

## Core Principles

### 1. Broad Swift Scope
**This is a general Swift skill, not a single-topic skill.** Cover:
- core Swift language patterns
- optionals, errors, and API design
- Swift concurrency
- Swift Package Manager workflows
- testing guidance
- SwiftLint and formatting support

Do not narrow the skill to only:
- SwiftLint
- SwiftUI
- one architecture style
- one team-specific coding convention

### 2. Prefer Standard Swift Guidance
**Use common Swift and Apple ecosystem practices.** Prioritize:
- language clarity
- safe and idiomatic APIs
- maintainable concurrency patterns
- readable package and test setup
- widely used lint and formatting conventions

Avoid inventing custom rules unless the user explicitly wants opinionated team standards.

### 3. Facts First, Opinions Second
**Lead with correctness and maintainability.** Use strong language for:
- unsafe patterns like `!` or `as!`
- concurrency misuse
- weak error handling
- obviously brittle package configuration

Use softer language for:
- naming nuance
- file organization
- access control preferences
- style choices where teams reasonably differ

### 4. Safe Edits First
**Prefer low-risk improvements before deeper refactors.** Good candidates:
- mechanical formatting cleanup
- redundant syntax removal
- `isEmpty` and boolean simplifications
- safer optional handling
- small package manifest cleanups
- focused test additions around touched behavior

Use more care with:
- public API changes
- cross-module renames
- concurrency model changes
- sweeping architecture rewrites

## Content Guidelines

### Include These Topics
- common Swift language pitfalls and modern idioms
- protocol and type design guidance
- error handling and optional handling
- structured concurrency patterns
- package manifests and dependency usage
- unit testing and test readability
- SwiftLint-backed formatting and linting guidance

### Avoid These Topics
- mandating MVVM, VIPER, TCA, or any other architecture
- prescribing a single folder layout
- framework-specific UI guidance unless the user asks for it
- tool walkthroughs that depend on a particular IDE
- style rules presented as universal law when they are team preferences

## Language and Tone

Use direct, practical wording:
- "Prefer X because it is safer or clearer in Swift."
- "Avoid X unless the invariant is explicit and documented."
- "Use the lint guide for mechanical cleanup, then apply judgment for API design and concurrency."

Avoid overclaiming:
- do not present style preference as compiler truth
- do not assume every project uses SwiftLint
- do not let one subtopic dominate the entire skill

## Repository Maintenance

This repository includes a maintenance skill for refreshing reference material:

- **`.agents/skills/update-swift-apis/SKILL.md`** — Review official Swift, Swift Package Manager, and SwiftLint sources, then update the reference guides when language or tooling guidance changes.

## Updating the Skill

When adding or changing guidance, ask:
1. Is this broadly useful to Swift developers?
2. Is it specific enough to help, without being overly opinionated?
3. Does it fit under the main Swift skill rather than needing its own skill?
4. Should this live in `SKILL.md` or a focused file in `references/`?

If the content is detailed or topic-specific, prefer a focused reference file.
