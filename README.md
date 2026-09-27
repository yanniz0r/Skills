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

### First-time setup in a target repo

Add this repo as a git submodule under `.claude/skills/`:

```sh
git submodule add https://github.com/yanniz0r/Skills.git .claude/skills/personal
git commit -m "Add personal skills submodule"
```

`git submodule add` already runs the initial checkout, so no separate `init`/`update` step is needed on first setup. This creates/updates `.gitmodules` and stages both it and the submodule pointer — commit them together.

Claude Code discovers every `SKILL.md` under `.claude/skills/`, so all skills in this collection become available immediately in that project. Skills that only make sense in one repo can still live alongside `personal/` as ordinary (non-submodule) entries in `.claude/skills/`.

### Cloning a repo that already has this submodule

Submodules aren't checked out by a plain `git clone`. Either clone recursively:

```sh
git clone --recurse-submodules <target-repo-url>
```

or, if already cloned without that flag:

```sh
git submodule update --init --recursive
```

### Pulling in updates later

```sh
git submodule update --remote .claude/skills/personal
git add .claude/skills/personal
git commit -m "Update personal skills"
```

This fast-forwards the submodule to the latest commit on its default branch and records the new pointer — commit that pointer change so other clones pick it up on their next `submodule update`.

## Adding a new skill

Use the `skill-creator` skill to scaffold and iterate on new skills — it handles the SKILL.md frontmatter, structure, and description tuning for good triggering. See [TEMPLATE.md](TEMPLATE.md) for the minimal shape a skill folder should have.
