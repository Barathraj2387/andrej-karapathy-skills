# Using this repo with OpenCode

[OpenCode](https://opencode.ai) loads instruction files and skills natively, so the guidelines need no plugin or marketplace.

## In this repository

1. Open the folder in OpenCode.
2. [`AGENTS.md`](AGENTS.md) is committed at the repository root, so the guidelines are loaded as project instructions automatically. There is nothing to install.
3. To get the skill itself in this repository as well, point OpenCode at the checkout with the `skills` array described below.

## Use the same guidelines in another project

OpenCode discovers skills from `.opencode/skills/<skill-id>/SKILL.md` (one project) and `~/.config/opencode/skills/<skill-id>/SKILL.md` (every project), with no configuration.

**Per project:**

```bash
mkdir -p .opencode/skills
cp -r skills/karpathy-guidelines .opencode/skills/
```

**Globally:**

```bash
mkdir -p ~/.config/opencode/skills
cp -r skills/karpathy-guidelines ~/.config/opencode/skills/
```

**Without copying anything** — add the checkout's `skills` directory to the `skills` array in `opencode.jsonc`:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["/absolute/path/to/andrej-karpathy-skills/skills"]
}
```

On Windows, `~/.config/opencode` is `C:\Users\<you>\.config\opencode`.

## Apply the guidelines to every model automatically

OpenCode advertises a skill to the model by its description and loads the body on demand, so whether it gets applied depends on the model choosing to load it.

To have the four principles apply to **every** model in **every** session without that step, install `AGENTS.md` as a global instruction file:

```bash
mkdir -p ~/.config/opencode
curl -o ~/.config/opencode/AGENTS.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/AGENTS.md
```

`~/.config/opencode/AGENTS.md` is loaded into the system prompt of every session, regardless of which model is selected. Use it alongside the skill rather than instead of it: the instruction file guarantees the rules are visible, and the skill carries the longer rationale.

To merge into instructions you already have:

```bash
echo "" >> ~/.config/opencode/AGENTS.md
curl https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/AGENTS.md >> ~/.config/opencode/AGENTS.md
```

## Loading the skill manually

OpenCode lists the ID, name, and description of each skill, then loads the body through its `skill` tool. To load it explicitly, mention it in your prompt:

```
use skill tool to load karpathy-guidelines
```

## Claude Code, Cursor, and OpenCode

| Tool | Applies automatically | Manual install |
|---|---|---|
| **Claude Code** | Plugin from the marketplace | `/plugin marketplace add forrestchang/andrej-karpathy-skills` |
| **Cursor** | [`.cursor/rules/karpathy-guidelines.mdc`](.cursor/rules/karpathy-guidelines.mdc) with `alwaysApply: true` | Copy the rule into `.cursor/rules/` |
| **OpenCode** | [`AGENTS.md`](AGENTS.md) as project instructions | Copy `skills/karpathy-guidelines/` into `.opencode/skills/` |

OpenCode V2 recognizes `AGENTS.md` only; it does not fall back to `CLAUDE.md`. That is why this repository carries both files with the same content.

## For contributors

When you change the four principles, keep **[`CLAUDE.md`](CLAUDE.md)** and **[`AGENTS.md`](AGENTS.md)** in sync. If the published skill text should match, update **[`.cursor/rules/karpathy-guidelines.mdc`](.cursor/rules/karpathy-guidelines.mdc)** and **[`skills/karpathy-guidelines/SKILL.md`](skills/karpathy-guidelines/SKILL.md)** as well.
