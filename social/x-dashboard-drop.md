# X Posts -- Dashboard Drop

---

## Main post (with video)

Claude Code + Supabase = GTM dashboard.

built this in one session. 5 pages. signal scoring. campaign tracking. dark theme.

i still use HubSpot and Instantly. this is not about replacing tools.

i'm building my database and my signal logic. the dashboard is just the visual layer on work i'm already doing. it stays in sync because i built both sides.

it's incomplete. and that's the point. what you see today will look different next week when i start sending campaigns.

sharing it as it grows.

fork it: github.com/shawnla90/gtm-coding-agent

[attach: dashboard-demo.mp4]

---

## Thread (optional, post as replies to the main)

**Reply 1:**
the signal model is the interesting part.

16 intent signal types. each weighted differently.

tool_evaluation = 10
vendor_switch = 10
hiring_signal = 8
pain_expression = 7
content_engagement = 3

all decay exponentially. 14-day half-life. yesterday's signal > last month's signal.

**Reply 2:**
the 3-contact rule.

the database enforces a max of 3 ranked contacts per company. a Postgres trigger blocks a 4th.

forces you to ask: who is the decision maker? who is the champion? who is the technical evaluator?

pick your best 3. sequence those.

**Reply 3:**
the stack:

- Next.js 16 + React 19 + TypeScript
- Supabase (Postgres)
- Tailwind v4 + shadcn/ui
- Recharts
- Python for the signal pipeline

~40 files. MIT license. chapter 11 has the full walkthrough.

**Reply 4:**
this is drop #2 of the GTM coding agent starter kit.

drop #1: 10 chapters on building GTM with coding agents
drop #2: deployable dashboard + signal scoring

drop #3 will have live campaign data.

star the repo if you want to follow along.

---

**Posting notes:**
- Post the main tweet with the video attached (mp4 renders natively on X)
- Thread the replies only if the main post gets traction (50+ impressions in first hour)
- Best times: 8-10am EST or 12-2pm EST, Tuesday-Thursday
- Pin to profile for a few days
- The hook "Claude Code + Supabase = GTM dashboard" is the equation format that performed well on drop #1
