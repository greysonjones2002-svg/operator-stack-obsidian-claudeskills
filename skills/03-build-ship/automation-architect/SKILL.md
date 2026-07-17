---
name: automation-architect
description: >
  Takes a description of a manual, repeated process and turns it into a concrete automation
  design — the trigger, the steps, the tool that should run it, and a rough sense of how long it'd
  take to build. Use when the owner says "this process is manual and slow," "can this be
  automated," "I do this the same way every time," "I keep copy-pasting between X and Y," "every
  time [event happens] I have to [manual steps]," or describes any repeated multi-step task done
  by hand. This skill scopes and designs the automation — it maps the trigger/action/notification
  pattern and names the right tool (n8n, Zapier, Make, or a simple script) — but building the full
  automation usually requires tool-specific account setup and configuration the skill is honest
  about not being able to finish unattended in one sitting. Not for one-off tasks, anything
  requiring judgment calls a machine can't make, or processes touching sensitive data at a scale
  that needs real infrastructure.
---

# Automation Architect — Process-to-Automation Design

## Why this exists

Most "can this be automated" conversations die in vague enthusiasm — "yeah, probably, with
Zapier or something" — and then nothing gets built because nobody turned the process into an
actual spec. This skill exists to close that gap: take the manual process as the owner actually
does it, break it into trigger → action → notification (or the closest real variant of that
pattern), and name the specific tool and rough effort it would take. That's a deliverable the
owner can hand to themselves, a contractor, or come back to and finish, even if this session can't
finish the wiring.

Be honest about what this skill is: a design pass, not always a finished automation. Some
automations are simple enough to fully build and hand over in one sitting (a script, a single
Zapier zap with no branching). Others need account-specific setup — OAuth connections to the
owner's specific email/CRM/spreadsheet, testing against their real data — that can't be completed
without the owner sitting through the account-linking steps themselves. Scope honestly, every
time, and say which kind this one is before starting.

## When to fire

- "This process is manual and slow"
- "Can this be automated?"
- "I do this the same way every time"
- "I keep copy-pasting between [tool A] and [tool B]"
- "Every time [X happens], I have to [list of manual steps]"
- Owner describes any recurring task with a clear trigger and a repeatable set of steps — new
  lead comes in and gets logged somewhere by hand, an invoice needs to go out on a schedule, a
  form submission needs a reply, files need to move from one place to another after an event

Not a fit — say so and redirect:
- **One-off tasks.** If it happens once, automating it costs more time than doing it by hand.
  Automation pays off on repetition — ask how often this happens before treating it as an
  automation candidate.
- **Steps that need real judgment.** If any step is "look at this and decide," that's not a
  trigger/action automation, it's a decision — automating around it means either accepting worse
  decisions or building something that just flags the case for a human. Say which one the design
  assumes.
- **Sensitive data at real scale.** Automations touching health records, financial account
  numbers, or anything with real compliance exposure, run at meaningful volume, need actual
  infrastructure and probably a developer or a compliance-aware vendor — not a no-code tool
  wired together in an afternoon. Flag this plainly rather than quietly designing around it.
- **Anything needing custom infrastructure** — a webhook server with uptime guarantees, a
  database of record, anything where "the automation breaks silently" is a real business risk
  with no one watching it. No-code tools are fine for most solopreneur workflows; they are not
  fine as the backbone of something that can't fail quietly.

## How to do it

### Step 1 — pull context first

Check whatever context layer is available (owner-context notes, client files, prior process
documentation) for anything already known about this workflow, the tools currently in the
owner's stack, and prior automation attempts that succeeded or failed. Don't re-ask what's
already on file — but do confirm it's still accurate, since manual processes drift.

### Step 2 — get the process exactly as it's actually done

Ask the owner to walk through the current manual version step by step, not the idealized version.
The real process usually has exceptions and workarounds that matter:

1. **What starts it?** A specific, nameable event — an email arrives, a form gets submitted, a
   date/time passes, a file lands somewhere, a status changes in some tool.
2. **What are the exact steps taken by hand right now?** In order, including the boring ones —
   "I open the spreadsheet, find the row, copy the email, paste it into..."
3. **Where does information live at each step?** Which tools, which spreadsheets, which inboxes.
4. **What ends it?** What does "done" look like — a notification sent, a record updated, a file
   moved, a task closed.
5. **What goes wrong today?** Exceptions, edge cases, things that require a judgment call. These
   either need to be handled in the automation logic or explicitly routed to a human — name which.
