---
name: quick-site
description: >
  Builds a real, working single- or few-page website from a plain description of what it needs to
  say and do — a landing page, a simple services/portfolio page, an event or launch page. Use when
  the owner says "I need a landing page," "build a site for [thing]," "I need a page for
  [offer/event/product]," "can you make me a simple website," or describes wanting an online
  presence for something specific and time-bound. Writes real HTML/CSS/JS the owner can host
  anywhere. Asks clarifying questions about audience, goal, and must-have sections before writing
  code. Does NOT register domains, buy hosting, or manage accounts on the owner's behalf — hands
  back a clear checklist of what the owner needs to do themselves to go live. Not for multi-user
  apps, logins, payments processing, or anything needing a database or backend — flag those as
  outside scope and say so plainly.
---

# Quick Site — Single-Page and Small Site Builder

## Why this exists

Most solopreneurs don't need a web developer, a website builder subscription, or a six-week
project to get one page live that says what they do and how to reach them. They need a landing
page for a launch, a one-pager for a new offer, a simple services page, or an event page — built
fast, built right, and handed over as files they own outright. No platform lock-in, no monthly
site-builder fee, no waiting on an agency.

This skill is scoped narrowly on purpose: one to five static pages, no login, no database, no
payment processing. That covers the large majority of what a solopreneur actually needs a website
for. Anything past that is a different, bigger project — this skill says so instead of quietly
overbuilding.

## When to fire

- "I need a landing page for [product/offer/event]"
- "Build a site for [business name]"
- "I need a page for [thing] — something people can find and see what it's about"
- "Can you make me a simple website / portfolio page / services page"
- Owner describes wanting to point people somewhere online — a link in a bio, a QR code on a
  flyer, an ad landing destination — and doesn't currently have a page for it

Not a fit — say so and redirect:
- Anything requiring user accounts, logins, or saved user data → that's an app, not a site. Flag
  it and recommend an actual developer or a dedicated platform (e.g., a proper SaaS starter, not a
  static site).
- Payment processing beyond a link-out to Stripe/PayPal checkout → linking out is fine, building a
  custom checkout flow is not.
- E-commerce with inventory, cart, multi-product catalog → that's a real application; point to
  Shopify, Squarespace Commerce, or a developer, not this skill.
- Content that needs to update itself dynamically (live data, user-generated content, a blog with
  a CMS) → static HTML can't do this well; say so and suggest a CMS platform if that's the real
  need.

## How to do it

### Step 1 — pull context first

If a vault/context layer is available (owner-context files, prior client or project notes), check
it before asking questions the owner has already answered elsewhere — existing brand language, a
prior offer description, a logo or color reference already on file. Don't make the owner repeat
themselves.

### Step 2 — ask before building

Do not start writing code on a vague request. Ask (briefly, not a 20-question form):

1. **Who is this for?** Who lands on this page, and how did they get there (ad, referral, QR
   code, social bio link)?
2. **What's the one action you want them to take?** Book a call, buy something, sign up, call a
   number, fill a form. A page trying to do five things does none of them well — push toward one
   primary call to action.
3. **What sections are non-negotiable?** Common ones: headline/value prop, what you offer, social
   proof (testimonials, logos, results), pricing or packages, FAQ, contact/booking, footer with
   real contact info.
4. **Any existing brand material?** Logo, colors, fonts, existing copy, a competitor site they
   like the feel of. Use what exists — don't invent a new brand identity as a side effect of
   building a page.
5. **Timeline pressure?** If this needs to be live today for an event tomorrow, say so up front —
   it changes how much polish is worth chasing versus just shipping.

Skip questions the context layer already answered. Don't skip questions it didn't.

### Step 3 — build it

- Plain HTML/CSS/JS, no framework, no build step, no `npm install`. A single `index.html` (plus
  `style.css` and a small `script.js` if there's real interactivity — a mobile nav toggle, a form
  validation, a smooth scroll) is the default. Multi-page sites get one HTML file per page with a
  shared stylesheet.
- Mobile-first. Most traffic to a landing page is a phone. Check the layout collapses cleanly
  before calling it done.
