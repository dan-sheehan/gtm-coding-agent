# LinkedIn Post — Dashboard Drop

---

Claude Code + Supabase = GTM dashboard.

built this in one session. open-sourcing it today.

the setup: Next.js + Supabase + a signal scoring engine in Python. 5 pages. dark theme. real-time polling.

what it tracks:
- company database with ICP scoring (0-100)
- intent signals from LinkedIn, Reddit, and engagement data
- contact ranking (top 3 per company, enforced at the database level)
- campaign segments computed live from your data
- domain health, send volume, bounce rates

the signal model is the interesting part. 16 intent signal types, each weighted differently. a tool evaluation signal (someone comparing vendors) scores 10. a content engagement signal scores 3. all signals decay exponentially with a 14-day half-life. yesterday's signal is worth more than last month's.

this is drop #2 of the GTM coding agent starter kit.

drop #1 was 10 chapters on building GTM with coding agents. context engineering, Python for GTM, voice DNA, automation.

drop #2 adds the dashboard starter + a new chapter on building it. fork the repo, set up Supabase, run 3 SQL files, and you have a working dashboard in 10 minutes.

the thing is, i still use HubSpot and Instantly. this is not about replacing those tools.

i'm already building my database, writing my signal logic, designing my segments. the dashboard is just the visual layer on top of work i'm already doing. it stays in sync because i built both sides.

and this is incomplete. what you see today will look different next week when i start sending actual email campaigns. that's the point. i'm sharing it as it grows because the building process is the learning.

the skill of being able to build your own tools will carry you. even if you use the SaaS, understanding what's happening underneath makes you better at the job.

who this is for:
- GTM engineers who want to build, not just buy
- founders doing their own outbound
- SDRs who want to understand the data behind their sequences
- anyone curious about what a production dashboard actually looks like under the hood

the full stack: Next.js 16, React 19, TypeScript, Tailwind v4, shadcn/ui, Recharts, Supabase Postgres. ~40 files. MIT license.

fork it. make it better. open a PR if you build something cool.

link in comments.

shawn, the gtme alchemist

---

**First comment:**

GitHub link: https://github.com/shawnla90/gtm-coding-agent

chapter 11 + the full dashboard starter are in `starters/signals-dashboard/`. fork it and `npm run dev`.

---

**Posting notes:**
- No links in post body (kills reach)
- Reply to every comment in the first 2 hours
- If people ask about the signal model, explain the decay formula
- If people ask about alternatives to Exa, point to Apollo/Clay/manual CSV
- Pin the link comment
- Post between 8-10am EST Tuesday or Wednesday
- Attach the dashboard demo video (assets/dashboard-demo.mp4) -- native video gets better reach than image
- If you can't attach video, post a screen recording natively through LinkedIn's video upload
- The hook "Claude Code + Supabase = GTM dashboard" is the equation format that performed on drop #1

