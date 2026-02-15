# GWI MCP Skill — Research Notes

Research conducted on 2026-02-15 to inform the creation of the `gwi-research` Claude Code skill.

## 1. GWI Platform Overview

### What is GWI?

GWI (Global Web Index) is a consumer research platform providing audience insights through large-scale online surveys. It offers structured consumer data — demographics, attitudes, behaviors, media consumption, purchase intent, and brand data — benchmarked against national averages.

**Key stats:**
- 2 million+ interviews conducted yearly (960K annual sample for Core)
- 35 billion total data points
- 54 markets covered (GWI Core)
- 57,000+ profiling points
- 5,000+ brands tracked
- 15+ years of trended insights (4 waves/quarters per year)
- Represents 3 billion internet users worldwide

### Data Structure

GWI organizes data in a three-tier hierarchy:

1. **Namespaces** — Top-level research domains (e.g., "Core", "Sports")
2. **Categories** — Grouped question areas within namespaces (e.g., "Demographics", "Media Consumption")
3. **Questions** — Individual data points (e.g., "What is your employment status?")

Full data structure reference: https://api.globalwebindex.com/docs/platform-api/getting-started/gwi-data-structure

### Datasets

| Dataset | Type | Frequency | Coverage |
|---------|------|-----------|----------|
| **GWI Core** | Flagship survey on digital attitudes & behaviors | Quarterly (since 2013) | 50+ markets |
| **GWI Zeitgeist** | Monthly survey on pressing topics | Monthly | Varies |
| **GWI Core Plus** | Additional categories/brands for specific markets | Semi-annual | Subset of markets |
| **Add-ons** (11) | Specialized topics | Varies | Varies |

**Full dataset breakdown:**

| Dataset | Markets | Annual Sample | Representation |
|---------|---------|---------------|----------------|
| **Core** | 54 | 960K | 3B internet users |
| **USA** | 50 states + DC | 80K | 250M internet users |
| **Gaming** | 18 | 65K | 1.8B gamers |
| **Sports** | 18 | 80K | 1.8B sports fans |
| **Kids** | 18 | 20K | Children 8-15 |
| **Travel** | 15 | 44K | N/A |
| **Work** | 19 | 30K | 940M+ professionals |
| **Alcohol** | 6 | 18K | 750M+ consumers |
| **Automotive** | 6 | 22.5K | 890M+ consumers |
| **Consumer Tech** | 9 | 15K | 430M+ consumers |
| **Luxury** | 5 | 13K | N/A |
| **Moments** | 2 | 8K | N/A |
| **Zeitgeist** | 11 | 12K per wave | Monthly topical |

**Important**: Agent Spark (MCP) only has access to **GWI Core** (and USA for eligible subscribers). Add-on datasets and custom studies are NOT available through the MCP integration.

### GWI Core Survey Components

The GWI Core survey has three integrated parts:

1. **Main Survey** — Completed by most respondents (35-50 minutes)
2. **Mobile Survey** — Optimized for smaller screens, slightly fewer questions
3. **Brand & Media Module** — Recontact survey with ~50% of main respondents, focused on brand engagement and media consumption

All three are combined into a single dataset on the platform.

### Core Question Categories (Known)

Based on available documentation, GWI Core covers:
- **Demographics**: Gender, gender identity, age, sexual orientation, ethnicity & nationality, education, location, household income, financial products, savings/investments, banks/financial institutions, household & family composition, employment status
- **Attitudes & Lifestyle**: Attitudes, brand & product preferences, brand relationships, character traits, future outlook, environmental consciousness
- **Device Ownership & Access**: Tablets, smartphones, computers, smart devices
- **Online Activities & Behaviors**: Internet usage, app usage, browsing behavior
- **Social Media**: Platform usage, engagement, content creation, social networking
- **Media Consumption**: TV channels, streaming, radio, print, podcasts, digital media
- **Commerce & Purchase Behavior**: Purchase drivers, buying habits, e-commerce, brand discovery
- **Brand Awareness & Sentiment**: 5,000+ brands tracked across sectors

Full questionnaire taxonomy is proprietary and only available within the GWI platform.

### Market Coverage

**EMEA**: Austria, Belgium, Denmark, Egypt, France, Germany, Ghana, Ireland, Israel, Italy, Kenya, Morocco, Netherlands, Nigeria, Norway, Poland, Portugal, Romania, Russia, Saudi Arabia, South Africa, Spain, Sweden, Switzerland, Turkey, UAE, UK

**Americas**: Argentina, Brazil, Canada, Chile, Colombia, Mexico, USA

