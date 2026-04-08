# Blog Post: Drop #2 -- I Built a GTM Dashboard While Building My Database

**Publication:** shawnos.ai blog (Chapter 12 in the GTM Coding Agent series)
**Slug:** `/blog/gtm-dashboard-claude-code-supabase`
**Meta title:** I Built a GTM Dashboard While Building My Database | Claude Code + Supabase
**Meta description:** Drop #2 of the GTM Coding Agent starter kit. A signals dashboard built with Claude Code and Supabase, shared as it grows.

---

## the post

i built a GTM dashboard this week. 5 pages, signal scoring, campaign tracking, the works.

it's incomplete. and that's the whole point.

### why i'm sharing this now

i could wait. wait until I've sent my first email campaign through it. wait until the signal pipeline has run for a month and the data looks impressive. wait until it's "ready."

but the point of this repo has always been to share the work as it happens. drop #1 was 10 chapters on using coding agents for go-to-market. drop #2 adds a deployable dashboard starter and the chapter that explains how to build it.

what you see today will look different next week when i start actually sending emails. the campaign pages will have real data. the signal scoring will be tuned from live results. the segments will get sharper. that's part of the story.

### i still use HubSpot and Instantly

let me be direct about this: i'm not replacing my tools.

i use HubSpot as my CRM. i use Instantly for outbound sequences. i use Apollo for enrichment. those tools are good at what they do and i'm not pretending otherwise.

what i am doing is building my own database alongside those tools. i'm writing signal logic that scores companies based on intent data from LinkedIn, Reddit, and engagement. i'm designing segments that match how i actually think about my market. and now i'm building a dashboard that visualizes all of it.

the dashboard is the visual layer on top of work i'm already doing. it stays in sync because i built both sides.

### the stack: Claude Code + Supabase

the whole thing was built in a single Claude Code session.

- **Supabase** for Postgres. companies, contacts, signals, campaigns, send queue. 3 SQL files to set up the schema.
- **Next.js 16** with React 19 and TypeScript for the frontend.
- **shadcn/ui** and Tailwind v4 for the dark-themed UI.
- **Recharts** for the charts.
- **Python** for the signal scoring pipeline. exponential decay with a 14-day half-life, 16 weighted signal types, diversity bonuses.

5 pages:
1. **Campaigns** -- KPI cards, 24-hour send volume, domain health, active campaign metrics
2. **Database Intelligence** -- enrichment coverage, score distributions, pipeline stages
3. **Accounts Browser** -- searchable table with expandable rows showing contacts and mapped signals
4. **Signals** -- signal type distribution, source breakdown, top signal-rich companies
5. **Segments** -- live-computed campaign segments with preview tables

everything polls every 15-30 seconds. no websockets. for an operational dashboard that refreshes every few seconds, polling is simpler and it works.

### the signal model is the brain

this is the part i'm most interested in stress-testing with real data.

16 intent signal types, each weighted from 1 to 10. a "tool evaluation" signal (someone comparing vendors in your category) scores a 10. a "content engagement" signal scores a 3. all signals decay exponentially -- yesterday's signal is worth more than last month's.

the scoring formula:

```
score = weight * source_reliability * e^(-0.0495 * days_old)
```

14-day half-life. a signal from 2 weeks ago is worth half what it was on day one. a signal from 2 months ago is worth about 5%.

diversity bonuses reward breadth: +2 per distinct signal type, +3 per distinct source. a company with signals from 3 types and 2 sources scores higher than one with 10 identical signals from one place.

this is configurable. `pipeline/config.py` has the weights, thresholds, and reliability scores. tune them for your market.

### what's in the repo

the dashboard starter lives inside the GTM Coding Agent repo, not as a separate project. one `git clone` gets you everything.

```
starters/signals-dashboard/
  schema/          -- 3 SQL files (companies, campaigns, seed data)
  pipeline/        -- Python scripts (discover, score, load)
  src/             -- Next.js app (5 pages, 10 API routes, dark theme)
```

Chapter 11 walks through the architecture, the signal model, every page, and the pipeline.

3 Python scripts for the pipeline:
- `discover_companies.py` -- find companies via Exa API neural search
- `score_signals.py` -- score signals using exponential decay
- `load_to_supabase.py` -- upsert everything into Supabase with domain dedup

the pipeline is modular. swap Exa for Apollo, Clay, or a manual CSV and the rest still works.

### the 3-contact rule

one design decision worth calling out: the schema enforces a maximum of 3 ranked contacts per company. a Postgres trigger blocks a 4th from being added.

this is intentional. it forces you to rank your contacts by quality instead of dumping every email into a sequence. who is the decision maker? who is the champion? who is the technical evaluator? pick your best 3 and sequence those. the rest go into overflow for reference.

### what's next

this is where the repo goes from here:

- **email campaigns through the dashboard.** i haven't sent a campaign yet. when i do, the campaign pages will light up with real send volume, reply rates, domain health.
- **live signal pipeline.** right now the signals are seed data. next step is connecting the Exa discovery script to a cron and watching real intent data flow in.
- **tuning the scoring model.** the weights are my best guess. real data will tell me if a "hiring_signal" at weight 8 is right or if it should be a 5.
- **more segments.** the current segments are starting points. as i learn what correlates with replies, the segment logic will get sharper.

i'll be updating the repo as this happens. star it if you want to follow along.

### the thesis

we are getting to the point where a single person with a coding agent can build production tools on the spot. not prototypes. not demos. real things they use every day.

this is not saying SaaS tools are going away. it's saying the skill of building your own tools -- even small ones, even incomplete ones -- will carry you. when you understand what's happening under the hood, you're better at using the SaaS too.

i built this dashboard in one session with Claude Code. the whole thing. if i can describe what i need, i can ship it. and so can you.

### fork it

GitHub: https://github.com/shawnla90/gtm-coding-agent

the dashboard starter is in `starters/signals-dashboard/`. Chapter 11 has the full walkthrough. MIT license.

if you build on it, open a PR. i want to see what you make.

shawn, the gtme alchemist

---

**Publishing notes:**
- Embed the dashboard demo video at the top (assets/dashboard-demo.mp4)
- Link back to Drop #1 blog post for readers coming in fresh
- Cross-link to Chapter 11 in the repo
- Add to the shawnos.ai/guide/gtm-coding-agent web guide as the next chapter
