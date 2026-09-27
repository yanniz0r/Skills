# Skills

Personal collection of [Claude Code](https://claude.com/claude-code) skills. Each skill lives in its own top-level folder containing a `SKILL.md`, so this repo can be dropped into any other project's `.claude/skills/` directory and picked up automatically.

## Layout

```
Skills/
  README.md
  TEMPLATE.md          # reference frontmatter/structure for a new skill (not a real skill itself)
  <skill-name>/
    SKILL.md
    ...supporting files (scripts, references, assets)
```

Each `<skill-name>/` folder is self-contained: everything the skill needs (helper scripts, reference docs, examples) lives inside it.

## Using these skills in another repo

Add this repo as a git submodule under `.claude/skills/` in the target project:

```sh
git submodule add https://github.com/<you>/Skills.git .claude/skills/personal
git submodule update --init --recursive
```

Claude Code discovers every `SKILL.md` under `.claude/skills/`, so all skills in this collection become available immediately in that project. Skills that only make sense in one repo can still live alongside `personal/` as ordinary (non-submodule) entries in `.claude/skills/`.

To pull in updates later:

```sh
git submodule update --remote .claude/skills/personal
```

## Adding a new skill

Use the `skill-creator` skill to scaffold and iterate on new skills — it handles the SKILL.md frontmatter, structure, and description tuning for good triggering. See [TEMPLATE.md](TEMPLATE.md) for the minimal shape a skill folder should have.