**APAC**: Australia, China, Hong Kong, India, Indonesia, Japan, Malaysia, New Zealand, Philippines, Singapore, South Korea, Taiwan, Thailand, Vietnam

### Methodology

- Age range: 16-64 (GWI Core)
- Quotas set for age, gender, and education
- Surveys administered in respondents' local languages
- Answer options localized (e.g., brand lists)
- De-branded surveys (respondents don't know it's GWI)
- Branching logic personalizes the experience
- Weighted to be representative of the internet population

Sources:
- https://www.gwi.com/core
- https://help.globalwebindex.com/en/articles/5880939-understanding-gwi-core
- https://api.globalwebindex.com/docs/overview/datasets
- https://www.gwi.com/data-coverage

---

## 2. GWI Agent Spark & MCP Integration

### What is Agent Spark?

Agent Spark is GWI's AI insights agent that provides analyst-quality consumer insights at AI speed. It integrates into ChatGPT, Claude, and Microsoft Copilot via MCP (Model Context Protocol).

### MCP Server Details

- **Endpoint**: `POST https://api.globalwebindex.com/v1/spark-api/mcp`
- **Protocol**: JSON-RPC 2.0
- **Authentication**: Bearer token
- **Free tier**: 10 prompts/month; Pro/Teams: unlimited
- **Announced**: November 3, 2025 (Claude integration)

The GWI MCP server (`gwi_spark_ai`) provides two tools:

#### `chat_gwi`
- **Purpose**: Ask natural language questions about audiences, behaviors, preferences, and trends
- **Parameters**:
  - `prompt` (required): Natural language question
  - `chat_id` (optional): UUID from previous call for follow-up conversations
- **Returns**: Structured insight text with insight IDs, source info, regions, time periods, and chat_id

#### `explore_insight_gwi`
- **Purpose**: Drill deeper into a specific insight returned by `chat_gwi`
- **Parameters**:
  - `insight_id` (required): Exact ID from previous `chat_gwi` response
- **Returns**: Detailed methodology, sample sizes, statistical confidence, geographic/demographic breakdowns, time period coverage

### Critical Usage Rules

1. **One question per call** — Never combine multiple questions in a single prompt
2. **No chat_id on first call** — Only include chat_id returned from previous responses
3. **chat_id must be valid UUID** — Never fabricate or guess values
4. **Trend questions split by year** — "How has X changed from 2020-2024?" → 5 separate calls
5. **US English only** — "Soccer" not "football", "cell phone" not "mobile"
6. **Core data only** — No access to add-on datasets (Gaming, Zeitgeist, Travel, etc.)

### Prompt Requirements

Every effective prompt must include:
1. **Audience** — Who (demographics, behaviors, interests)
2. **Topic** — What (behavior, attitude, preference being queried)
3. **Location** (optional) — Where (omit for all 50+ markets)
4. **Timeframe** (optional) — When (omit for latest 4 waves)

### Example Prompts from GWI Documentation

- "What is the difference in gaming platforms usage between generations?"
- "Compare Gen X and Millennials reasons for using social media"
- "What features increase the likelihood of buying a product for Millennial males?"
- "Tell me about EV owners that are also Formula E fans"
- "Tell me about devices used for gaming in the UK in Q3 2024"
- "What are the most popular social media platforms among eco-conscious millennials in the UK?"
- "How do young parents discover brands?"

### Follow-Up Patterns

After an initial query, follow up using the same `chat_id` to:
- Change geographic focus: "And what about France?"
- Narrow the audience: "What about just the 18-24 age group?"
- Explore a different angle: "What are their top social media platforms?"

Sources:
- https://www.gwi.com/platform/spark
- https://www.gwi.com/platform/mcp
- https://help.globalwebindex.com/en/articles/10725804-get-started-with-gwi-spark
- https://api.globalwebindex.com/docs/spark-mcp/integration-guide/mcp-api

---

## 3. Data Interpretation

### Five Core Metrics

1. **Responses (Sample Size)**: Number of survey respondents in a group. Reference metric for data robustness. NOT used for calculating percentages or indexes.
2. **Universe (Population Estimate)**: Estimated real-world internet users in a group. Used for calculating percentage and index figures. Averaged across selected waves.
3. **Audience %**: Proportion of your audience matching a data point. Formula: `(Positive Size / Audience Size) x 100`
4. **Data Point %**: Contribution of your audience to a data point's total. Formula: `(Audience matching data point / Total matching data point) x 100`
5. **Index Score**: How much more/less likely your audience matches a trait vs. the base audience. Baseline = 100. Formula: `(Column % of crossover cell / Column % of total cell) x 100`

