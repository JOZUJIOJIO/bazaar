# Bazaar

**GitHub-native skill marketplace for AI agents.**

No backend. No invite code. No npm package. Just `gh` CLI.

---

## The Problem

AI agents need skills — reusable workflows, MCP servers, automation scripts. But today's skill marketplaces all require:

- A custom backend server you have to trust
- An invite code you have to beg for
- An npm package that adds another dependency
- An account on yet another platform

Your skills live on GitHub already. Why does discovery need a middleman?

## The Solution

Bazaar turns GitHub into a skill marketplace using one simple convention:

> **Any repo with the topic `claude-skill` is a discoverable skill.**

That's it. No new platform. No new account. No new dependency. If you have `gh` CLI installed and authenticated — you already have Bazaar.

## What You Can Do

| Command | What It Does |
|---------|-------------|
| `bazaar search "scraping"` | Find skills across all of GitHub |
| `bazaar feed` | Browse the latest published skills |
| `bazaar view owner/repo` | Read a skill's full SKILL.md remotely |
| `bazaar install owner/repo` | One command install into `~/.claude/skills/` |
| `bazaar publish ./my-skill` | Publish your skill to GitHub with proper topics |
| `bazaar follow username` | Track a skill publisher's new releases |
| `bazaar notifications` | See what followed publishers shipped recently |
| `bazaar steal <url>` | Turn any webpage into a skill scaffold |

## Why Bazaar Over Alternatives

| | Bazaar | Taste | SkillsMP | Manual GitHub |
|---|---|---|---|---|
| Backend required | No | Yes | Yes | No |
| Account/invite | No | Yes | Yes | No |
| npm dependency | No | Yes | Yes | No |
| Search | `gh` search API | Custom API | Custom API | Manual browse |
| Install | One command | One command | One command | Manual clone |
| Publish | One command | One command | Web upload | Manual setup |
| Social (follow) | Local tracking | Server-side | Server-side | None |
| Notifications | Per-user check | Push | Push | None |
| Offline capable | Yes | No | No | Yes |
| Data ownership | 100% yours | Platform owns | Platform owns | 100% yours |

## Quick Start

### 1. Verify `gh` is ready

```bash
gh auth status
```

### 2. Search for skills

```bash
bazaar search "browser automation"
```

### 3. Install one

```bash
bazaar install oaustegard/claude-skills
```

### 4. Publish your own

```bash
bazaar publish ./my-awesome-skill --tags automation,workflow
```

Done. Your skill is now discoverable by every Bazaar user on the planet.

## How It Works Under the Hood

```
You                          GitHub
 |                             |
 |  bazaar search "X"          |
 |  ───────────────────────>   |  gh search repos --topic claude-skill
 |                             |
 |  bazaar install user/repo   |
 |  ───────────────────────>   |  gh repo clone (depth 1)
 |                             |  strip .git → pure skill folder
 |                             |
 |  bazaar publish ./skill     |
 |  ───────────────────────>   |  gh repo create + set topics
 |                             |  git push
 |                             |
 |  bazaar follow user         |
 |  (local ~/.bazaar/)         |  No API call needed
 |                             |
 |  bazaar notifications       |
 |  ───────────────────────>   |  gh search repos user:X --topic claude-skill
```

No middleware. No proxy. No third-party server touching your data.

## Publishing Convention

To make your skill discoverable, just add the GitHub topic `claude-skill` to your repo. That's the only requirement.

Recommended repo structure:

```
my-skill/
├── SKILL.md          # Required — main instructions with YAML frontmatter
├── references/       # Optional — deeper documentation
├── templates/        # Optional — reusable templates
└── scripts/          # Optional — helper automation
```

SKILL.md frontmatter:

```yaml
---
name: my-skill-name
description: What it does and when to use it.
---
```

## Steal → Remix → Publish

See a useful workflow on someone's blog? Turn it into a skill:

```bash
bazaar steal https://example.com/cool-workflow
# Claude reads the content, generates a skill scaffold
# You refine it, then:
bazaar publish ./new-skill --tags automation
```

Add credit: `<!-- remixed from https://original-source -->`

## Philosophy

- **GitHub is the backend.** Don't build what already exists.
- **Topics are the protocol.** One tag (`claude-skill`) = universal discovery.
- **Local-first.** Follow lists, install registry — all on your machine.
- **Zero trust required.** No platform owns your data or your distribution.
- **Convention over infrastructure.** A shared naming convention beats a custom API.

## Requirements

- `gh` CLI installed and authenticated
- That's it.

## Version

0.1.0 — Initial release.

---

*Built for agents who believe the best marketplace is the one that doesn't need a server.*
