---
name: content-engine
description: >
  Looks at what's actually working — sales data, best-performing past content, or the owner's
  description of recent wins — and turns it into a focused 2–4 week content/outreach plan built on
  evidence, not a generic 30-post calendar with no strategic basis. Use when the owner asks "what
  should I post," "content plan," "what's selling," or wants direction on where to put content effort
  next. Works from sales/order exports, screenshots or descriptions of top-performing posts, or the
  owner's own account of what's been landing — no analytics connector required. If a
  social/analytics/sales connector is available, pull performance data directly; otherwise ask the
  owner what's sold well or performed well recently. Explicitly names what to stop doing, not just
  what to start.
---

# Content Engine

## Why this exists

A 30-day content calendar with a slot for every platform every day is busywork, not strategy — it
treats all content as equally valuable and gives the owner no reason to believe any of it will work.
This skill starts from the opposite direction: what has actually sold, engaged, or converted
recently, and builds a short plan around doing more of that and less of everything else. A plan the
owner can execute in the next 2–4 weeks beats a calendar they'll abandon by week two.

## When to fire

- "What should I post"
- "Content plan" / "what's my content strategy this month"
- "What's selling" (as a lead-in to figuring out what to promote)
- Owner wants direction on where to focus content or outreach effort next

## How to do it

### Step 1 — find the evidence

Content plans built on vibes are why most of them fail. Pull real signal first:
- Sales/order data — what actually sold in the last 30–90 days (a CSV export, a screenshot, or the
  owner just naming top sellers)
- Best-performing past content — posts, emails, or listings that got real engagement or conversions,
  not just what the owner remembers liking
- If a social/analytics/e-commerce connector is available, pull the numbers directly
- If not, ask directly: "What sold well recently? What's the one post or email in the last few
  months that actually got a response — replies, shares, sales, bookings?"

Also check `journal/` and `memory/clients/` (via `operator-prime`) for any mentioned wins that
didn't make it into formal data — a client comment, a word-of-mouth referral spike, a product that
kept coming up in conversation.

### Step 2 — separate signal from noise

Not everything that got posted is evidence of what works. Distinguish:
- **Real signal**: content that drove a measurable outcome (sale, booking, reply, share by someone
  outside the owner's existing audience)
- **Noise**: content that existed but produced no discernible response — don't build a strategy
  around repeating it just because it's the most recent thing in the feed

If there isn't enough data to find a clear signal, say so and default to the strongest hypothesis
available (e.g., "no strong existing signal — recommend testing 2 angles over the next 2 weeks and
tracking which gets response, rather than committing to a full month on either").

### Step 3 — build the plan around what to push AND what to drop

A useful plan says both. If a service, product line, or content angle has been getting attention
but the owner's been spending equal time on three other things that get nothing, the plan should
say explicitly: put more time here, stop spending time there.

### Step 4 — output format

```
CONTENT PLAN — [date] to [date] (3 weeks)

What's working (the evidence):
- [Specific product/service/angle] — [specific evidence: "3 of last 5 sales came from referrals
  mentioning the workshop," "the before/after post got 4x the engagement of anything else this
  quarter"]
- [Second signal, if one exists]

What to push these 3 weeks:
- Week 1: [specific content/outreach action tied directly to signal above] — e.g., "post a
  behind-the-scenes on the workshop process, since that's what's driving referral conversations"
- Week 2: [specific action]
- Week 3: [specific action]

What to stop or scale back:
- [Specific thing the owner's been doing that isn't producing evidence of working] — stated plainly,
  not softened. If it's genuinely unclear whether it's working, say "not enough data, hold steady
  and measure" rather than a false stop/go call.

Watch for:
- [The specific metric or signal that would confirm this plan is working, e.g., "if the
  behind-the-scenes post gets 2+ inbound DMs, that confirms the angle — plan week 4 around it"]
```

3–5 concrete actions across the window beats 20 scheduled posts with no reasoning behind any of
them. If the owner wants more volume, expand within the same evidence-backed angles rather than
padding with unrelated generic content.

## Handoff

Pull sales/engagement history and prior journal mentions of what's landed via `operator-prime`
before building the plan. After the plan is set, log it to `journal/YYYY-MM-DD.md`, add the
week-by-week actions to `TASKS.md`, and if the plan reveals a durable insight about what the
business's audience responds to, write it to `memory/context/you.md` so future plans start from it
instead of re-deriving it — via the `capture-everything` pattern.

## What this skill does not do

- Never produces a generic content calendar with no evidence behind the choices
- Never posts, schedules, or publishes anything directly — output is a plan for the owner to execute
- Never treats posting volume as a strategy on its own — every recommended action ties back to a
  stated piece of evidence
