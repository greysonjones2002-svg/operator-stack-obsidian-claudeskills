---
name: outreach-drafts
description: >
  Drafts cold outreach and follow-up messages (email, LinkedIn, DM) in the owner's own voice, pulling
  whatever is known about the recipient from the vault or from what the owner pastes/describes. Use
  when the owner says "draft an email to," "follow up with," "reach out to," "write a cold email,"
  or pastes a thread and asks for a reply. Produces 2–3 short variants for cold outreach so the owner
  has real options, not one take-it-or-leave-it draft; follow-ups can be a single draft since the
  context is narrower. If an email/CRM connector is available, use it to pull thread history or send
  status directly; otherwise ask the owner to paste the prior thread or describe what's known about
  the person. Never sends anything — every output is a draft placed for the owner to review, edit,
  and send themselves.
---

# Outreach Drafts

## Why this exists

Generic cold email is easy to spot and easy to ignore. The difference between a message that gets a
reply and one that gets deleted is almost always specificity — a real detail about the person or
company, and a voice that sounds like an actual human, not a template. This skill exists to make
that specificity fast to produce instead of a 20-minute stare-at-blank-page exercise every time the
owner needs to reach out to someone.

## When to fire

- "Draft an email to [name]"
- "Follow up with [lead/client]"
- "Reach out to [company/person]"
- "Write a cold email for [offer/campaign]"
- Owner pastes a thread and says "help me respond" or "what should I say back"

## How to do it

### Step 1 — gather context

Pull what's known about the recipient before writing anything:
- Check `memory/clients/` and `memory/people/` (via `operator-prime`) for any existing file on this
  person or company
- Check `journal/` for prior mentions — a call, a comment, a status change
- If an email or CRM connector is available, pull the actual thread history directly
- If none of that exists or connects, ask the owner directly: "What do you know about them? Paste
  the last email if there's a thread, or just describe the situation."

Never fabricate a detail about the recipient to sound personal. If there's nothing specific to work
with, say so and draft from the offer/value prop instead of inventing a fake personalization.

### Step 2 — match the owner's voice

Read `memory/context/preferences.md` for tone/voice notes if present. In the absence of an explicit
voice guide, infer from any writing samples in the vault (past journal entries, prior sent emails
pasted into the vault) rather than defaulting to generic "professional" tone. Flag it once if no
voice signal exists at all: "I don't have a voice sample for you yet — this draft is a reasonable
default, tell me what to adjust and I'll remember it for next time."

### Step 3 — draft

**Cold outreach → always produce 2–3 short variants**, not one draft. Vary the angle, not just the
wording:
- One that opens with a specific observation about them/their business
- One that opens with the problem/pain point directly
- One that's shorter and leads with a direct ask (works better for busy/senior recipients)

Keep cold emails short — 60–120 words. Nobody reads a five-paragraph cold email from a stranger.

**Follow-ups → one draft is fine**, since the context (prior thread, what was said, how long it's
been) narrows the options. Match tone to how the relationship has gone so far — a follow-up to a
warm lead who went quiet reads differently than a follow-up to someone who just asked a question.

### Step 4 — sample output format

```
Draft 1 (specific-observation opener):
Subject: quick one on [specific detail]

Hey [Name],

Saw [specific, real detail — a launch, a hire, a post, a mutual connection]. [One line connecting
that to the problem you solve.]

[One line of concrete value — not "we help businesses grow," but the actual mechanism.]

Worth a 15-minute call next week, or should I just send over a couple examples?

[Owner's name]

---

Draft 2 (problem-first opener):
Subject: [specific pain point]

Hey [Name],

Most [their role/industry] I talk to are dealing with [specific problem]. Is that live for you right
now, or has it already been solved?

If it's live — happy to share what's worked for others in [space]. No pitch, just comparing notes.

[Owner's name]

---

Draft 3 (short + direct ask):
Subject: [company] + [owner's company]

[Name] — [one line: who you are, one line: the specific reason you're reaching out]. Worth 10
minutes?

[Owner's name]
```

Always label which variant is which and why it differs — the owner should be able to pick based on
the recipient's seniority/relationship, not just gut feel on which sounds better.

## Handoff

Read recipient/client context via `operator-prime` before drafting (memory/clients/, memory/people/,
journal/). After the owner picks and sends a draft, log the outreach — who, what was sent, when — to
the relevant `memory/clients/` or `memory/people/` file and note it in `journal/YYYY-MM-DD.md`, via
the `capture-everything` pattern. If a reply is expected, add a follow-up task to `TASKS.md` with a
date.

## What this skill does not do

- Never sends an email, DM, or message on its own — output is always a draft for the owner to copy,
  edit, and send
- Never invents personal details about a recipient to fake specificity
- Never produces a single generic template dressed up with a mail-merge field for cold outreach —
  variants must differ in substance, not just the greeting line
