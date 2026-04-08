# Reddit Post — Dashboard Drop

**Target subs:** r/SaaS, r/ClaudeAI, r/sales, r/nextjs, r/webdev

---

**Title:** I built a GTM dashboard with Claude Code + Supabase. sharing it as it grows.

**Body:**

i've been building go-to-market systems with coding agents (Claude Code specifically) for the past few months. the first thing i open-sourced was a 10-chapter starter kit for GTM engineers learning to use coding agents.

today i'm adding a production dashboard to that repo.

**the stack:**

- Next.js 16 + React 19 + TypeScript
- Tailwind v4 + shadcn/ui (dark theme)
- Recharts for charts
- Supabase (Postgres) for the database
- Python scripts for the signal pipeline

**what the dashboard does:**

5 pages. campaigns overview with KPI cards and send volume charts. database intelligence showing enrichment coverage and score distributions. an accounts browser with expandable rows (click a company, see its contacts and mapped signals). a signals page with intent signal analytics. and a segments page with live-computed campaign segments.

everything polls from Supabase via Next.js API routes every 15-30 seconds. no websockets needed for an operational dashboard.

**the signal scoring model is the core:**

16 intent signal types, each with a configurable weight (0-10). signals decay exponentially with a 14-day half-life. the formula:

```
score = signal_weight * source_reliability * e^(-0.0495 * days_old)
```

capped at 20 points per signal type to prevent one source from inflating scores. diversity bonuses: +2 per distinct signal type, +3 per distinct data source. a company with signals from 3 different types and 2 sources scores higher than one with 10 identical signals from one source.

signal types include: tool_evaluation (10), vendor_switch (10), hiring_signal (8), pain_expression (7), budget_mention (6), competitor_mention (5), and more.

**the supabase schema:**

companies table with ICP scoring. contacts table with a hard 3-per-company limit enforced by a postgres trigger (forces you to rank contacts by quality). signals table mapped to companies. campaign infrastructure with auto-pause triggers when bounce rate exceeds 2%.

3 SQL files, run them in order, you have a working backend.

**the pipeline:**

3 Python scripts. one discovers companies via the Exa API (neural search by vertical). one scores signals using the decay formula. one loads everything to Supabase. you can swap Exa for Apollo, Clay, or a manual CSV and the rest still works.

**why build it when i use hubspot and instantly already:**

i'm already building my database, writing signal logic, and designing segments. the dashboard is just the visual layer on top of work i'm already doing. it's in sync with my data because i built both. and when i need a new view next week, i add it in 20 minutes instead of submitting a feature request.

**the repo:**

it's part of the GTM coding agent starter kit. chapter 11 walks through the architecture. the starter is in `starters/signals-dashboard/`. MIT license.

this is not a finished product. it's a starting point. i'm still building on it and would genuinely appreciate feedback, PRs, or just hearing what you'd add.

link: [will add in edit/comment per sub rules]

---

# Per-Community Variants

---

## r/ClaudeAI Variant

**Title:** Claude Code + Supabase = GTM dashboard. built the whole thing in one session.

**Body:**

sharing something i built entirely in Claude Code this week.

i've been using Claude Code for go-to-market work (not software engineering -- prospecting, enrichment, campaign management). earlier this year i open-sourced a starter kit with 10 chapters on using coding agents for GTM.

this week i sat down and built a full dashboard in a single session. the whole thing -- schema, API routes, 5 pages, signal scoring pipeline.

**what Claude Code built:**

- Supabase schema: 3 SQL files with companies, contacts, signals, campaigns. triggers that enforce a 3-contact-per-company limit and auto-pause domains over 2% bounce rate.
- 10 Next.js API routes with parallel Supabase queries
- 5 React pages with shadcn/ui components, Recharts charts, real-time polling
- Python signal scoring pipeline with exponential decay
- the whole project genericized from my production mission control

i described what each page should show and Claude Code wrote it. when something was wrong i described the fix and it applied it. the iteration loop was fast enough that i shipped 48 files in one sitting.

**the interesting technical parts:**

the signal model uses 16 weighted intent signal types with exponential decay (14-day half-life). `score = weight * reliability * e^(-0.0495 * days_old)`. diversity bonuses reward breadth across signal types and sources.

a Postgres trigger enforces max 3 ranked contacts per company. forces you to think about who actually matters before sequencing.

polling at 15-30s intervals instead of websockets. for an operational dashboard, this is simpler and works fine.

**this is incomplete and that's the point.** i haven't sent a campaign through it yet. the data is seed data. sharing it now because i'll be updating it weekly as i add real data and live campaigns. the building process is the content.

repo: https://github.com/shawnla90/gtm-coding-agent (the dashboard is in `starters/signals-dashboard/`)

happy to answer questions about the Claude Code workflow or the architecture.

---

## r/GrowthEngineering / GTM Builders Variant

**Title:** building a GTM dashboard alongside my database. sharing it as it grows.

**Body:**

i've been building go-to-market systems with coding agents for the past few months. open-sourced a 10-chapter starter kit earlier this year.

this week i added a deployable dashboard to the repo.

**the context:** i use HubSpot and Instantly. this is not about replacing those tools.

i'm building my own database -- companies, contacts, intent signals, segments. writing signal logic that scores accounts based on engagement, LinkedIn activity, Reddit mentions, hiring patterns. designing segments that match how i actually think about my market.

the dashboard is just the visual layer on top of that work. it stays in sync because i built both sides. when i need a new view, i add it in 20 minutes instead of submitting a feature request.

**what it tracks:**

- company database with ICP scoring (0-100)
- 16 intent signal types with exponential decay scoring
- 3 ranked contacts per company (database-enforced limit)
- campaign segments computed live from your data
- domain health and send volume (for when i start sending)

**why share it incomplete:**

i haven't sent a single email campaign through this yet. the campaign pages show seed data.

i'm sharing it now because what you see today will look different next week when i start sending. and the week after when the signal pipeline is running on a cron. the building process is the learning, and i want to document it in real time.

**the thesis:** we are at the point where one person with a coding agent can build production tools alongside their existing stack. not to replace the SaaS. to understand what's happening under the hood and build the pieces that don't exist yet.

repo: https://github.com/shawnla90/gtm-coding-agent (`starters/signals-dashboard/` for the dashboard, chapter 11 for the walkthrough)

would love feedback. what would you add to a dashboard like this?

---

**Posting notes:**
- r/ClaudeAI: post first. lead with the Claude Code workflow. the community wants to see real non-coding use cases.
- r/GrowthEngineering / GTM builders: post 1-2 hours after r/ClaudeAI. lead with the building-alongside thesis.
- r/SaaS: use the general version above. lead with "i built alongside my tools, not instead of them."
- r/sales: use the general version. highlight the signal model and the 3-contact rule.
- Include the GitHub link in the body for Reddit (LinkedIn keeps links in comments)
- Reply to technical questions with specifics (share the actual scoring formula, table schemas, etc.)
- If someone asks "why not just use X tool" -- honest answer: i do use those tools. this is about understanding and building alongside, not replacing.
- Attach the video if the sub supports it, otherwise link to the GitHub README where it's embedded.

