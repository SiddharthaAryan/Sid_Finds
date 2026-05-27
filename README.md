# Sid Finds — Keyword Intelligence Dashboard

Sid Finds is a CSV-first keyword analysis dashboard for healthcare digital marketing teams.

It helps the digital head decide which keywords should be pushed to get maximum reach by combining:

- Google Search Console keyword data
- RankNow ranking data
- Google Analytics 4 landing-page data
- Google Trends / manual trend data
- Hospital-specific department and intent mapping

## Current version

This is **MVP 1**.

It does not require API keys yet. The first version works through CSV uploads so the scoring logic can be validated before building secure API connections.

## Files

- `index.html` — full dashboard application
- `README.md` — setup and usage guide

## How to use

Open `index.html` in a browser or publish the repository through GitHub Pages.

Then use either:

1. **Load sample hospital data** — to see the dashboard instantly.
2. **Upload CSV exports** from the data sources.
3. **Add manual keywords** when the team has campaign ideas but no export yet.
4. **Export recommendations CSV** for weekly reporting.
5. **Print / Save PDF** for management sharing.

## Expected CSV columns

The app is flexible with column names, but these are the recommended columns.

### Google Search Console CSV

| Column | Meaning |
|---|---|
| `query` | Search keyword |
| `clicks` | Search clicks |
| `impressions` | Search impressions |
| `ctr` | Click-through rate |
| `position` | Average Google position |
| `page` | Landing page URL/path |

### RankNow CSV

| Column | Meaning |
|---|---|
| `keyword` | Keyword being tracked |
| `rank` | Current rank |
| `previous rank` | Previous rank |
| `url` | Ranking URL |

### Google Analytics 4 CSV

| Column | Meaning |
|---|---|
| `landing page` | Landing page path |
| `users` | Users |
| `sessions` | Sessions |
| `conversions` | Leads, appointments or key events |

### Google Trends CSV

| Column | Meaning |
|---|---|
| `keyword` | Keyword |
| `interest` | Trend interest score |
| `growth` | Growth percentage or movement |

## Scoring logic

Each keyword gets a score from 0 to 100.

The simplified formula is:

```text
Keyword Score = Demand + Trend + Current Reach + Conversion Intent + Local Boost + Gap Opportunity + GA Value
```

Where:

- **Demand** comes from impressions.
- **Trend** comes from Google Trends interest/growth.
- **Current Reach** comes from current rank or average position.
- **Conversion Intent** is inferred from terms like doctor, hospital, treatment, surgery, emergency, near me, etc.
- **Local Boost** is added if the keyword includes the selected city, for example Raipur.
- **Gap Opportunity** is added when the keyword has high impressions but low CTR, or is ranking between position 4 and 20.
- **GA Value** is added if the mapped landing page has users or conversions.

## Hospital-specific department mapping

The MVP automatically maps keywords into departments such as:

- Cardiac
- Renal
- Neuro
- Oncology
- Emergency
- Orthopedics
- Gastro
- Mother & Child
- General Medicine
- Diagnostics
- Generic / Brand

## Recommended build roadmap

### Stage 1 — CSV MVP

Completed in the current version.

### Stage 2 — Google Search Console API

This should be the first live API integration because it gives real query-level SEO data: clicks, impressions, CTR and average position.

### Stage 3 — GA4 Data API

This adds landing-page performance and conversion context.

### Stage 4 — RankNow integration

If RankNow provides API access, connect directly. If not, CSV upload remains a safe workflow.

### Stage 5 — Trends layer

Google Trends should be treated carefully because official production API support is limited. For now, Trends CSV/manual input is safest.

### Stage 6 — Weekly AI report

Generate a weekly digital marketing action report with:

- Top keywords to push
- Keywords losing rank
- CTR leakage keywords
- Department-wise priorities
- Recommended content actions

## Important security note

Do not put private OAuth secrets, service account keys or admin credentials inside `index.html`.

When live API integration starts, use a backend layer such as Firebase Functions, Cloud Run, Node.js server or another secure backend.

## Suggested GitHub Pages setup

1. Go to repository settings.
2. Open **Pages**.
3. Select source: `Deploy from a branch`.
4. Select branch: `main`.
5. Select folder: `/root`.
6. Save.
7. Open the generated GitHub Pages link.