### Index Scores

An index score compares an audience's likelihood of a behavior against the general internet population. 100 = average.

- **Index 150** = 1.5x more likely than average
- **Index 200** = 2x more likely (double the rate)
- **Index 50** = half as likely
- **Bidirectional**: Index 122 for "Millennials buying tech" also means "early tech buyers are 22% more likely to be Millennials"
- **Critical distinction**: Index describes propensity, NOT proportion. Correct: "Millennials are 22% MORE LIKELY to buy tech." Incorrect: "22% OF Millennials buy tech."

### When Index Scores Are Misleading

- A 200 index representing 2% of audience is less actionable than a 120 index representing 60%
- Always pair index with penetration percentage
- Flat indexes (~100) suggest overly broad audience definition
- Consistently high indexes may reflect category engagement rather than demographic uniqueness
- Indexes between 90-110 generally not significant enough to warrant attention

### Percentage Caveats

- Percentages may **exceed 100%** because response options are often multi-select (not mutually exclusive)
- Percentages may **fall below 100%** because some questions are routed (only asked to relevant respondents)
- All metrics are calculated using **universe figures, NOT response/sample figures**

### Sample Size Best Practices (from GWI)

GWI recommends:
- **300+ sample size** wherever possible for robust results
- **100-1000** range can produce meaningful results
- Higher within the 100-1000 range = more robust
- Below 100 = directional at best
- **Margin of error**: Small market (3M pop, 1,500 sample) = ~2.5% at 95% confidence; large market (~200M pop, 25,000 quarterly) = <1%

### Rebasing (Advanced)

Rebasing means changing the reference population for comparison. Default base = all internet users aged 16-64.

