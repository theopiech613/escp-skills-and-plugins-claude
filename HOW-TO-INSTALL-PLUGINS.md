# How to install a Claude plugin from GitHub

A plugin is installed in two steps: first add the GitHub repo as a **marketplace**
(a catalogue of plugins), then **install** a plugin from that marketplace.

## 0. Check that the repo really is a Claude plugin

Open the GitHub page and look for a folder called `.claude-plugin` containing
`marketplace.json`. Most plugin READMEs also show the exact install commands
(usually in a section called "Install — Claude Code").

From `marketplace.json` you need two names:

- the marketplace name: the top-level `"name"`
- the plugin name: the `"name"` inside `"plugins"`

## 1. Add the marketplace (once per GitHub repo)

Use `owner/repo` from the GitHub link:
`https://github.com/williamtsoi1/google-cloud-slides-skill` → `williamtsoi1/google-cloud-slides-skill`

In a Claude Code chat:

```
/plugin marketplace add williamtsoi1/google-cloud-slides-skill
```

Or in the Mac Terminal:

```bash
claude plugin marketplace add williamtsoi1/google-cloud-slides-skill
```

## 2. Install the plugin

Format: `plugin-name@marketplace-name`

```
/plugin install google-cloud-slides@google-cloud-slides
```

Terminal version:

```bash
claude plugin install google-cloud-slides@google-cloud-slides
```

## 3. Check it worked

```bash
claude plugin list
```

Then **start a new Claude session**. A plugin's skills only load when a session starts.

## Useful extra commands

| What | Command |
|---|---|
| See installed plugins | `claude plugin list` |
| See added marketplaces | `claude plugin marketplace list` |
| Get the newest version | `claude plugin marketplace update <marketplace-name>` |
| Turn a plugin off | `claude plugin disable <plugin>@<marketplace>` |
| Remove a plugin | `claude plugin uninstall <plugin>@<marketplace>` |

## When the repo is NOT a plugin (plain skills)

Some repos have no `.claude-plugin` folder, only folders that each contain a
`SKILL.md` (example: `zbsaygin/econ-skills`). Those are installed by putting
each skill folder into `~/.claude/skills/`:

```bash
# 1. Download the repo to a permanent place
git clone https://github.com/zbsaygin/econ-skills.git ~/.claude/econ-skills

# 2. Link each skill folder into your skills folder (one line per skill)
ln -s ~/.claude/econ-skills/read-paper ~/.claude/skills/read-paper
```

Check first that no skill in `~/.claude/skills` already has the same name
(`ls ~/.claude/skills`). Also read the README: some skills have placeholders
like `<AUTHOR_NAME>` you must fill in.

To update later: `cd ~/.claude/econ-skills && git pull`

## Safety

Plugins can run code on your computer. Only install plugins from people or
sources you trust, and skim the README and files on GitHub first.

## Note: "command not found: claude"

The `claude` command only works in Terminal if Claude Code's command-line tool
is installed. Without it, use the `/plugin ...` commands in a Claude chat
instead, or ask Claude to run the install for you.
