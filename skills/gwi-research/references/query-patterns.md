# GWI Query Patterns Reference

## Table of Contents

- [Prompt Construction](#prompt-construction)
- [Audience Definitions](#audience-definitions)
- [Location and Timeframe](#location-and-timeframe)
- [Query Operators](#query-operators)
- [Common Pitfalls](#common-pitfalls)
- [Advanced Techniques](#advanced-techniques)
- [Research Workflows](#research-workflows)

## Prompt Construction

### The Four Components

Every effective `chat_gwi` prompt includes:

```
[Audience] + [Topic] + [Location (optional)] + [Timeframe (optional)]
```

**Minimal prompt** (uses all markets, latest 4 waves):
> "What are the social media habits of Gen Z?"

**Specific prompt**:
> "What are the top social media platforms among eco-conscious millennials in the UK in 2024?"

### Prompt Phrasing Styles

| Style | Example | Best For |
|-------|---------|----------|
| Profile | "Tell me about [audience] in [location]" | Broad audience overview |
| Comparison | "Compare [A] and [B] on [topic]" | Competitive/segment analysis |
| Preference | "Are [audience] more likely to [X] or [Y]?" | Binary choice questions |
| Driver | "What motivates [audience] to [behavior]?" | Purchase/behavior drivers |
| Temporal | "Tell me about [audience] in [location] in [year]" | Point-in-time snapshot |

## Audience Definitions

### Demographic Audiences

- Age groups: "Gen Z", "Millennials", "Gen X", "Baby Boomers", "ages 18-24", "aged 25-34"
- Gender: "males", "females", "women aged 25-34"
- Income: "high-income consumers", "middle-income households"
- Education: "university-educated", "postgraduate consumers"
- Employment: "full-time workers", "freelancers", "business decision-makers"
- Parenting: "parents", "young parents", "parents of children under 5"

### Behavioral Audiences

- Platform users: "Instagram users", "TikTok creators", "YouTube Premium subscribers"
- Device: "smartphone-only internet users", "tablet owners", "smart TV users"
- Activity: "online shoppers", "mobile gamers", "podcast listeners", "ad blocker users"
- Purchase: "luxury buyers", "EV owners", "subscription service users"

### Interest-Based Audiences

- Sports: "football fans", "basketball fans", "Formula E fans", "esports viewers"
- Lifestyle: "fitness enthusiasts", "eco-conscious consumers", "foodies"
- Tech: "early adopters", "AI tool users", "cryptocurrency investors"
- Media: "streaming subscribers", "news readers", "audiobook listeners"

### Combining Audience Criteria

Combine demographics + behaviors + interests for precision:
> "Tell me about female gamers aged 18-34 in Germany who use social media daily"

> "Compare high-income EV owners with middle-income EV owners in the US"

> "What are the media habits of eco-conscious Gen Z parents in the UK?"

## Location and Timeframe

### Location Specification

- **Single market**: "in the UK", "in Japan", "in Brazil"
- **Multi-market**: "in Germany and France", "in the US and UK"
- **Regional**: "in Europe", "in Asia Pacific", "in Latin America"
- **Global**: Omit location entirely (defaults to all 50+ markets)

**Important**: Country local regions (e.g., "in Bavaria", "in California") are NOT supported. Use country-level only.

### Available Markets (GWI Core)

**EMEA**: Austria, Belgium, Denmark, Egypt, France, Germany, Ghana, Ireland, Israel, Italy, Kenya, Morocco, Netherlands, Nigeria, Norway, Poland, Portugal, Romania, Russia, Saudi Arabia, South Africa, Spain, Sweden, Switzerland, Turkey, UAE, UK

**Americas**: Argentina, Brazil, Canada, Chile, Colombia, Mexico, USA

**APAC**: Australia, China, Hong Kong, India, Indonesia, Japan, Malaysia, New Zealand, Philippines, Singapore, South Korea, Taiwan, Thailand, Vietnam

### Timeframe Specification

- **Year**: "in 2024", "in 2023"
- **Quarter**: "in Q3 2024", "Q1 and Q2 2022"
- **Range**: "from 2021 to 2023" (but break into single-year calls for trends)
- **Default**: Omit for latest 4 waves of data

## Query Operators

When building audiences in `chat_gwi`, GWI processes natural language. Consider logical scope:

- **AND (intersection)**: "gamers AND parents" = people who are both
- **OR (union)**: "Instagram OR TikTok users" = people who use either
- **"At least" function**: "people who meet at least 2 of these 4 criteria"

**Tip**: People don't always need to meet ALL criteria joined by AND. If your audience is too narrow, consider OR or "at least" phrasing.

## Common Pitfalls

### Language Ambiguity
- "Football" means soccer in most markets but American football in the US. Say "soccer" or "American football" explicitly.
- "Mobile" can mean cell phone or mobile internet. Be specific: "smartphone" or "mobile phone".

### Overly Complex Prompts
**Bad**: "What are the demographics, behaviors, and marketing channels for Windows 10 users in the UK?"
**Good**: Break into 3 separate calls, each with one question.

### Add-On Data Requests
Agent Spark only accesses GWI Core. Requests for Gaming, Zeitgeist, Travel, Luxury, Sports, Automotive, Alcohol, Consumer Tech, Work, or Moments add-on data will not return results.

### Trend Questions in Single Call
**Bad**: "How has consumer perception of Tesla changed from 2020 to 2024?"
**Good**: 5 separate calls, one per year (2020, 2021, 2022, 2023, 2024), using the same `chat_id`.

### Missing Audience or Topic
Prompts without a clear audience AND topic produce vague results. Always specify both.

### Narrow Audience + Small Market
Combining a niche audience with a small market (e.g., "vegan gamers aged 18-24 in Kenya") may yield sample sizes too small for reliable insights. Broaden the audience, add markets, or extend the timeframe.

## Advanced Techniques

### Sequential Deepening

Start broad, narrow progressively:
```
1. "Tell me about streaming service users in Germany" → overview
2. "What content genres do they prefer?" → behavioral detail
3. "How do they discover new shows?" → media touchpoint mapping
4. explore_insight_gwi → statistical backing for key finding
```

### Competitive Audience Overlap

Map audience overlaps between brands:
```
1. "Tell me about Netflix subscribers in the UK"
2. "What about Disney+ subscribers in the UK?" (same chat_id)
3. "Compare Netflix and Disney+ subscribers on social media usage" (same chat_id)
```

### Market Entry Research

Evaluate a market opportunity:
```
1. "Tell me about [product category] users in [target market]"
2. "What brands do they currently prefer?" (chat_id)
3. "What are their unmet needs or pain points?" (chat_id)
4. "How do they discover new brands in this category?" (chat_id)
```

### Persona Building

Create a data-backed persona:
```
1. Demographics → age, gender, income, education profile
2. Digital life → devices, platforms, daily screen time
3. Media diet → news sources, streaming, social media
4. Purchase behavior → drivers, channels, brand loyalty signals
5. Attitudes → values, concerns, lifestyle priorities
```

## Research Workflows

### Agency Pitch Preparation
1. Profile the target audience with demographics + behaviors
2. Compare with competitor brand audiences
3. Identify unique behavioral or attitudinal differentiators
4. Extract 3-5 headline stats for the pitch deck
5. Format as persona card + key insight slides

### Content Strategy
1. Profile the target audience's media consumption
2. Identify top platforms and content formats
3. Query content discovery behaviors
4. Map content preferences by platform
5. Synthesize into channel-by-content matrix

### Brand Health Check
1. Query brand awareness/perception in target market
2. Compare with 2-3 competitor brands (same chat_id)
3. Break into yearly snapshots for trend analysis
4. Identify strengths and vulnerabilities
5. Format as brand scorecard with trend arrows
