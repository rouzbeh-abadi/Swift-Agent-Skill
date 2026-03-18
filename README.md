# Swift Agent Skill

A publishable Agent Skills repository for broad Swift development guidance, with focused references for SwiftLint, concurrency, package management, testing, and everyday language best practices.

Repository: [rouzbeh-abadi/Swift-Agent-Skill](https://github.com/rouzbeh-abadi/Swift-Agent-Skill)

## Included skill

- `swift-expert-skill` — Use when writing, reviewing, refactoring, or maintaining Swift code across app, package, and library projects.

## Who this is for

- Swift developers who want an AI agent to reason about real Swift code, not just formatting
- Teams using Swift Package Manager, tests, and concurrency in everyday development
- Anyone who wants SwiftLint support as part of a broader Swift engineering skill

## How to Use This Skill

### Option A: Manual install

1. Clone this repository:

```bash
git clone https://github.com/rouzbeh-abadi/Swift-Agent-Skill.git
```

2. Install or symlink the `swift-expert-skill/` folder into your tool's skills location.
3. Ask your coding agent to use the `swift-expert-skill` for Swift work.

Example prompt:

> Use the swift expert skill and review this Swift package for concurrency, testing gaps, and SwiftLint issues.

### Option B: Claude Code Plugin

#### Personal Usage
To install this skill for your personal use in Claude Code:

1. Add the marketplace:

```bash
/plugin marketplace add rouzbeh-abadi/Swift-Agent-Skill
```

2. Install the skill:

```bash
/plugin install swift-expert@swift-expert-skill
```

### Option C: Cursor plugin (coming soon)

This repository is now packaged for Cursor plugin submission, but the marketplace listing is not live yet.

### Option D: Codex / OpenAI-compatible tools

This repository includes an `agents/openai.yaml` manifest. Copy or symlink the `swift-expert-skill/` folder into your Codex skills directory:

```bash
cp -R swift-expert-skill/ "$CODEX_HOME/skills/swift-expert-skill"
```

See [Codex skills documentation](https://developers.openai.com/codex/skills/) for details on where to save skills.

### How to verify

Your agent should reference [SKILL.md](./swift-expert-skill/SKILL.md) and then pull in the relevant files from [references](./swift-expert-skill/references) for the task at hand.

## What it covers

- Swift language patterns and API design
- optionals and error handling
- Swift concurrency
- Swift Package Manager
- testing guidance
- SwiftLint and code style support

## What's Inside

This skill is meant to stay broad enough for day-to-day Swift engineering work while still being compact enough for agents to load efficiently. The main skill gives the workflow and review checklist, and the topic-specific references provide the deeper guidance only when needed.

- **Language patterns** — optionals, errors, API design, mutability, and control flow
- **Concurrency** — structured concurrency, task ownership, isolation, and cancellation
- **Swift Package Manager** — `Package.swift`, targets, dependencies, and package hygiene
- **Testing** — practical review guidance for unit and async tests
- **SwiftLint support** — formatting, common lint rules, and safe mechanical cleanup
- **Starter assets** — a baseline SwiftLint config you can adapt per project

## Repository layout

```text
swift-expert-skill/
  SKILL.md
  references/
    swift-language-patterns.md
    swift-concurrency-guide.md
    swift-package-manager-guide.md
    swift-testing-guide.md
    swift-style-and-lint-guide.md
  assets/
    swiftlint.yml
agents/
  openai.yaml
.claude-plugin/
  plugin.json
  marketplace.json
.cursor-plugin/
  plugin.json
assets/
  logo.svg
```

## Skill Structure

- [swift-expert-skill/SKILL.md](./swift-expert-skill/SKILL.md) - Main workflow, guidance, and review checklist
- [swift-expert-skill/references/swift-language-patterns.md](./swift-expert-skill/references/swift-language-patterns.md) - Core Swift language guidance
- [swift-expert-skill/references/swift-concurrency-guide.md](./swift-expert-skill/references/swift-concurrency-guide.md) - Async and concurrency guidance
- [swift-expert-skill/references/swift-package-manager-guide.md](./swift-expert-skill/references/swift-package-manager-guide.md) - Package and target structure guidance
- [swift-expert-skill/references/swift-testing-guide.md](./swift-expert-skill/references/swift-testing-guide.md) - Test review and implementation guidance
- [swift-expert-skill/references/swift-style-and-lint-guide.md](./swift-expert-skill/references/swift-style-and-lint-guide.md) - SwiftLint-aligned style and lint guidance
- [swift-expert-skill/assets/swiftlint.yml](./swift-expert-skill/assets/swiftlint.yml) - Starter SwiftLint configuration
- [agents/openai.yaml](./agents/openai.yaml) - OpenAI-compatible manifest for Codex and related tools
- [.claude-plugin/plugin.json](./.claude-plugin/plugin.json) - Claude plugin metadata
- [.claude-plugin/marketplace.json](./.claude-plugin/marketplace.json) - Claude marketplace metadata
- [.cursor-plugin/plugin.json](./.cursor-plugin/plugin.json) - Cursor plugin metadata
- [assets/logo.svg](./assets/logo.svg) - Decorative plugin icon asset

## Maintenance

The repository includes a maintenance skill for refreshing the reference material:

```text
.agents/skills/update-swift-apis/
  SKILL.md
  references/
    scan-manifest.md
```

Use [update-swift-apis/SKILL.md](./.agents/skills/update-swift-apis/SKILL.md) when Swift, Swift Package Manager, or SwiftLint guidance changes and you want to refresh the repository references before a release.

Note: only `swift-expert-skill` is intended to be published in the Cursor plugin. The maintenance skill remains a repository workflow utility.

## Contributing

Contributions are welcome. This repository follows the [Agent Skills open format](https://agentskills.io/home), so structure and file placement matter.

Please read [CONTRIBUTING.md](./CONTRIBUTING.md) for:

- what to change in `SKILL.md` versus `references/`
- how to keep additions concise and publish-friendly
- expectations for pull requests and review quality

## Installation Notes

Install or symlink the `swift-expert-skill/` folder into a skills-compatible location such as:

- `<project>/.agents/skills/`
- `~/.agents/skills/`

The Agent Skills specification and discovery conventions are documented at [agentskills.io/specification](https://agentskills.io/specification) and [agentskills.io/client-implementation/adding-skills-support](https://agentskills.io/client-implementation/adding-skills-support).

Popular tool docs:

- Codex: [Where to save skills](https://developers.openai.com/codex/skills/#where-to-save-skills)
- Claude: [Using Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview#using-skills)
- Cursor: [Plugins documentation](https://cursor.com/docs/plugins)
- Cursor: [Enabling Skills](https://cursor.com/docs/context/skills#enabling-skills)

## Validation

If you have the reference validator installed, validate the skill with:

```bash
skills-ref validate ./swift-expert-skill
```

## Acknowledgments

This repository was shaped by a few strong sources and examples:

- [SwiftUI-Agent-Skill](https://github.com/AvdLee/SwiftUI-Agent-Skill) by [Antoine van der Lee](https://github.com/AvdLee), which helped set the reference structure and publishable repository pattern
- The [Agent Skills open format](https://agentskills.io/home), which defines the portable structure used by this repository
- The official [OpenAI Codex skills documentation](https://developers.openai.com/codex/skills/), which informs the Codex usage guidance in this README
- The Swift and Swift Package Manager ecosystems, whose documentation and conventions inform the skill content
- [SwiftLint](https://github.com/realm/SwiftLint), whose rule set and common usage patterns inform the linting guidance and starter config

## License

This repository is available under the MIT License. See [LICENSE](./LICENSE) for details.
