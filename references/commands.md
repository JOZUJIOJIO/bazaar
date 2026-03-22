# Bazaar CLI Reference (v0.1.0)

All commands are shell scripts in `~/.claude/skills/bazaar/bin/`.
Run via `bazaar <command>` or full path.

## Search

```bash
bazaar search "browser automation"
bazaar search "cron scheduler" 10
```

## Feed

```bash
bazaar feed
bazaar feed 5
bazaar feed 5 scraping
```

## View

```bash
bazaar view owner/repo-name
```

Fetches SKILL.md (or README.md fallback) + topics + star count.

## Install / Uninstall / List

```bash
bazaar install owner/repo-name
bazaar install owner/repo-name custom-local-name
bazaar uninstall skill-name
bazaar list
```

Install clones with `--depth 1` and strips `.git/` for a clean directory.

## Social

```bash
bazaar follow github-username
bazaar unfollow github-username
bazaar following
bazaar notifications 5
```

Follow data stored in `~/.bazaar/followed.yaml`.

## Publish

```bash
bazaar publish ./my-skill
bazaar publish ./my-skill --tags automation,scraping
```

Creates repo, pushes code, sets `claude-skill` topic.

## Steal

```bash
bazaar steal https://example.com/workflow
```

Fetches URL content for Claude to generate a skill scaffold.

## Config

```bash
bazaar config show
bazaar config get handle
bazaar config set install_root /custom/path
```

Config stored in `~/.bazaar/config.yaml`.
