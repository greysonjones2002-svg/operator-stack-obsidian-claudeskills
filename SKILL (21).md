---
name: tool-builder
description: >
  Builds small, single-purpose internal tools for one owner's own use — a pricing calculator, a
  simple tracker, a form that logs submissions to a spreadsheet, a quick converter or estimator.
  Use when the owner says "I need a calculator for," "I need a tracker for," "can you build me a
  simple tool that," "I need a form for [thing] that saves the answers somewhere," or describes
  wanting a small piece of software to do one specific repeatable job for themselves or their
  team. Produces plain code (usually a single HTML file with embedded JS, or a short script) the
  owner doesn't need to maintain beyond asking Claude to change it later. Scoped tightly to
  internal, single-purpose tools — NOT for building a product to sell to others, which is a much
  bigger conversation this skill should name explicitly if asked, not attempt to solve inline.
---

# Tool Builder — Small Internal Tools

## Why this exists

A lot of the software a solopreneur actually needs day to day is small: "how much should I quote
this job," "what jobs are still open," "did this client pay yet." These don't need a SaaS
subscription or a custom app — they need twenty lines of logic wrapped in a page that's easy to
open and use. This skill builds exactly that: a single-purpose tool, built once, owned outright,
changeable later just by asking.

The tight scope is the point. A calculator that computes one thing well and is easy to change six
months from now beats a half-built platform that tries to do five things and breaks when the
owner's process shifts. If the ask grows into "and other people should be able to use this too" or
"and I want to charge for this," that's a different project — this skill says so rather than
quietly scope-creeping into it.

## When to fire

- "I need a calculator for [pricing/quoting/estimating something]"
- "I need a tracker for [jobs/clients/inventory/hours]"
- "Can you build me a simple tool that [does one specific repeatable job]"
- "I need a form for [thing] that saves the answers somewhere I can see them"
- Owner describes wanting to stop doing a small repeated calculation or lookup by hand or in a
  messy spreadsheet, for their own use

Not a fit — say so and redirect:
- **A product meant to be sold or used by other businesses/customers.** That's a real software
  product with real requirements — multi-tenant data separation, security review, support,
  versioning. Name this explicitly the moment it comes up and don't try to solve it as a quick
  build. Point toward a proper development engagement instead.
- **Anything storing other people's sensitive data at scale** (customer PII beyond a name and
  email, payment details, health information). A simple tool logging a client's name and a quote
  amount to a spreadsheet the owner alone can see is fine. A tool meant to hold sensitive records
  for many people needs real data handling practices this skill doesn't provide.
- **Multi-user tools with logins, permissions, or concurrent editing.** The moment a tool needs
  "who's allowed to see what" logic, it has crossed from a script into an application. Flag it.

## How to do it

### Step 1 — pull context first

Check the available context layer for relevant numbers already on file — pricing structure,
service list, past quotes, existing tracker formats the owner has used before (even a messy
spreadsheet). Reuse real numbers and real categories instead of inventing placeholder ones.

### Step 2 — scope the one job this tool does

Ask directly, and resist letting the answer sprawl:

1. **What's the one thing this needs to do?** State it as a single sentence — "calculate a quote
   from square footage and job type," "log a new client and show which ones haven't paid,"
   "convert hours logged into an invoice total."