- Real copy, not lorem ipsum. Write actual headline and body copy based on what the owner told
  you. If they gave partial copy, extend it in their voice, don't replace it with generic
  marketing language.
- Keep it fast: no heavy JS libraries for a static page, optimize or placeholder-flag any images,
  no auto-playing video/audio.
- Include basic on-page SEO: a real `<title>`, a meta description, one `<h1>`, alt text on images.
  Costs nothing to do right the first time.
- Include a working contact path — a `mailto:` link, a tel: link, or a form that posts to a
  service the owner can actually receive submissions from (see the "form that logs somewhere"
  note below — form handling needs a backend or a third-party form service; plain HTML forms
  don't send email by themselves).
- Save the files somewhere the owner can find them, and note the path back in the session.

### Step 4 — tell them what YOU didn't do

This is the part that gets skipped and shouldn't be. After the files are built, give a plain
checklist of what's still required to make the page live, and be explicit that these steps need
the owner's own accounts and can't be done on their behalf without their login:

- **Domain**: do they have one already? If not, they need to buy one (a registrar — the specific
  choice doesn't matter much, price and renewal terms do). This skill can suggest options and
  explain the process but cannot purchase a domain — that requires the owner's payment method and
  account.
- **Hosting**: for a static site like this, cheap or free options exist (a static host, or
  wherever they already have hosting). Explain the option that fits their situation, but don't
  assume — ask if they already have hosting before recommending a new account.
- **DNS**: pointing the domain at the host requires access to wherever the domain is registered.
  Walk through the steps in plain language; don't attempt to log into their registrar.
- **Form handling** (if the page has a contact/lead form): a static page cannot email itself.
  Either point the form at a third-party form-handling service, or wire it to a simple
  automation (this is where `automation-architect` picks up — a form submission triggering a
  notification is a textbook automation, not a website feature).
- **Analytics** (optional): if they want to know if the page is working, a simple analytics
  snippet can be added — ask if they want it before adding tracking scripts of any kind.

### Step 5 — write back

Log what was built and where, and add the "what's left to go live" checklist as action items —
this is exactly the kind of decision and next-step list the foundation capture layer exists to
hold onto, so it doesn't get lost between this session and whenever the owner actually buys the
domain.

## Worked example

**Owner says:** "I need a landing page for a workshop I'm running next month — 'Pricing Your
Freelance Work,' it's a paid 90-minute session, $75, on Zoom."

**Clarifying questions asked:**
- Who's the audience? → Freelancers who undercharge and don't know how to fix it.
- One action? → Get them to click through to a checkout/registration link (owner already has a
  payment link from their existing invoicing tool).
- Must-have sections? → What you'll learn, who it's for, date/time, price, a short bio, an FAQ
  about refunds and recordings.
- Brand material? → Owner has a logo and generally uses a dark green/cream color scheme on
  Instagram.
- Timeline? → Needs to be shareable by tomorrow.

**What gets built:** a single `index.html` with `style.css`, dark green/cream palette matching
their Instagram, headline built from their workshop pitch, a details block (date, time, price,
platform), a short "what you'll walk away with" list, an FAQ section, and a prominent button
linking straight to their existing payment link — no custom form needed since the checkout already
exists elsewhere.

**Handback checklist given to the owner:**
- Domain: none yet — recommend buying one if this becomes a recurring workshop series, otherwise a
  free static host with a subdomain is fine for a one-off.
- Hosting: point to a couple of simple no-cost static hosting options and explain the account
  creation and file-upload steps in plain language.
- No form needed — the page links straight to the existing payment/registration link, so no
  automation build-out required this time.
- Logged the build and the open "pick a host and go live" task to the owner's task list.

## Scope reminder

This skill ships a page, not a business. If the request grows into "and I want people to create
accounts" or "and I want to sell multiple products with a cart," stop, name that this has become a
different and larger project, and say plainly that it needs either a dedicated e-commerce/app
platform or an actual developer — building it ad hoc as static HTML would be unsafe or unworkable
past this point.
