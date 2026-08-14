# Modren Client Acquisition (MCA)

A single, deep context document for this project. This is the only markdown file the repo needs. Keep it current instead of spawning new `.md` files.

Built by Abhinav Dunna, Founder of Autometa AI.

> Naming note: the project was previously called "Modern Signal Driven Leads Engine". It is now **Modren Client Acquisition (MCA)** everywhere: the HTML title, nav logo, breadcrumb, footer, and the repo slug `modren-client-acquisition`.

## 1. What this project is

A signal-driven B2B outbound system, designed as one system with two uses:

1. Run Autometa's own outbound to win clients.
2. Productize the same architecture and sell it to clients as a done-for-you "leads engine".

It is not nine separate tactics. It is one connected pipeline:

Detect a buying signal → identify the account → waterfall-enrich the contact → qualify against the ICP → score → reach on the right channel with the right angle → warm → convert → revive the no's, with a shared database and a scoreboard running underneath the whole thing.

The current deliverable is an interactive HTML blueprint (`index.html`) that documents this system stage by stage. It is a working document/app, not the automation itself. The automation gets built later against this blueprint.

## 2. Current status

`index.html` is a self-contained, single-file interactive blueprint. It is done for v1:

* Clean light UI (blue/teal/gold, dark hero) matching Autometa's existing "Murshid" product-doc style.
* 8 stages + 2 always-on foundation layers, each as a tap-to-expand card with a "Why we do it" and "What it must do" section.
* Hover (desktop) / tap (mobile) tooltips on every jargon term, defined in plain English.
* Every stage has buttons that open their own sub-page (deep-dives and per-tool guides).
* Fully mobile responsive with an app feel: bottom-sheet definitions on touch, pinned scrollable stage-nav, full-width buttons, press feedback, slide transition into sub-pages.
* Sub-page rendering now supports real content through an optional `body` field on each page object (see section 6).

The sub-pages are intentionally blank. Each opens a titled page with a "this page is yours to fill" placeholder. Filling them in is the main remaining work (see the task map in section 6).

## 3. The strategy (full reference)

The lead flows top to bottom through 8 stages. Two foundation layers run under all of them.

**Stage 1 — ICP Defining & Signal Identification.** Lock the ICP (industry, size, geography, tech stack, revenue band) and the negative ICP (never-contact list: too small, wrong geo, competitors, existing clients) first, then layer signals (hiring, funding, new office, leadership change, site visit) on top. Signals without a tight ICP just produce a bigger pile of the wrong people.

**Stage 2 — Database Building & Waterfall Enrichment.** One clean database of accounts + contacts. Fill missing email/phone/LinkedIn by querying providers in sequence (A, then B, then C) instead of dropping the lead. Verify every email before it enters the send list so bounce rate stays low. Only our contact path is exposed.

**Stage 3 — Channel Strategy & Message/Angle Mapping.** The signal decides the angle (the hook). Geography decides the first channel: US/Europe open on email, Dubai/Asia lean phone-first (subject to available data). AI writes the personalized opener per lead from its signal + company data, so scale still feels 1-to-1.

**Stage 4 — Multi-Channel Outreach & Deliverability.** The stage most people get wrong. Before any cold email: secondary domains, inbox rotation, domain warm-up (~3 to 4 weeks), SPF/DKIM/DMARC, per-inbox send caps. Then run the multi-touch cadence. Cold channels are email + LinkedIn only.

**Stage 5 — Lead Scoring & Engagement Tracking.** Score = ICP-fit (static) + engagement (dynamic), with decay so stale interest doesn't read as hot. Higher score means a human steps in faster. Every open/click/reply/visit writes back to the record.

**Stage 6 — Nurture & Re-engagement.** An interested-but-not-ready lead is re-approached on LinkedIn or another channel (this is what "retargeting" means here, NOT paid ads), and warmed by our own organic content. Clean three-way split: opt-out / converted / re-engage.

**Stage 7 — Conversion & Handoff.** Automation qualifies to MQL and books the meeting; a human closes. Cold WhatsApp and calling happen ONLY here, after the prospect has confirmed by WhatsApp or email that they're open to a call/meet. Handoff passes full context to the human closer.

**Stage 8 — Closed-Lost Revival.** Store every "no" with reason and date. Wait ~10 days or for a fresh signal, then re-approach on a different channel. Reviving a warm "not now" is cheaper than a new cold prospect.

