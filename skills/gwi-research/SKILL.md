---
name: gwi-research
description: >
  Consumer audience research and insights using GWI (Global Web Index) data via
  the gwi_spark_ai MCP server. Use when the user asks about audience demographics,
  consumer behaviors, media consumption, social media usage, purchase drivers,
  brand perception, market sizing, audience profiling, competitive audience analysis,
  trend identification, or any consumer/market research question that can be answered
  with survey data. Also use when interpreting GWI results, formatting insight reports,
  or building audience segments. Triggers: audience research, consumer insights,
  market research, demographic analysis, media planning, brand health, audience profile,
  GWI query, consumer trends, digital behavior, purchase intent.
---

# GWI Research Skill

Use the `gwi_spark_ai` MCP server tools (`chat_gwi`, `explore_insight_gwi`) to query GWI's consumer insights database of 35B+ data points across 50+ markets.

## Quick Reference

### Available Tools

| Tool | Purpose |
|------|---------|
| `chat_gwi` | Ask questions about audiences, behaviors, preferences, trends |
| `explore_insight_gwi` | Drill deeper into a specific insight returned by `chat_gwi` |

### Prompt Formula

Every `chat_gwi` prompt must include:

1. **Audience** (who) - e.g., "Gen Z", "gamers aged 18-34", "EV owners"
2. **Topic** (what) - e.g., "social media usage", "purchase drivers", "media consumption"
3. **Location** (where) - e.g., "in the UK", "in Germany and France" (omit for global)
4. **Timeframe** (when) - e.g., "in 2024", "Q3 2024" (omit for latest 4 waves)

### Critical Rules

- **One question per call.** Never combine multiple questions in a single prompt.
- **First call: no `chat_id`.** Only include `chat_id` from a previous response for follow-ups.
- **US English only.** Say "soccer" not "football", "cell phone" not "mobile" to avoid ambiguity.
- **Trend questions: one year per call.** Break "How has X changed from 2020 to 2024?" into 5 separate calls (2020, 2021, 2022, 2023, 2024), using the same `chat_id`.
- **Core dataset only.** Agent Spark cannot access add-on datasets (Gaming, Zeitgeist, Travel, etc.) or custom studies.

## Workflow: Standard Audience Query

```
1. chat_gwi → Initial question (no chat_id)
2. chat_gwi → Follow-up to narrow/expand (with chat_id)
3. explore_insight_gwi → Deep dive on specific insight_id
4. Format findings for user (see references/output-formats.md)
```

## Workflow: Comparative Analysis

```
1. chat_gwi → "Compare [audience A] and [audience B] on [topic] in [location]"
2. chat_gwi → Follow-up on most interesting difference (with chat_id)
3. explore_insight_gwi → Statistical detail on key finding
4. Synthesize into comparison table with index scores
```

## Workflow: Trend Over Time

```
1. chat_gwi → "[topic] for [audience] in [location] in 2020"
2. chat_gwi → Same for 2021 (with chat_id)
3. chat_gwi → Same for 2022 (with chat_id)
4. chat_gwi → Same for 2023 (with chat_id)
5. chat_gwi → Same for 2024 (with chat_id)
6. Compile year-over-year narrative with direction indicators
```

## Workflow: Full Audience Profile

Build a complete audience portrait in sequential calls:

```
1. chat_gwi → Demographics (age, gender, income, education)
2. chat_gwi → Digital behaviors (devices, platforms, apps)
3. chat_gwi → Media consumption (channels, formats, time spent)
4. chat_gwi → Purchase drivers (motivations, brand preferences)
5. chat_gwi → Attitudes and interests (values, lifestyle, passions)
6. Synthesize into structured profile (see references/output-formats.md)
```

## Sample Prompts

**Audience profile:**
> "Tell me about PlayStation 5 owners in Japan"

**Comparison:**
> "Compare Gen X and Millennials reasons for using social media"

**Preference:**
> "Are people in the US aged 20 to 25 more likely to use TikTok or Instagram?"

**Feature analysis:**
> "What features increase the likelihood of buying a product for Millennial males?"

**Cross-audience:**
> "Tell me about EV owners that are also Formula E fans"

**Temporal:**
> "Tell me about Instagram Reel users in the UK in 2024"

## Data Interpretation Quick Guide

- **Index score > 100**: Over-indexes vs. general population (more likely)
- **Index score < 100**: Under-indexes (less likely)
- **Index > 120**: Notable over-index worth highlighting
- **Index > 150**: Strong signal, lead with this in findings
- **Sample size < 100**: Treat as directional only, caveat in output
- **Sample size 100-300**: Usable but flag as moderate confidence
- **Sample size > 300**: Robust, report with confidence

For detailed interpretation guidance, see [references/data-interpretation.md](references/data-interpretation.md).

## Formatting Findings

Match output format to use case:

| Use Case | Format |
|----------|--------|
| Quick lookup | 3-5 bullet points with key stats |
| Research report | Structured sections with tables and narrative |
| Strategy deck | Headline stat + supporting evidence + "so what" |
| Competitive analysis | Side-by-side comparison table |
| Audience profile | Persona card with demographic + behavioral layers |

For templates and examples, see [references/output-formats.md](references/output-formats.md).

## Error Handling

| Problem | Action |
|---------|--------|
| Low/no sample size | Broaden audience definition, add more markets, or expand timeframe |
| "No data available" | Check if question uses add-on data (not available); rephrase with Core-compatible terms |
| Unexpected results | Verify audience definition isn't too narrow; check if question is ambiguous |
| Contradictory data | Cross-reference with a second query; note the discrepancy and possible explanations |
| Rate limiting | Space out calls; batch related questions in the same chat session |

## GWI Data Coverage

- **Markets**: 50+ countries across EMEA, Americas, APAC
- **Respondents**: 1.4M+ annual surveys, representing 2.8B internet users
- **Age range**: 16-64 (GWI Core)
- **Frequency**: Quarterly (since 2013)
- **History**: 15+ years of data
- **Profiling points**: 250K+ covering demographics, interests, behaviors

## Reference Files

- **[references/query-patterns.md](references/query-patterns.md)**: Detailed query construction patterns, audience filters, common pitfalls, and advanced techniques
- **[references/data-interpretation.md](references/data-interpretation.md)**: How to read index scores, percentages, sample sizes, statistical significance, and cross-referencing with other sources
- **[references/output-formats.md](references/output-formats.md)**: Templates for research reports, persona cards, comparison tables, and executive summaries
