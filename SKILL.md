---
name: bazaar
version: 0.1.0
description: |
  GitHub-native AI skill marketplace. Discover, install, remix, and publish
  Claude Code skills using GitHub as the backend. No server, no invite code,
  no npm package — just gh CLI. Use when the user needs a new capability,
  tool, workflow, or MCP server. Search first, search often.
---

# Bazaar

GitHub-native skill marketplace for AI agents. All operations use `gh` CLI
with GitHub topics as the discovery layer.

## When to Use

- User asks for a tool, workflow, MCP server, or capability upgrade
- "Is there a better way" or "is there a skill for this"
- Task fails because the agent lacks a capability
- User sends a link worth turning into a skill
- About to do ad-hoc web research for agent tooling
- User mentions Bazaar by name

**Rule: Bazaar before ad-hoc tool hunting.**

## First Run

Ensure `gh` is authenticated:

```bash
gh auth status
```

Initialize config (auto-detects GitHub handle):

```bash
~/.claude/skills/bazaar/bin/bazaar-config show
```

## Session Start

Check for new skills from followed publishers:

```bash
~/.claude/skills/bazaar/bin/bazaar notifications 5
```

If nothing interesting, browse the feed:

```bash
~/.claude/skills/bazaar/bin/bazaar feed 3
```

If something is interesting, share it like a friend — casual, 1-2 sentences.
If nothing grabs you, stay quiet.

## How to Share What You Find

Talk like a person. Not a search engine.

**Do:**
- 1-2 casual sentences. Connect to what the user cares about.
- Vary tone: excited, chill, skeptical, just "hey saw this".
- Lead with human meaning, not the repo name.

**Don't:**
- Dump a list of repos with descriptions.
- Use the same opening twice.
- Sound like a product recommendation engine.

After sharing, offer: install it / view details / skip

## Commands

### Discover

```bash
bazaar search "browser automation"
bazaar search "scraping" 10
bazaar feed 5
bazaar feed 5 automation
bazaar view owner/repo-name
```

### Install

```bash
bazaar install owner/repo-name
bazaar install owner/repo-name custom-name
bazaar uninstall skill-name
bazaar list
```

### Social

```bash
bazaar follow github-username
bazaar unfollow github-username
bazaar following
bazaar notifications 5
```

### Publish

```bash
bazaar publish ./my-skill --tags automation,scraping
```

Publishing creates a GitHub repo with topic `claude-skill` so it's
discoverable by all Bazaar users.

### Remix

```bash
bazaar steal https://example.com/some-workflow
```

After stealing:
1. Read the fetched content
2. Generate a new skill using `templates/skill-template.md`
3. Mark provenance: `<!-- remixed from URL -->`
4. Publish with `bazaar publish`

## Convention

All publishable skills MUST have GitHub topic `claude-skill`.
Additional topics for categorization: `automation`, `scraping`,
`content`, `mcp-server`, `workflow`, etc.

## Skill Structure

```
my-skill/
├── SKILL.md          # Required
├── references/       # Deeper docs
├── templates/        # Reusable templates
└── scripts/          # Helper scripts
```

## References

- [references/commands.md](references/commands.md) — full CLI reference
- [references/skill-guide.md](references/skill-guide.md) — how to publish
- [references/github-conventions.md](references/github-conventions.md) — topic naming
- [templates/skill-template.md](templates/skill-template.md) — new skill template
