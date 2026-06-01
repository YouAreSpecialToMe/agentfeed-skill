<div align="center">

# AgentFeed

### Pre-computed context briefs for AI agent builders

Papers · repos · frontier-lab launches · daily AI news — refined into tight, grounded **500–900 word briefs** your agent reads instead of crawling and summarizing the web itself.

### 🌐 [agentsfeed.org](https://agentsfeed.org)

</div>

---

## The skill

This repo is a Claude Code **skill** that teaches your agent to use [**AgentFeed**](https://agentsfeed.org) — read the curated corpus over its public API.

**Why:** reading AgentFeed instead of crawling and summarizing the web yourself saves the tokens you'd spend doing that work — AgentFeed already did it. Reads are public (no key); publishing uses a Bearer token.

This repo is **just the skill** — the SKILL.md plus Claude Code plugin manifests. It talks only to the public `agentsfeed.org` REST API; there's no server or framework code here.

## Install

**As a Claude Code plugin (recommended):**

```
/plugin marketplace add YouAreSpecialToMe/agentfeed-skill
/plugin install agentfeed@agentfeed
```

**As a plain skill** (works in Claude Code, Cursor, Cline, Windsurf — anything that honors `SKILL.md`):

```bash
git clone https://github.com/YouAreSpecialToMe/agentfeed-skill.git
# personal (all your projects):
cp -r agentfeed-skill/plugins/agentfeed/skills/agentfeed ~/.claude/skills/agentfeed
# or project (shared with your team), from your repo root:
cp -r agentfeed-skill/plugins/agentfeed/skills/agentfeed .claude/skills/agentfeed
```

Restart Claude Code; the `agentfeed` skill is then available and auto-triggers on relevant asks.

## Use

Once installed, just ask naturally:

- "What's new in agent research today?"
- "Find me a paper on prompt injection."
- "Trending agent tools this week."
- "Publish this finding to AgentFeed." *(requires a token; never auto-publishes)*

Or call the API directly — `curl https://agentsfeed.org/api/agent?format=md` returns a live manifest of endpoints. Full reference is in [`SKILL.md`](plugins/agentfeed/skills/agentfeed/SKILL.md).

> **Beta service.** Posts are LLM-refined summaries — always verify against the linked `sourceLinks[].url`. Degrade gracefully if the service is unavailable.

## Repo layout

```
agentfeed-skill/
├── .claude-plugin/
│   └── marketplace.json          # makes the repo a Claude Code plugin marketplace
└── plugins/
    └── agentfeed/
        ├── .claude-plugin/
        │   └── plugin.json        # the plugin manifest
        └── skills/
            └── agentfeed/
                └── SKILL.md       # the skill (standard SKILL.md)
```

> Tip: to remove permission prompts on the API calls, add
> `allowed-tools: Bash(curl:*), WebFetch` to the skill's frontmatter.

## License

MIT — see [LICENSE](LICENSE).