**Foundation A — CRM & Lead State Machine.** Every lead sits in exactly one state (New → Enriched → Contacted → Engaged → Qualified → Meeting → Won/Lost → Revival), with deduplication so one person is one record across all channels.

**Foundation B — Measurement & Learning Loop.** Track reply rate, positive-reply rate, meeting rate, and cost-per-meeting, broken down by signal and by channel. Feed the winners back into targeting. This is what makes the lookalike engine smarter over time.

## 4. Decisions & guardrails (do not drift from these)

* "Retargeting" = re-approaching on LinkedIn or another channel. NOT paid ads. Ads are out of scope for this system.
* Cold WhatsApp / cold calling only happen AFTER the prospect confirms interest (via WhatsApp or email). They are warm channels, never cold openers.
* Geo channel rule: US/EU → email first; Dubai/Asia → phone-lean (subject to available data).
* Deliverability is non-negotiable and must be built before any email sends.
* Content is the nurture fuel. Autometa's organic IG/LinkedIn content warms leads between touches.
* Copy style: grounded, plain, concrete. No flattery, no AI-ish marketing phrasing, no em dashes.
* Branding: this is an Autometa product. Do NOT mention InstaMeta anywhere. Footer credit stays "Built by Abhinav Dunna, Founder of Autometa AI."
* Project name is **Modren Client Acquisition (MCA)**. Use it everywhere in the UI and docs.

## 5. Tools

Chosen:

* Email outbound → Instantly.ai
* WhatsApp (warm) → Zoko.io

Pending decision (currently shown as "· TBD" buttons in the HTML):

* Signal / intent source (Stage 1)
* Enrichment stack (Stage 2), waterfall across multiple providers
* LinkedIn outreach tool (Stage 4)
* Calling / dialer (Stage 4)
* CRM (Foundation A)

Eventual build backbone (from the original concept, for when we automate): n8n for orchestration, Supabase/Postgres for the data layer, multi-provider waterfall enrichment, a CRM, and AI for scoring/research/personalization.

## 6. Task map (the remaining work)

Every item below is a blank sub-page in `index.html` that needs real content, or a tool decision. Work through them with Abhi one at a time; he supplies the guide/instructions per page, and we write it into that page styled to match the document.

### How to fill a page

The plumbing is already built. Each page object in `STAGES` / `FOUNDATIONS` accepts two optional fields:

```js
{
  id: "icp-define",
  label: "Defining an ICP",
  kind: "deep",
  intro: "One or two grounded sentences for the dark page header.",
  body: `<div class="pg-sec"> ... page content ... </div>`
}
```

`openPage()` renders `body` into `#subbody` when present and hides the blank placeholder; with no `body` the placeholder stays. Everything remains in the single HTML file.

Classes available for page bodies, all matching the existing style system:

| Class | Use |
| --- | --- |
| `.pg-sec` | White card that wraps a section of the page |
| `.block-k.why-k` / `.block-k.build-k` | The gold "Why we do it" and blue "What it must do" labels |
| `.motiv` | Gold reasoning box |
| `.does` | Gradient-bulleted list |
| `.steps` | Numbered step list with gradient number badges |
| `.note` / `.warn` | Gold callout / red callout |
| `.grid2` + `.mini` | Two-up small cards (`.mk` for the card label) |
| `.tblwrap` + `table.tbl` | Horizontally scrollable table |
| `.chips` + `.chip` / `.chip.no` | Inclusion and exclusion pills |
| `.term` + `.tip` | The hover/tap jargon tooltip |
| `code` | Inline code / field names |

### Deep-dive pages to write

* [x] Stage 1 — Defining an ICP — **done.** Six parts: how an ICP is chosen (7 rules, 2 gates, the 3 boxes, the thinkers), Murshid as the product, the 3 candidate ICPs, the chosen ICP in 3 boxes, why it was chosen, and the discovery stack.
* [x] Stage 1 — Negative ICP / Exclusions — **done.** Four buckets (never / not now / free tier only / never cold call), why it is not the inverse of the ICP, the four reasons to exclude, both lists, the channel rule, and how the suppression list is enforced in the system.
* [x] Stage 1 — Signal Identification — **done.** Four tiers, the reframe that product usage outranks every bought signal, manufacturing signals in a small market, the signal list, shelf life and refresh rates, sources, signal-to-first-line, and what to build first.
* [ ] Stage 2 — Building the database
* [ ] Stage 2 — Waterfall Enrichment
* [ ] Stage 2 — Email Verification
* [ ] Stage 3 — Channel-by-Geo logic
* [ ] Stage 3 — Signal → Angle Matrix
* [ ] Stage 3 — AI Personalization
* [ ] Stage 4 — Sequencing / Cadence
* [ ] Stage 4 — Deliverability Setup
* [ ] Stage 5 — The Scoring Model
* [ ] Stage 5 — Engagement Tracking & DB Write-back
* [ ] Stage 6 — Re-approach Playbook
* [ ] Stage 6 — Content-as-Fuel
* [ ] Stage 7 — Booking & Qualification
* [ ] Stage 7 — Closer Handoff
* [ ] Stage 8 — Revival Triggers & Timing
* [ ] Foundation A — The State Machine
* [ ] Foundation B — Metrics & Dashboard

