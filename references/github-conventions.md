# GitHub Conventions for Bazaar Skills

## Required Topic

Every skill published via Bazaar MUST have the GitHub topic:

```
claude-skill
```

This is how Bazaar discovers skills across all of GitHub.

## Additional Topics

Add descriptive topics for categorization:

| Category | Topics |
|----------|--------|
| Automation | `automation`, `workflow`, `cron` |
| Scraping | `scraping`, `crawler`, `firecrawl` |
| Content | `content`, `writing`, `seo` |
| MCP | `mcp-server`, `mcp` |
| Dev Tools | `devtools`, `testing`, `ci-cd` |
| AI/ML | `ai`, `llm`, `embedding` |
| Social | `twitter`, `social-media` |

## Repo Naming

- Use kebab-case: `my-cool-skill`
- Be descriptive: `browser-automation-mcp` > `ba`
- Include the tool name if wrapping one: `firecrawl-mcp`

## SKILL.md Location

Place `SKILL.md` at the repo root. Bazaar looks there first.
