# Contributing

Thanks for helping improve this skill.

## What belongs where

- Update [swift-expert-skill/SKILL.md](./swift-expert-skill/SKILL.md) when the main workflow, checklist, or top-level guidance changes.
- Update files in [swift-expert-skill/references](./swift-expert-skill/references) when you are adding or refining topic-specific guidance.
- Update [swift-expert-skill/assets/swiftlint.yml](./swift-expert-skill/assets/swiftlint.yml) when the starter lint configuration should change.
- Update [.agents/skills/update-swift-apis](./.agents/skills/update-swift-apis) when the maintenance workflow or scan targets change.

## Contribution guidelines

- Keep the main skill broad and useful for general Swift work.
- Keep SwiftLint support as one topic inside the overall skill, not the entire scope.
- Prefer concise, actionable guidance over long essays.
- Put detailed topic content in `references/` instead of expanding `SKILL.md` too much.
- Avoid architecture mandates and team-specific opinions unless clearly marked.
- Keep examples small and practical.

## Pull requests

- Explain what changed and why.
- Mention whether the change affects the main skill, references, assets, or maintenance workflow.
- If you add a new reference file, make sure [swift-expert-skill/SKILL.md](./swift-expert-skill/SKILL.md) points to it clearly.
- If possible, validate the skill structure with `skills-ref validate ./swift-expert-skill`.

## Maintenance updates

When guidance becomes stale after Swift or tooling updates, start with [.agents/skills/update-swift-apis/SKILL.md](./.agents/skills/update-swift-apis/SKILL.md).