### Tool guide pages to write

* [ ] Instantly.ai (email), chosen, needs setup + how-we-use-it guide
* [ ] Zoko.io (WhatsApp), chosen, needs setup + how-we-use-it guide
* [ ] Signal / intent source, pick tool, then write guide
* [ ] Enrichment stack, pick tools, then write guide
* [ ] LinkedIn outreach, pick tool, then write guide
* [ ] Calling / dialer, pick tool, then write guide
* [ ] CRM, pick tool, then write guide

### Settled decisions from the ICP session

* **Beachhead:** Dubai real estate brokerages. Settled and already public (22 of 38 LinkedIn posts, plus a stated "we only work in Dubai real estate"). Do not reopen without new evidence.
* **The three layers:** Murshid is the product sold to brokerages. MCA is the internal engine that finds them. MCA is sold to non-real-estate buyers only on inbound or referral, never advertised, never outbound.
* **Murshid ICP:** an off-plan focused agent selling to overseas investors, at a Dubai brokerage of 15 to 60 agents. The agent is the user, the owner is the buyer, and if the user does not adopt, the buyer churns.
* **Motion:** agent adopts a free wedge tool bottom-up, brokerage buys the Agency plan top-down. Product usage is the strongest signal we have.
* **Pricing correction:** the monthly is defensible against their existing CRM spend; the large setup fee is what kills deals. Drop it to a small commitment fee credited back. First three clients priced near cost as design partners in exchange for documented results.
* **Data reality:** Apollo and ZoomInfo have thin UAE SME coverage. Build the waterfall around the RERA broker register, the property portals, Google Maps and LinkedIn instead.

### Page style, now established

Both filled pages are written as **training docs for a sales head**, not reference material. The pattern to follow on every remaining page:

* Open with an at-a-glance card so the whole point is readable in ten seconds.
* Short sections with numbered parts. Aim for 8 to 9 rather than 5 dense ones.
* Average paragraph around 25 words, one idea each.
* Tables only for genuinely tabular data with short cells. Use `.mini` cards for anything scannable.
* Keep total page length near 1,000 to 1,600 words.

### Signal decisions worth carrying forward

* **Product usage outranks every bought signal.** Two or more agents from one brokerage on the free tool is the strongest buying signal in the system, and it costs nothing to collect.
* **Our market is small enough to manufacture signals.** ~1,000 accounts means we can run a test enquiry against every one of them rather than waiting for signals to appear. No large-market competitor can do this.
* **Build order:** test-enquiry response time first (works before the product ships, covers 100% of the market), then free-tool signups matched to accounts. Everything else is phase two.
* **Email opens are not a signal.** Scanners and privacy features open mail automatically. Do not score on them.
* Stage 1 is now complete. All three deep-dive pages are written.

### Up next

* Tool guides for Instantly.ai and Zoko.io
* Stage 2 pages (database, waterfall enrichment, email verification)
* Note: Zoko is single-tenant and does not fit a multi-customer product. If the WhatsApp layer becomes part of a SaaS, evaluate multi-tenant providers with Meta Embedded Signup instead.

## 7. Repo & folder structure

Keep it minimal. Do not add extra markdown files.

```
modren-client-acquisition/
├── README.md      # this file, the single source of truth
└── index.html     # the interactive blueprint app
```

### GitHub

The repo is live at `modren-client-acquisition` under the Autometa-AI account. It was created with:

```bash
gh repo create modren-client-acquisition \
  --public \
  --description "Modren Client Acquisition (MCA), a signal-driven B2B outbound system by Autometa" \
  --source . --remote origin
git add README.md index.html
git commit -m "Initial commit: Modren Client Acquisition (MCA) blueprint (v1)"
git push -u origin main
```

`index.html` is a single self-contained file, so the repo can be served directly via GitHub Pages if a live link is ever wanted.