Use cases:
1. Excluding irrelevant populations (e.g., analyzing men's skincare → apply male-only base)
2. Accounting for routed questions (apply base matching respondent subset)
3. Managing multi-module studies (filter to respondents who completed all relevant survey components)

### Data Point Availability

Not all questions are asked in all markets. When constructing queries:
- Verify data points are present across selected markets
- Exclude markets where the question isn't asked
- Select more waves to increase sample
- Find similar available questions if needed

### Query Logic

When using AND/OR operators in audience definitions:
- People don't always need to meet ALL criteria joined by AND
- Consider using OR when either criterion is relevant
- Use "at least" function to capture people meeting a minimum number of criteria

Sources:
- https://gwihelpcenter.zendesk.com/hc/en-us/articles/4404472522898-Minimum-sample-sizes
- https://help.globalwebindex.com/en/collections/12042531-metrics-and-interpretation

---

## 4. Claude Code Skill Best Practices

### Skill Structure

Every skill requires a `SKILL.md` file with:
- **YAML frontmatter**: `name` (required) + `description` (required)
- **Markdown body**: Instructions, workflows, reference links

Optional bundled resources:
- `scripts/` — Executable code for deterministic tasks
- `references/` — Documentation loaded into context as needed
- `assets/` — Files used in output (templates, images, etc.)

### Progressive Disclosure (3 levels)

1. **Metadata** (~100 tokens) — Always in context. The `name` + `description` determine when the skill triggers.
2. **SKILL.md body** (<5k words) — Loaded when skill triggers.
3. **Bundled resources** (unlimited) — Loaded as needed by Claude.

### Key Conventions

- **Description is the primary trigger** — Include all "when to use" info in the description, NOT the body
- **Body under 500 lines** — Split to references/ if longer
- **One level deep references** — All reference files link directly from SKILL.md
- **No auxiliary files** — No README, CHANGELOG, INSTALLATION_GUIDE
- **Imperative/infinitive writing** — "Use X" not "You should use X"
- **Copy-paste ready examples** — Not pseudocode
- **Don't duplicate MCP tool docs** — Skill = workflow/domain expertise; MCP = connectivity/tools

### MCP-Wrapping Skill Pattern

From Anthropic: "MCP is like having access to the aisles [in a hardware store]. Skills are like an employee's expertise."

A skill wrapping an MCP server should provide:
1. **Workflow sequences** — Which tools to call in what order
2. **Domain knowledge** — How to interpret results, what to check first
3. **Output standards** — How to format and present findings
4. **Multi-step orchestration** — How to break complex questions into sequential queries
5. **Quality standards** — What makes a complete analysis vs. superficial

It should NOT provide:
- How to call the MCP tools (that's the MCP server's job)
- API parameters or connection details
- Generic tool error handling

Sources:
- https://github.com/anthropics/skills (official skills repo + skill-creator SKILL.md)
- https://claude.com/blog/extending-claude-capabilities-with-skills-mcp-servers
- https://claude.com/blog/skills-explained
- Existing local skills: `picnic-mcp-skill`, `ea-sports-fc-brand`, `s5gg-design`

---

## 5. Community Skill Patterns

### Notable Patterns from Community Skills

- **obra/superpowers**: 20+ battle-tested skills with slash commands (/brainstorm, /write-plan, /execute-plan)
- **Trail of Bits Security Skills**: 23+ specialized security analysis skills
- **Vercel Engineering Skills**: Framework-specific best practices
- **Cloudflare Skills**: Platform-specific deployment patterns

### What Top Skills Have in Common

- Comprehensive descriptions listing every trigger scenario
- Quick start sections for immediate use
- Progressive complexity (quick start → common tasks → advanced → reference)
- Explicit warnings about common pitfalls
- Decision trees for choosing approaches
- Cross-references to bundled reference files

Sources:
- https://github.com/travisvn/awesome-claude-skills
- https://github.com/VoltAgent/awesome-agent-skills

---

## 6. Skill File Summary

### Files Created

```
~/.claude/skills/gwi-research/
├── SKILL.md                           # Main skill file (~120 lines)
└── references/
    ├── query-patterns.md              # Detailed query construction guide
    ├── data-interpretation.md         # Index scores, sample sizes, caveats
    └── output-formats.md              # Templates for research outputs
```

### Design Decisions

1. **Description includes all triggers**: audience research, consumer insights, market research, demographic analysis, media planning, brand health, etc.
2. **SKILL.md body stays lean**: Quick reference, critical rules, workflow steps, sample prompts, and links to references. Under 500 lines.
3. **Three reference files**: Split by domain (querying, interpreting, formatting) so Claude only loads what's needed.
4. **No MCP tool duplication**: Skill focuses on workflow, domain expertise, and output quality — doesn't re-explain `chat_gwi` parameters.
5. **Practical over theoretical**: Real prompt examples, concrete templates, actionable error handling.

---

## 7. All Sources

### GWI Platform & Data
- https://www.gwi.com/core
- https://www.gwi.com/data-coverage
- https://www.gwi.com/data
- https://www.gwi.com/connecting-the-dots/methodology

### GWI Help Center
- https://help.globalwebindex.com/en/articles/5880939-understanding-gwi-core
- https://help.globalwebindex.com/en/articles/5880933-gwi-metrics-explained
- https://help.globalwebindex.com/en/articles/5880946-understanding-index-scores
- https://help.globalwebindex.com/en/articles/10725994-understanding-percentages
- https://help.globalwebindex.com/en/articles/10725804-get-started-with-gwi-spark
- https://help.globalwebindex.com/en/articles/13141005-how-to-access-agent-spark
- https://help.globalwebindex.com/en/articles/10726000-rebasing-explained
- https://help.globalwebindex.com/en/articles/5880935-interpreting-wave-on-wave-changes
- https://help.globalwebindex.com/en/collections/12042531-metrics-and-interpretation
- https://gwihelpcenter.zendesk.com/hc/en-us/articles/4404472522898-Minimum-sample-sizes

### GWI API & MCP
- https://api.globalwebindex.com/docs/welcome
- https://api.globalwebindex.com/docs/spark-mcp/integration-guide/mcp-api
- https://api.globalwebindex.com/docs/spark-mcp/integration-guide/overview
- https://api.globalwebindex.com/docs/platform-api/getting-started/gwi-data-structure
- https://api.globalwebindex.com/docs/overview/key-metrics
- https://api.globalwebindex.com/docs/overview/datasets
- https://api.globalwebindex.com/docs/spark-api/getting-started/insight
- https://api.globalwebindex.com/docs/llms.txt
- https://www.gwi.com/platform/mcp
- https://www.gwi.com/platform/spark
- https://www.gwi.com/gwi-mcp-claude-integration
- https://www.gwi.com/integrations

### Press & Announcements
- https://itbrief.co.uk/story/claude-enables-instant-market-research-with-gwi-audience-data
- https://finance.yahoo.com/news/claude-now-run-instant-research-140000095.html
- https://itbrief.asia/story/gwi-unveils-agent-spark-to-power-ai-with-real-audience-data

### Claude Code Skills
- https://github.com/anthropics/skills
- https://claude.com/blog/extending-claude-capabilities-with-skills-mcp-servers
- https://claude.com/blog/skills-explained
- https://github.com/travisvn/awesome-claude-skills
- https://github.com/VoltAgent/awesome-agent-skills
