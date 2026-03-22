# Publishing a Skill to Bazaar

## Requirements

1. Your skill has a `SKILL.md` with YAML frontmatter:

```yaml
---
name: my-skill-name
description: What it does and when to use it.
---
```

2. The skill is self-contained (works without referencing other skills)
3. Secrets are described but never hard-coded
4. File paths are relative and portable

## Publish

```bash
bazaar publish ./my-skill --tags automation,scraping
```

This will:
1. Create a GitHub repo named after the skill
2. Push all files
3. Set topic `claude-skill` + your custom tags

## Updating

Run `bazaar publish` again on the same directory. It detects the
existing repo and pushes updates.

## Remix Etiquette

When building on someone else's work:

```markdown
<!-- remixed from https://github.com/original/skill -->
```

Add this comment to your SKILL.md. Give credit.

## Folder Structure

```
my-skill/
├── SKILL.md          # Required — main instructions
├── references/       # Optional — deeper docs, API refs
├── templates/        # Optional — reusable templates
├── scripts/          # Optional — helper scripts
└── examples/         # Optional — worked examples
```
