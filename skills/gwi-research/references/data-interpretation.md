# GWI Data Interpretation Reference

## Table of Contents

- [Five Core Metrics](#five-core-metrics)
- [Index Scores](#index-scores)
- [Percentages and Reach](#percentages-and-reach)
- [Sample Size Considerations](#sample-size-considerations)
- [Quarterly Data Context](#quarterly-data-context)
- [Cross-Referencing and Caveats](#cross-referencing-and-caveats)
- [Rebasing](#rebasing)
- [Common Interpretation Mistakes](#common-interpretation-mistakes)

## Five Core Metrics

GWI reports five primary metrics:

1. **Responses (Sample Size)**: Number of survey respondents in a group. Reference for data robustness. NOT used for calculating percentages or indexes.
2. **Universe (Population Estimate)**: Estimated real-world internet users in a group. Used for calculating percentage and index. Averaged across selected waves.
3. **Audience %**: Proportion of your audience matching a data point. Formula: `(Positive Size / Audience Size) x 100`
4. **Data Point %**: Contribution of your audience to a data point's total. Formula: `(Audience matching data point / Total matching data point) x 100`
5. **Index Score**: How much more/less likely your audience matches a trait vs. base. Formula: `(Column % of crossover cell / Column % of total cell) x 100`

All metrics are calculated using **universe (population estimate) figures, NOT sample/response figures**.

## Index Scores

### What Index Scores Mean

An **index score** compares an audience's likelihood of a behavior/attitude against the general internet population (the base). An index of 100 means average.

| Index Range | Meaning | Reporting Guidance |
|-------------|---------|-------------------|
| < 80 | Significantly under-indexes | "notably less likely than average" |
| 80-95 | Slightly under-indexes | "somewhat less likely" |
| 95-105 | Average / in line | "in line with the general population" |
| 105-120 | Slightly over-indexes | "somewhat more likely" |
| 120-150 | Notably over-indexes | "significantly more likely" — highlight this |
| 150-200 | Strongly over-indexes | "strongly over-indexes" — lead with this |
| > 200 | Extremely over-indexes | "extremely distinctive" — headline stat |

### Interpreting Index Scores

- An index of **150** means the audience is **1.5x more likely** than average to exhibit this behavior
- An index of **200** means **2x more likely** (double the average rate)
- An index of **50** means **half as likely** as the general population
- **Bidirectional**: Index 122 for "Millennials buying tech" also means "early tech buyers are 22% more likely to be Millennials"
- **Critical distinction**: Index describes propensity, NOT proportion. Correct: "Millennials are 22% MORE LIKELY to buy tech." Incorrect: "22% OF Millennials buy tech."

### When Index Scores Are Most Useful

- Identifying what makes an audience **distinctive** vs. the general population
- Comparing **relative strength** of different attributes within an audience
- Finding **over-indexed behaviors** for targeting and messaging
- Spotting **under-indexed areas** as potential white space opportunities

### When to Use Percentages Instead

- Reporting **absolute reach** or market size
- Communicating to stakeholders who need real numbers, not relative metrics
- Comparing **how many people** in an audience do something (not how distinctive it is)

## Percentages and Reach

### Types of Percentage Metrics

- **Audience %**: The proportion of your defined audience that exhibits a behavior. Formula: `(Positive Size / Audience Size) x 100`
- **Data Point %**: Contribution of your audience to a data point's total. Formula: `(Audience matching / Total matching) x 100`
- **The gap between audience % and population % produces the index score**

### Important: Percentages Can Exceed 100%

- GWI questions are often **multi-select** (respondents pick all that apply), so percentages across options do NOT sum to 100%
- Some questions are **routed** (only asked to relevant respondents), so base sizes vary within a dataset

### Reading Percentages

A high percentage with a low index means the behavior is common generally (not distinctive).
A low percentage with a high index means the behavior is niche but strongly over-represented in this audience.

Example:
- "85% of Gen Z use social media" (high %, but everyone does — index might be 105)
- "12% of Gen Z invest in crypto" (low %, but if the general pop is 5%, index = 240 — very distinctive)

**Always report both the percentage AND the index** when the distinction matters.

## Sample Size Considerations

### Minimum Thresholds

| Sample Size | Confidence Level | Reporting Guidance |
|-------------|-----------------|-------------------|
| < 50 | Unreliable | Do not report. Flag as insufficient data. |
| 50-99 | Low | Directional only. "Indicative data suggests..." |
| 100-299 | Moderate | Usable with caveat. "Based on a moderate sample..." |
| 300-999 | Good | Report with confidence. Standard reliability. |
| 1000+ | High | High confidence. Lead with these findings. |

### GWI Recommendation

GWI recommends **300+ sample size** wherever possible. Between 100-1000 can produce meaningful results; higher within this range = more robust.

### How to Increase Sample Size

If sample is too small:
1. **Broaden audience** — Widen age range, remove a filter layer
2. **Add markets** — Include additional countries in the query
3. **Extend timeframe** — Select more quarterly waves
4. **Use related questions** — Find a similar question asked in more markets

### Reporting Low Sample Sizes

Always flag in output:
> "Note: This finding is based on a sample of [N] respondents and should be treated as directional rather than definitive."

## Quarterly Data Context

### How Quarterly Data Works

GWI Core surveys are conducted quarterly. Responses include metadata about which quarters are covered.

### Using Quarterly Information

- **Reference specific quarters** when discussing data recency
- **Account for seasonality** — Q4 captures holiday behaviors, Q1 shows post-holiday patterns
- **Mention data coverage span** when relevant: "Based on Q3 2024 through Q2 2025 data"

### Seasonal Considerations

| Quarter | Context |
|---------|---------|
| Q1 (Jan-Mar) | Post-holiday, New Year resolutions, back-to-routine |
| Q2 (Apr-Jun) | Spring/summer planning, pre-vacation |
| Q3 (Jul-Sep) | Summer behavior, back-to-school, early holiday planning |
| Q4 (Oct-Dec) | Holiday shopping, year-end consumption peaks |

### Example Quarterly Framing

> "Based on Q3-Q4 2024 and Q1-Q2 2025 data, PlayStation 5 users in Japan show strong social media engagement patterns, with particularly high TikTok usage (index: 201) and Instagram activity (index: 200). The Q4 2024 data captures holiday season behaviors, while Q1-Q2 2025 shows post-holiday patterns."

## Cross-Referencing and Caveats

### What GWI Data Is

- **Self-reported survey data** from online respondents aged 16-64
- Represents the **internet population**, not total population
- Weighted and quota-controlled for age, gender, and education
- Consistent methodology across 50+ markets

### What GWI Data Is Not

- Not transactional or behavioral tracking data (it's what people say, not what systems log)
- Not representative of offline-only populations
- Not real-time (quarterly cadence with processing lag)
- Not a substitute for first-party customer data

### Combining with Other Sources

When cross-referencing GWI data:

1. **First-party data** (CRM, analytics): GWI adds attitudinal and behavioral context that first-party data lacks
2. **Social listening**: GWI provides structured survey data to validate or challenge social trends
3. **Census/government data**: GWI covers internet population only; caveat when comparing with total population stats
4. **Competitor platforms** (Statista, eMarketer): Methodologies differ; note the source and approach when comparing

### Standard Caveats to Include

Always include when presenting GWI findings:

- **Source**: "Source: GWI Core [quarter/year], [market(s)], internet users aged 16-64"
- **Sample**: "Based on [N] respondents" (when known)
- **Population caveat**: "Figures represent the online population aged 16-64"
- **Self-report caveat**: "Based on self-reported survey data" (when relevant, e.g., for sensitive topics)

## Rebasing

### What Is Rebasing?

Rebasing means changing the reference population for comparison. By default, the base is all internet users aged 16-64 in the dataset.

### When to Rebase

1. **Excluding irrelevant populations**: Analyzing men's skincare → apply male-only base
2. **Accounting for routed questions**: Apply base matching the respondent subset who received that question
3. **Managing multi-module studies**: Filter to respondents who completed all relevant survey components

### Effect on Metrics

Rebasing recalculates all percentages and index scores against the new base. A behavior that indexes at 120 against the general population may index at 95 when rebased to a more relevant segment — revealing it's not actually distinctive within that group.

## Common Interpretation Mistakes

### Mistake: Confusing Index with Percentage
An index of 200 does NOT mean 200% of the audience does something. It means they are 2x more likely than average.

### Mistake: Ignoring Base Rates
A high index on a rare behavior might represent very few actual people. Always check the percentage alongside the index.

### Mistake: Over-Reading Small Differences
An index of 108 vs. 104 is not meaningful. Focus on differences of 15+ index points.

### Mistake: Treating Survey Data as Behavioral Fact
GWI data is self-reported. People may overstate socially desirable behaviors (exercise, healthy eating) and understate undesirable ones (screen time, junk food).

### Mistake: Ignoring Market Availability
Not all questions are asked in all 50+ markets. If data seems missing, the question may not be available in that market. Remedy: exclude the market or find a similar available question.

### Mistake: Comparing Across Incompatible Timeframes
Quarterly data from Q1 2024 is not directly comparable to Q4 2024 without accounting for seasonal effects. Compare same quarters year-over-year for clean trend analysis.
