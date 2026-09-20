# Using this repo with pi coding agent

The Karpathy-inspired guidelines work with [pi coding agent](https://github.com/badlogic/pi) two ways: automatically via `CLAUDE.md`, and as a reusable Agent Skill.

## Automatic, project-local guidelines

Pi reads `AGENTS.md` or `CLAUDE.md` from the project root (and ancestor directories) at startup and adds them to the system prompt. This repo already commits [`CLAUDE.md`](CLAUDE.md), so pi picks it up automatically whenever you run it inside this repo — no setup needed.

To use the same guidelines in another project, copy `CLAUDE.md` into that project's root (or merge it into an existing `AGENTS.md`/`CLAUDE.md`).

## Reusable Agent Skill

Pi implements the [Agent Skills standard](https://agentskills.io/specification) natively, and [`skills/karpathy-guidelines/SKILL.md`](skills/karpathy-guidelines/SKILL.md) already conforms to it — no adaptation was needed. You just need to put it (or point pi at it) somewhere pi looks for skills.

**Personal, all projects:**
```bash
mkdir -p ~/.pi/agent/skills
ln -s "$(pwd)/skills/karpathy-guidelines" ~/.pi/agent/skills/karpathy-guidelines
```

**Single project** (place in `.pi/skills/`, loads once the project is trusted):
```bash
mkdir -p .pi/skills
cp -r /path/to/pi-skills/skills/karpathy-guidelines .pi/skills/
```

**Without copying**, reference the path in `.pi/settings.json` (project) or `~/.pi/agent/settings.json` (global):
```json
{
  "skills": ["/path/to/pi-skills/skills/karpathy-guidelines"]
}
```

**One-off, via CLI flag:**
```bash
pi --skill /path/to/pi-skills/skills/karpathy-guidelines
```

**As a pi package** (this repo ships a `package.json` with a `pi.skills` manifest, so pi's package manager can install it directly — either globally or with `-l` for project-local):
```bash
pi install /path/to/pi-skills          # local checkout
pi install git:github.com/<owner>/pi-skills
```

## Forcing the skill to load

Pi loads only the skill's name and description into the system prompt by default and decides on its own whether to read the full `SKILL.md`. To force it for a turn, run:
```
/skill:karpathy-guidelines
```

## Claude Code vs Cursor vs pi

- **Claude Code:** plugin marketplace, or `CLAUDE.md`.
- **Cursor:** committed `.cursor/rules/karpathy-guidelines.mdc` (`alwaysApply: true`).
- **pi:** `CLAUDE.md` is read automatically, same as Claude Code; the Agent Skill also works out of the box since pi implements the same Agent Skills spec — see install options above.

## For contributors

When you change the four principles, keep [`CLAUDE.md`](CLAUDE.md), [`.cursor/rules/karpathy-guidelines.mdc`](.cursor/rules/karpathy-guidelines.mdc), and [`skills/karpathy-guidelines/SKILL.md`](skills/karpathy-guidelines/SKILL.md) in sync.
