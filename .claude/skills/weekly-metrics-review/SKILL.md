---
name: weekly-metrics-review
description: >-
  Writes the Monday metrics review for a subscription business from an exported metrics table (CSV, Markdown table or pasted rows). Computes MRR movement, net MRR churn, quick ratio, CAC, LTV:CAC, net burn and runway for the latest period, compares with the previous period, and ends with three flags and three actions. Use when the founder asks for a weekly or monthly review, "how did last week go", or hands over a metrics export.
argument-hint: "[path-to-metrics.csv]"
allowed-tools: Read Glob Grep Write
---

# Weekly metrics review

You are writing the one-page review a founder reads on Monday morning. The reader already knows the business; they want the movement, the reasons, and what to do this week.

## Inputs

1. `$ARGUMENTS` is the path to the metrics export. If empty, look in the location named under **Metrics** in `CLAUDE.md`; if that is blank too, ask for the file and stop.
2. From `CLAUDE.md` take: gross margin assumption, target MRR, runway alarm threshold, review output path. A missing value becomes an "Assumption" line at the top of the review, never a silent default.

Expected columns, one row per period (month unless the file says otherwise): period, new customers, churned customers, new MRR, expansion MRR, contraction MRR, churned MRR, sales & marketing spend, total expenses, cash at period end. Optional: MRR start and customers start per row. Map column names loosely (`s&m`, `marketing_spend` and `sales_marketing_spend` are the same thing) and list the mapping you used.

If the file has no MRR start and customers start columns, you need the MRR and paying customers at the end of the period before the first row. Take them from **Metrics → Starting values** in `CLAUDE.md`; if that is blank, ask for the two numbers once and stop. Chain every later row from them and say so in Assumptions.

## Method

Compute for the latest period (L) and the one before (P). Show the formula once, in the Definitions block at the end.

- MRR end = MRR start + new + expansion − contraction − churned. Customers end = customers start + new − churned. Chain both from the starting values when the file lacks start columns.
- Net new MRR = new + expansion − contraction − churned.
- MoM MRR growth = MRR end ÷ MRR start − 1.
- Net MRR churn = (contraction + churned − expansion) ÷ MRR start. Negative is good.
- Gross MRR churn = (contraction + churned) ÷ MRR start.
- Quick ratio = (new + expansion) ÷ (contraction + churned); not computable when contraction + churned = 0.
- Customer churn = churned customers ÷ customers at start.
- ARPA = MRR end ÷ customers at end.
- CAC = sales & marketing spend ÷ new customers.
- LTV = ARPA × gross margin ÷ monthly customer churn, capped at 60 months of lifetime when churn is zero.
- CAC payback (months) = CAC ÷ (ARPA × gross margin).
- Net burn = total expenses − MRR end. Runway = cash ÷ net burn; "profitable" when net burn ≤ 0.

Rules:
- A denominator of zero gives "not computable (no new customers this period)", never a number.
- Compute every Change from unrounded values, then round: money to whole units, ratios and months to one decimal, percentages to one decimal, percentage-point changes to one decimal.
- Compare L with P in words a founder uses: "MRR grew 12.5% to 34,120, up from 11.0% growth last month."
- Flat rule, applied to the Change column and to prose alike: a percentage that moved less than 0.5 point, or any other metric that moved less than 2% of its previous value, is written as "flat". Everything else gets its signed number.

## Output

Write Markdown to the review path from `CLAUDE.md` (default `docs/reviews/<YYYY-MM-DD>.md`, today's date) and print it. Structure, in this order and nothing else:

```
# Metrics review — <period L> (written <today>)

Assumptions: <gross margin %, target MRR, source file, column mapping; or "none, all from CLAUDE.md">

## Headline
<Two sentences: the single most important movement and whether the period is on plan against target MRR.>

## Numbers
| Metric | <L> | <P> | Change |
(MRR, net new MRR, MoM growth, paying customers, net MRR churn, quick ratio, ARPA, CAC, LTV:CAC, CAC payback, net burn, runway)

## Three flags
1. <Something that got worse, with the number and the likeliest cause from the data>
2. ...
3. <If nothing got worse, say so and flag the thing most likely to turn next>

## Three actions for this week
1. <Specific, finishable in a week, tied to a flag>
2. ...
3. ...

## Definitions
<one line per formula used>

Written to <path>
```

## Checklist before you finish

- [ ] Every number in the table traces to a column in the input or a formula in Definitions.
- [ ] No metric is computed from fewer than one full period.
- [ ] Runway is compared against the alarm threshold from `CLAUDE.md`, and the alarm is the first flag when it trips.
- [ ] Actions name a thing to ship, send or measure, not "look into".
- [ ] The file was written to the review path and the path is the last line of the output.

## Pitfalls

- Stripe exports count refunds as negative new MRR; net them into churned MRR and say so.
- Annual plans paid up front are not twelve months of new MRR; divide by twelve.
- A period with no rows is a missing export, not zero revenue. Stop and ask.
