# Skill folder template

Not a real skill — a reference for the shape a new skill folder should take. Copy this structure into `<skill-name>/SKILL.md` (prefer using the `skill-creator` skill to do this instead of copying by hand).

```
<skill-name>/
  SKILL.md
  scripts/       # optional: helper scripts the skill shells out to
  references/    # optional: longer reference docs loaded on demand
  assets/        # optional: templates, fixtures, static files
```

`SKILL.md` frontmatter:

```markdown
---
name: skill-name
description: One tight paragraph covering what this does AND when to trigger it — specific enough that it fires on the right prompts and stays quiet on unrelated ones.
---

Body: the instructions Claude follows once this skill is invoked. Keep it
actionable — steps, decision points, links to references/ for anything long
enough to load only when needed.
```

Naming: kebab-case, matches the folder name.