6. **How often does this happen, and how long does it take by hand?** This is what justifies (or
   doesn't) building the automation at all.

### Step 3 — map it to the pattern

Almost every solopreneur automation is a variant of:

**Trigger → Action(s) → Notification/Record**

- **Trigger**: the specific event that starts it (form submission, new email matching a filter, a
  scheduled time, a new row in a sheet, a status change).
- **Action(s)**: what happens automatically — data gets moved/transformed, a message gets sent, a
  record gets created, a file gets generated.
- **Notification/Record**: how the owner (or the customer) knows it happened — an email, a Slack
  message, a logged row, an updated status.

Name each part explicitly. If a step doesn't fit cleanly (there's a judgment call in the middle),
call that out as a branch point that either needs conditional logic (still doable in most no-code
tools) or a human-in-the-loop step (the automation does the tedious parts and stops to ask).

### Step 4 — name the tool and be honest about effort

- **A single script** (something Claude can write directly, run in a scheduled job, or trigger
  manually) fits when the whole thing lives in one place the owner already has file/shell access
  to — e.g., renaming and organizing files, generating a report from data already on disk,
  reformatting a spreadsheet. No external accounts required, so this can often be fully built and
  handed over in the same sitting.
- **Zapier** fits simple, mostly linear automations connecting two or three well-known apps
  (Gmail, Google Sheets, Calendly, Slack, Stripe, a CRM). Fastest to set up, most limited on
  complex branching, has a free tier for very light use and paid tiers that scale with volume.
- **Make** (formerly Integromat) fits automations with more branching logic, multiple conditional
  paths, or where Zapier's per-step pricing gets expensive at volume. Steeper learning curve than
  Zapier, more visual/flexible.
- **n8n** fits when the owner wants more control, is comfortable with a slightly more technical
  interface, wants to self-host to avoid subscription costs, or the automation needs custom code
  steps mixed with no-code steps. Free if self-hosted, otherwise a paid cloud tier.

For each recommendation, give a rough scope estimate: "this is a 15-minute build once you connect
your Gmail and Sheets accounts" versus "this needs three connected apps, two conditional branches,
and testing against real submissions — budget an hour, plus troubleshooting."

### Step 5 — build what can be built now, hand off what can't

- If it's a pure script with no external account dependencies, write it now, test it against
  sample data the owner provides, and hand over working code plus plain-language instructions for
  running it.
- If it needs Zapier/Make/n8n with the owner's own accounts, this skill cannot log into the
  owner's Gmail/CRM/Stripe on their behalf. What it CAN do: give the owner a precise, step-by-step
  build sheet — trigger app and event, each action step in order with the exact fields to map,
  and what the notification step should say — so the owner (or anyone helping them) can build it
  in the tool's UI in one sitting without having to figure out the logic from scratch.
- Flag clearly which parts, if any, will need the owner to test with real data before trusting the
  automation unattended — most no-code automations should run in a monitored/test mode for the
  first several real triggers before being trusted silently.

### Step 6 — write back

Log the process as documented (it's often the first time it's been written down at all — valuable
on its own even if the automation never gets built), the design decision (which tool, why), and
the build sheet or the finished script as an action item / reference file. This is exactly what
the foundation capture layer is for — a half-finished automation design is worth nothing if it
evaporates at the end of the session.

## Worked example

**Owner says:** "Every time someone books a call through my Calendly, I have to manually go add
them to my client spreadsheet and send them a welcome email with my intake form attached. I
forget half the time."

**Process as described:**
1. Trigger: someone books a call in Calendly.
2. Manual steps today: owner checks Calendly, copies the name/email into a Google Sheet, then
   manually writes and sends a welcome email with an intake form link attached, from memory.
3. Ends when: welcome email is sent and the row exists in the sheet.
4. Exceptions: sometimes owner is busy and this doesn't happen for a day or two, which looks bad
   to new clients.
5. Frequency: 3-5 times a week, takes about 5 minutes each time when remembered, costs a bad first
   impression when forgotten.

**Design:**
- Trigger: new Calendly booking (Calendly has a native trigger for this).
- Action 1: create a new row in the Google Sheet with name, email, booking time (direct field
  mapping, no branching needed).
- Action 2: send a templated welcome email with the intake form link, via Gmail or the email
  provider already in use.
- Notification: none needed beyond the email itself being the notification to the client; owner
  can also add a Slack/email ping to themselves confirming it fired.

**Tool recommendation:** Zapier. Three connected apps (Calendly, Google Sheets, Gmail), no
conditional branches, this is close to a template Zapier already has pre-built for. Estimated
build time once accounts are connected: 10-15 minutes.

**What got handed to the owner:** a step-by-step build sheet naming the exact trigger app/event,
the two action steps with field mappings, and the suggested welcome email copy — plus a note to
run it in test mode against the owner's own next booking before trusting it fully. Logged the
process documentation and the open "build this zap" task.

## Scope reminder

If the process touches something with real compliance weight (health information, payment card
data beyond a standard processor's hosted checkout, anything where a silent failure has legal
exposure), stop and say plainly that this needs infrastructure and oversight beyond a no-code tool
wired together in a sitting — that's a developer and possibly a compliance review, not this skill.
