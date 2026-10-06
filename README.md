# Founder Ops Skills Lite

Two free skills for Claude Code that handle jobs a one-person SaaS repeats: the Monday metrics review and release notes. Plain Markdown, MIT licensed, each with a worked example.

From Small Numbers, plain tools for one-person businesses. Not affiliated with Anthropic.

## The two skills

| Skill | Run it when | What you get |
|---|---|---|
| `/weekly-metrics-review` | Monday, with last period's numbers exported | A one-page review: MRR movement, net MRR churn, quick ratio, CAC, LTV:CAC, runway, three flags and three actions |
| `/release-notes` | Before you tag a release | A CHANGELOG entry, customer-facing release notes and a 280-character summary, all from the commits since the last tag |

Each folder holds the skill (`SKILL.md`) and `examples/`: a realistic input and the output the skill produced from it, so you can see the standard before you run it.

```
.claude/
└── skills/
    ├── weekly-metrics-review/   SKILL.md + examples/metrics-sample.csv, review-example.md
    └── release-notes/           SKILL.md + examples/git-log-sample.txt, release-notes-example.md
```

## Install

1. Copy the `.claude/skills/` folder into the root of your repository, so it sits next to your code. To use the skills in every project, copy the two folders into `~/.claude/skills/` instead.
2. Add the lines below to the `CLAUDE.md` in your repo root (create it if you have none) and fill the blanks. The skills read them. A missing value is either asked for (the metrics starting values) or written as an "Assumption" line at the top of the output, never used silently.
3. Open Claude Code in the repo and type `/`. Both skills appear in the menu, and each also triggers when your request matches its description.
4. Try the review on its example. To reproduce `examples/review-example.md`, fill the Metrics lines with the example's values: starting values 21,390 MRR and 91 customers, gross margin 82%, target MRR 50,000, runway alarm under 9 months. Then run `/weekly-metrics-review .claude/skills/weekly-metrics-review/examples/metrics-sample.csv`. The review is also saved as a Markdown file at your review path (default `docs/reviews/<date>.md`); delete it after the test if you like.

```markdown
## Metrics
- Source of truth (where the export lives): <path to CSV export, e.g. data/metrics.csv>
- Columns: <month, new_customers, churned_customers, new_mrr, expansion_mrr, contraction_mrr, churned_mrr, sales_marketing_spend, total_expenses, cash>
- Starting values (when the export has no MRR-start column): <MRR and paying customers at the end of the month before the first row>
- Gross margin assumption: <80%>. Target MRR: <X>. Runway alarm: <under 9 months>.
- Review output path: <docs/reviews/YYYY-MM-DD.md>

## Release process
- Changelog: <CHANGELOG.md>. Release notes posted to: <changelog page, email>.
- Commit convention: <Conventional Commits, or none>.
- Voice: <plain, no hype>. Words customers use: <"workspace", not "tenant">.
```

## How they behave

- The review lists its assumptions at the top; the release notes mark a version they proposed and list commits that need your word.
- They never invent numbers: a metric the input cannot support is shown as "not computable" with the reason.
- They never send, post, deploy or tag anything. The review writes one Markdown file to your review path; release notes are printed for you to check and paste.
- The review works on monthly or weekly rows; the examples use monthly.

## The full kit

The paid edition, [Founder Ops Skills for Claude Code](https://smallnumbers.gumroad.com/l/founder-ops-skills-claude-code), adds four more skills (support replies in your voice, pricing-page tests, incident write-ups, cancellation feedback) and a full `CLAUDE.md` template covering product, pricing, policies, voice and support. The weekly review pairs with the free [SaaS Metrics Dashboard Lite](https://smallnumbers.gumroad.com/l/saas-metrics-lite) spreadsheet.

## License

MIT. See `LICENSE`. "Claude" and "Claude Code" are trademarks of Anthropic, PBC; these files are an independent project written for use with Claude Code and are not affiliated with, sponsored by or endorsed by Anthropic.