2. **What are the inputs?** Every field the tool needs, and where those numbers currently come
   from (owner's head, a price list, a spreadsheet).
3. **What's the output?** A number, a list, a saved record, a generated summary — be specific.
4. **Where does data need to live?** Does this need to remember anything between uses (a tracker,
   a log) or is it stateless (a calculator that just computes and shows a result each time)?
   Stateless is simpler — don't add storage the tool doesn't need.
5. **Who uses it, and on what?** Just the owner, on their laptop? Also on a phone? This affects
   layout, not architecture — it's still a single file either way.

### Step 3 — pick the right shape

- **Stateless calculator/converter/estimator**: a single HTML file with embedded CSS and
  JavaScript. Inputs, a calculation, a displayed result. No storage needed. This is the simplest
  and most common case — build it as one self-contained file the owner can open by double-clicking,
  no server required.
- **Tracker that remembers entries between sessions, single user, single device**: same single
  HTML file, but store entries in the browser's local storage so they persist between visits
  without needing any backend. Simple, free, works offline, but data lives only in that one
  browser on that one device — say this limitation out loud.
- **Form that needs to log submissions somewhere durable, or be accessible from multiple
  devices**: this needs somewhere to actually write data — a spreadsheet via a simple
  integration, or a lightweight backend. If the owner already has a spreadsheet-based workflow, the
  cleanest path is usually wiring form submissions to append rows to a sheet — which is an
  automation, not just a tool. Hand this specific piece to `automation-architect` to design the
  trigger/action, and come back here only for the front-end form itself. Don't build a custom
  database-backed backend for something a spreadsheet handles fine — that's over-engineering a
  simple need.

### Step 4 — build it plainly

- Write real, working code — not a mockup. Test the calculation or logic against a couple of
  real numbers the owner would actually enter, and show the result back to them before calling it
  done.
- Comment the code lightly where the logic isn't obvious (a pricing formula, a rounding rule) so
  that asking Claude to change it later is fast and accurate — the owner never needs to read the
  comments themselves, they're there so future changes stay correct.
- Keep it to the smallest reasonable number of files. One HTML file beats an HTML file, a CSS
  file, and a JS file for something this size — fewer files means fewer things to lose track of.
- Make the update path explicit to the owner in plain language: "to change the price per square
  foot, tell Claude the new number and which tool this is — it's a one-line change." They should
  never feel like they need to touch code themselves.

### Step 5 — write back

Log what was built, where the file lives, and what it does — plus any open follow-up (e.g., "this
tracker only saves data on this laptop, flag if that becomes a problem"). If real business numbers
were used (a price list, a rate), and those aren't already recorded in the context layer, this is
also the moment to capture them there — a pricing calculator is often the first time a rate
structure gets written down anywhere durable.

## Worked example

**Owner says:** "I quote landscaping jobs based on square footage and whether it's a one-time
cleanup or a recurring contract, but I keep doing the math wrong in my head. Can you build me a
calculator?"

**Scoping:**
- One job: take square footage and job type, output a quote.
- Inputs: square footage (number), job type (one-time cleanup vs. recurring contract — different
  rate structures), and the owner confirms their actual current rates: $0.35/sq ft for one-time,
  $0.20/sq ft/month for recurring with a 3-month minimum.
- Output: a dollar figure, and for recurring jobs, the 3-month minimum total shown alongside the
  monthly rate.
- Storage: none needed — stateless, just compute and display.
- Used on: owner's phone, standing in a client's yard.

**Build:** a single `landscaping-quote.html` file — two inputs (square footage, a toggle for job
type), a calculate button, a result display showing the quote (and the 3-month minimum total for
recurring jobs), styled to be readable and tappable on a phone screen. Tested against a 2,000 sq
ft one-time job ($700) and a 1,500 sq ft recurring job ($300/month, $900 minimum) with the owner
confirming both matched their own mental math.

**Write-back:** logged the file location, the exact rate structure used ($0.35/sq ft one-time,
$0.20/sq ft/month recurring, 3-month minimum) into the owner's context notes since it wasn't
written down anywhere before, and noted the update path ("tell Claude the new rate and which
calculator, it's a one-line change") so the owner doesn't need to touch the code directly next
time rates change.

## Scope reminder

If asked to make a tool "so other landscapers could use it too" or "and charge people $10/month
for it," stop and name that plainly: that's a real product with real requirements (multiple
users, billing, support, a much longer build) — not a variation on this single-purpose tool. Flag
it as a separate, bigger conversation rather than trying to bolt multi-tenant features onto a
one-file calculator.
