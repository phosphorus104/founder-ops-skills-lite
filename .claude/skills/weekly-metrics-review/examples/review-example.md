# Metrics review — September 2026 (written 2026-10-05)

Assumptions: from CLAUDE.md, gross margin 82%, target MRR 50,000, runway alarm under 9 months, no target date (so "on plan" below means the target is reached within six months if growth holds), starting values 21,390 MRR and 91 paying customers at the end of May 2026 (the file has no start columns, so MRR and customers are chained from these); source `metrics-sample.csv`, monthly rows, columns mapped one to one.

## Headline
MRR grew 12.5% to 34,120, the fourth month in a row above 12%. If growth holds at that pace, MRR passes the 50,000 target in January 2027, so the period is on plan; runway is 51.4 months, well clear of the 9-month alarm.

## Numbers
| Metric | Sep 2026 | Aug 2026 | Change |
|---|---|---|---|
| MRR | 34,120 | 30,330 | +3,790 |
| Net new MRR | 3,790 | 3,270 | +520 |
| MoM growth | 12.5% | 12.1% | flat |
| Paying customers | 135 | 122 | +13 |
| Net MRR churn | 0.4% | 0.8% | flat |
| Quick ratio | 4.0 | 3.6 | +0.4 |
| ARPA | 253 | 249 | flat |
| CAC | 341 | 353 | −12 |
| LTV : CAC | 18.5 | 16.0 | +2.5 |
| CAC payback (months) | 1.6 | 1.7 | −0.1 |
| Net burn | 2,600 | 2,900 | −300 |
| Runway (months) | 51.4 | 47.0 | +4.4 |

## Three flags
1. Churned MRR rose for the second month, to 1,050 from 1,010, while churned customers held at 4. That is about 263 per leaver against an ARPA of 253, so the customers leaving are slightly larger than average.
2. Sales & marketing spend has risen every month in the file, from 4,600 to 5,800 (+9.4% this month). CAC fell only because new customers rose faster (+13.3% to 17); if sign-ups slow while spend keeps rising, CAC goes up.
3. Runway (51.4 months) is well clear of the 9-month alarm. Most likely to turn next: expansion MRR (1,150) is what keeps net MRR churn under 1%; if expansion stalls, net churn moves toward gross churn, 4.2% this month.

## Three actions for this week
1. List the four September cancellations with plan and tenure, and read any exit-survey text you have for a shared reason.
2. Before raising spend again, split last month's 5,800 by channel in next month's export, so CAC can be read per channel.
3. Pick the five accounts with the largest expansion since June and ask each one what made them upgrade; use the answers on the pricing page.

## Definitions
- MRR end = MRR start + net new MRR. Net new MRR = new + expansion − contraction − churned. Customers end = customers start + new − churned.
- MoM growth = MRR end ÷ MRR start − 1.
- Net MRR churn = (contraction + churned − expansion) ÷ MRR start. Gross MRR churn = (contraction + churned) ÷ MRR start.
- Quick ratio = (new + expansion) ÷ (contraction + churned). Customer churn = churned customers ÷ customers start.
- ARPA = MRR end ÷ customers end. CAC = S&M spend ÷ new customers. LTV = ARPA × 0.82 ÷ customer churn. Payback = CAC ÷ (ARPA × 0.82).
- Net burn = total expenses − MRR end. Runway = cash ÷ net burn.

Written to docs/reviews/2026-10-05.md
