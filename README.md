# NBA Dashboards

This workspace contains self-contained dashboard generators for the CSV file:

`C:\Users\NathanJeongGilligan\Downloads\NBA data_2026-05-25-1100.csv`

## Dashboards

### 1. Next Best Action Dashboard

Files:

- `generate_dashboard.mjs`
- `dashboard.html`
- `analysis-summary.json`
- `top10-next-best-actions.csv`
- `priority-customers.csv`

Run:

```powershell
node .\generate_dashboard.mjs
```

This is the action-oriented view. It ranks campaign opportunities using lifecycle, spend, recency, channel, family/lifestage, and linked-brand signals.

### 2. Insights Dashboard

Files:

- `generate_insights_dashboard.mjs`
- `insights-dashboard.html`
- `insights-summary.json`

Run:

```powershell
node .\generate_insights_dashboard.mjs
```

This is the exploratory view. It focuses on data breakdowns such as:

- lifecycle cluster mix
- customer/value concentration
- recency buckets
- spend buckets
- shopping preference mix
- lifestage mix
- linked-brand coverage
- data completeness

When you run the insights generator, it also writes `index.html` so the dashboard is ready for GitHub Pages.

## How to run it

From this folder:

```powershell
node .\generate_dashboard.mjs
```

or

```powershell
node .\generate_insights_dashboard.mjs
```

To point it at a different CSV:

```powershell
node .\generate_dashboard.mjs "C:\path\to\your-file.csv"
```

```powershell
node .\generate_insights_dashboard.mjs "C:\path\to\your-file.csv"
```

## Host on GitHub Pages

The easiest way to publish the insights dashboard is to upload these files to a GitHub repository:

- `index.html`
- `insights-dashboard.html`
- `insights-summary.json`
- `README.md`

Notes:

- `index.html` is the file GitHub Pages will load automatically
- you usually do not want to upload the raw CSV here because it is large
- the generated dashboard is static, so it can be hosted directly on GitHub Pages

Basic flow:

1. Create a new GitHub repository.
2. Upload the files above using the GitHub web interface or git locally.
3. In the GitHub repo, go to `Settings` -> `Pages`.
4. Under `Build and deployment`, set `Source` to `Deploy from a branch`.
5. Choose the `main` branch and the `/ (root)` folder, then save.
6. Wait a minute or two for GitHub Pages to publish the site.
7. Open the URL GitHub shows, which will look like `https://your-username.github.io/your-repo-name/`.

## Next Best Action Scoring

The ranking is rule-based, not predictive. It uses:

- lifecycle cluster
- spend/value
- recency
- shopping preference
- family/lifestage signals
- linked-brand inactivity

Estimated impact is calculated from:

`value base x lift assumption x urgency multiplier x family relevance multiplier`

Notes:

- `value base` prefers `TOTAL_SPEND_365D`, then falls back to `TOTAL_YEARLY_SPEND`, then `MONETARY`
- action audiences can overlap
- `NO OP TRANSACTION`, `MISSING`, and `DROPSHIP EXCLUDED` rows are excluded from the eligible action base
