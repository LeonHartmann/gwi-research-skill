# GWI Research Skill for Claude Code

A Claude Code skill that adds consumer research expertise on top of the [GWI (Global Web Index)](https://www.gwi.com) MCP server. Makes anyone using Claude with GWI immediately more effective at pulling, interpreting, and presenting consumer insights.

## What It Does

This skill teaches Claude how to:

- **Query GWI effectively** — prompt construction patterns, audience definitions, follow-up strategies
- **Interpret results correctly** — index scores, percentages, sample sizes, statistical caveats
- **Format findings professionally** — persona cards, comparison tables, research reports, executive summaries
- **Avoid common pitfalls** — one question per call, trend splitting, US English, Core-only limitations

## Prerequisites

You need the GWI MCP server (`gwi_spark_ai`) configured in your Claude Code environment. This requires a GWI account with Spark API access.

## Installation

### Option A: Plugin Install

```bash
# Add the marketplace
/plugin marketplace add LeonHartmann/gwi-research-skill

# Install the skill
/plugin install gwi-research-skill
```

### Option B: Manual Copy

```bash
git clone https://github.com/LeonHartmann/gwi-research-skill.git
cp -r gwi-research-skill/skills/gwi-research ~/.claude/skills/
```

## Skill Contents

```
skills/gwi-research/
├── SKILL.md                          # Core skill — workflows, rules, quick reference
└── references/
    ├── query-patterns.md             # Query construction, 54 markets, audience filters
    ├── data-interpretation.md        # Index scores, 5 metrics, rebasing, caveats
    └── output-formats.md             # 7 templates (quick lookup → trend narrative)
```

## Triggers

The skill activates when you ask about: audience research, consumer insights, market research, demographic analysis, media planning, brand health, audience profiling, competitive audience analysis, trend identification, GWI queries, consumer trends, digital behavior, or purchase intent.

## Example Usage

```
"Tell me about esports viewers in Germany"
"Compare Gen X and Millennials on social media usage in the UK"
"What motivates eco-conscious consumers to purchase sustainable products?"
"Build me an audience profile of EV owners in the US"
```

## Research

See [RESEARCH.md](RESEARCH.md) for the full research notes that informed this skill, including GWI platform documentation, MCP server details, data interpretation methodology, and Claude Code skill best practices.

## License

MIT
