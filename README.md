# pi-context-skills

A Pi coding agent extension that keeps skill context small by selecting only the skills relevant to the current project.

## Features

- Discovers project-local, user, Claude, and custom skills
- Uses compact project context (dir tree, README etc.) to select using default model relevant skills on first run
- Falls back to local heuristics when no model/auth is available
- Stores per-project selections in `.pi/skills-selection.json`
- Injects only enabled skills into the agent system prompt
- Provides `/skills` commands to list, edit, and reset selections
- Shows selection status with a `[Context-Skills]` UI header

## Installation

Install as a Pi package:

```text
/add @sean_pedersen/pi-context-skills
```

Or install directly from GitHub:

```text
/add https://github.com/SeanPedersen/pi-context-skills
```

## Usage

On first launch in a project, the extension discovers available skills and selects a relevant subset. The selected skills are saved to:

```text
.pi/skills-selection.json
```

The extension then replaces Pi's default skill section with only the enabled skills for that project.

## Commands

```text
/skills          Edit this project's skill selection
/skills edit     Edit this project's skill selection
/skills list     Show selected and available skills
/skills reset    Re-run skill selection for this project
```

## Skill discovery

Skills are discovered from:

- `<project>/.claude/skills`
- `~/.agents/skills`
- `~/.claude/skills`
- Paths listed in `PI_SKILL_PATHS`

`PI_SKILL_PATHS` uses the platform path delimiter (`:` on macOS/Linux, `;` on Windows).

## Selection behavior

The extension asks the active Pi model to select relevant skills using compact context from:

- top-level project file list
- `README.md` or `README`
- `package.json`
- `pyproject.toml`

If model selection is unavailable, it uses conservative heuristics and always enables project-local skills.

## License

MIT
