---
name: hardgpt
description: "Conduct thorough research on complex, real-world questions. Covers any domain: travel policies, local services, product comparisons, technical topics, regulations, financial decisions, health questions, or any problem where the user needs reliable answers from both official sources and real-world experiences. Adapts research strategy based on question type -- adjusting clarification depth, source selection, search orchestration, and output format for each question."
argument-hint: "[question or topic]"
disable-model-invocation: false
---

<!-- HardGPT Research Skill | Copyright (c) 2026 Woody Li (woodydesign.io) | CC BY-NC-SA 4.0 -->

> Copyright (c) 2026 Woody Li (woodydesign.io). Licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
> Commercial licensing: https://woodydesign.io

# Research Skill

A structured, adaptive workflow for researching complex, real-world questions.
Instead of jumping straight into web searches, this skill first clarifies
the user's goal and context, then researches using the strategy best suited
to the question type.

<principles>

1. **Clarify first, research second** — spending 2 minutes clarifying upfront
   saves 10 minutes of misdirected research. Restate the user's goal,
   check if it's clear enough to research, and ask about genuinely missing
   dimensions before searching. Do NOT assume the user has defined their
   problem perfectly. Skip clarification only when the question is already
   specific with all constraints provided.

2. **Route, don't brute-force** — different questions need different strategies.
   Profile the question internally (see routing table), then let the profile
   shape clarification depth, source selection, search orchestration,
   and output format.

3. **Deliver early, deepen on signal** — don't wait for perfection. When you
   have a good-enough answer, deliver it and ask for feedback. The user's
   reaction to v1 is more informative than a 3rd round of clarification.
   After v1, offer: direction check, deepening on interesting findings,
   or refinement with more user info. Build v2 incrementally — don't repeat
   what was already delivered. Skip iteration when the question is already
   fully constrained.

4. **Be honest about uncertainty** — if information might be outdated or
   unverified, say so explicitly. Annotate sources older than 1 year
   with "(as of YYYY)". Flag single-source facts. Include publication
   dates in all source links.

</principles>

<routing>

## Question Profile

When you understand the user's goal, internally assess these 4 dimensions.
Do not output the profile — let it shape your behavior.

| Dimension | Options |
|-----------|---------|
| **Knowledge type** | Factual / Decision support / Plan creation / Exploration |
| **Best sources** | Authority-led / Community-led / Expert-led / Mixed |
| **Time sensitivity** | High (policies, prices) / Medium (reviews) / Low (principles) |
| **Reasoning complexity** | Single-step / Multi-step / Multi-factor trade-off |

A 5th dimension — **user familiarity** (novice / experienced / expert) —
is determined during clarification via proxy questions (e.g., "What's your
current training background?" instead of "How familiar are you?").
Novice: include background, explain terms. Expert: lead with conclusions.

## Routing Matrix

| Profile | Clarify | Search | Deliver |
|---------|---------|--------|---------|
| **Factual / Authority-led** | 1 round: precise identifiers (airline, card, policy version) | Authority-first → community validation. Sequential chaining for multi-step. | Reasoning chain (A → B → C) + uncertainty flags |
| **Discovery / Community-led** | 0–1 round: preferences + constraints | Community-first → official baseline. Parallel searches. | Ranked shortlist: 2-3 attributes + verdict per item |
| **Plan / Expert-led** | 2–3 rounds: trace backward from deliverable to user attributes | Expert-First strategy (below). Map schools of thought. | Phased schedule with progression logic + expert attribution |
| **Trade-off / Mixed** | 2–3 rounds: multi-dimensional constraints | Parallel per dimension, both official + community. | Comparison matrix + "Choose X if..." conditionals |
| **Exploration / Mixed** | 1–2 rounds: scope + depth preference | Mixed sources, map the landscape. | Taxonomy first, then progressive detail per branch |

**Hard stop**: Maximum 3 clarification rounds regardless of type.
After 3 rounds, treat remaining unknowns as variables and proceed.

</routing>

<strategies>

## Clarification Dimensions

Only ask about dimensions that are unclear AND would materially change
the research or the answer. When the answer contains specific numbers
(weights, prices, doses), trace backward: what user attributes determine
those values?

- **Who**: membership status, role, experience level, and — when
  answer-relevant — gender, age, body type, ability level
- **What specifically**: exact product, service, route, scenario, version
- **Where / When**: location, dates, deadlines, timezone, season
- **Existing conditions**: accounts, cards, memberships, subscriptions
- **Constraints**: budget, time, preferences, deal-breakers, must-haves
- **Prior research**: what they've already found, tried, or ruled out

## Clarification Conduct

- Use AskUserQuestion with structured options when choices are enumerable
- 3–5 questions per round; fewer is better
- Questions must have **logical progression** — Round 2 questions should
  be informed by Round 1 answers, not predetermined
- Skip clarification entirely when: the question is factual with all
  constraints provided, the user gave all relevant context upfront,
  or additional context wouldn't change the research approach

## Handling "Not Sure"

When the user can't answer a clarification question:

1. **Offer structured alternatives** — convert the open question into
   2-3 concrete options the user can pick from
2. **Try a different angle** — ask for a related data point that serves
   the same purpose (e.g., don't know booking class → ask what they
   paid or what their confirmation email shows)
3. **Use a reasonable default and declare it** — "I'll assume X (the
   most common case) — I'll note where the answer differs if it's
   actually Y"
4. **Treat it as a variable** — cover multiple scenarios in the final
   answer rather than blocking on it

Never dead-end. Every response must offer at least one clear path forward.

## Research Plan Checkpoint

Before searching, summarize your understanding + proposed plan to the user.
Include: what you'll search, which sources, orchestration approach, and
the deliverable format. Wait for confirmation unless the user said "just go"
or the plan is obviously straightforward. If the user provides a reference
template, use it as the structural guide for delivery.

## Expert-First Strategy

For expert-led questions, **find the people first, then find the content**.

1. **Map the landscape**: search "[domain] expert / coach / thought leader",
   "[domain] best [YouTube / podcast / blog / book]", and in communities
   "who do you follow / recommend"
2. **Cover major schools of thought**: at least one expert per distinct
   approach. Go deep on each framework. Pay attention to where experts
   **disagree** — that reveals trade-offs.
3. **Community validation**: search for practitioners' real results
   ("Followed [expert]'s method, here's what happened")

Budget: 2-3 searches to map landscape, 1-2 per expert deep-dive.
**Hard cap**: 5 experts. Stop at perspective saturation or early if
the first 2 experts largely agree (high consensus → move to validation).
Note credentials, commercial bias, and points of disagreement.

## Source Weight Allocation

| Best sources | Primary | Cross-reference with |
|-------------|---------|---------------------|
| **Authority-led** | Official sites, policy pages, regulations | Community — does real experience match the policy? |
| **Community-led** | Review platforms, forums, social media | Official — are reviews consistent with official claims? |
| **Expert-led** | Expert-First strategy (above) | Community — does the theory hold up in practice? |
| **Mixed** | Both tracks with equal weight | Flag any discrepancies explicitly |

Discover sources dynamically — do NOT rely on memorized site names.
Search "[domain] best forum / subreddit / community" to find them.

## Search Orchestration

- **Single-step**: run searches in parallel, converge quickly.
- **Multi-step**: chain searches — each step informs the next query.
- **Multi-factor**: search each dimension in parallel, then synthesize.

## Freshness Rules

| Time sensitivity | During search | After search |
|-----------------|---------------|--------------|
| **High** | Add current year or "latest" to queries | Must have source < 6 months old; flag if not |
| **Medium** | Prefer recent sources | 1-2 year old sources acceptable |
| **Low** | No time constraint | Classic/foundational sources fine |

Cross-verify critical facts with 2+ independent sources.
Flag date-conflicting sources explicitly.

## Delivery Formats

Structure every answer with: **direct answer first** (1-3 sentences,
conclusion before reasoning), then evidence, validation, alternatives,
caveats, and sources with clickable links.

- **Factual**: default structure. Multi-step chains: show reasoning
  explicitly (A → B → therefore C) so the user can verify each link.
- **Decision (discrete options)**: comparison table (rows = options,
  columns = user's dimensions) + "Choose X if..." recommendations.
- **Decision (discovery)**: ranked shortlist. Each item: 2-3 key
  attributes + one-line verdict. Readable in isolation.
- **Plan creation**: phased schedule (Week/Phase | Focus | Details | Notes).
  Include progression logic, "start now" action, transition criteria.
- **Exploration**: taxonomy/map first, then progressive detail.
  Surface expert disagreements. Mark "further reading" links.

**Output medium**: when the structured content is complex enough that
markdown tables become hard to scan, also write the full report as a
self-contained `{descriptive-slug}.html` (inline CSS, no CDN,
`@media print` for PDF export, clickable source links). Always provide
an in-chat summary with the direct answer and key takeaways — the user
should never need to open the file to see the conclusion. When in doubt,
stay in-chat only.

## Early Delivery

Deliver v1 when you have enough to answer the core question — don't
wait for completeness. After v1, offer one of: direction check
("Is this the right direction?"), deepening ("I noticed X — want me
to dig deeper?"), or refinement ("If you can tell me X, I can improve
this"). Build v2 incrementally — don't repeat v1 content.

**When NOT to iterate**: if the question is already fully constrained
and the research is straightforward, deliver the complete answer
directly. Don't iterate for the sake of iterating.

## Uncertainty Annotations

- Source > 1 year old: "(as of YYYY)"
- High time-sensitivity, unconfirmed: "⚠ Verify directly — this may have changed"
- Single source for critical fact: "(single source, not cross-verified)"
- Sources: always include clickable links with publication dates

</strategies>

<examples>

These examples show the full workflow — from profile assessment through
clarification, research plan, and delivery — for each question archetype.

## Example 1: Multi-step Factual Chain

**User**: "My flight to Tokyo doesn't include free checked bags, but I
have a Chase Sapphire Reserve. Does it cover free baggage?"

**Internal profile**: Factual / Authority-led / High time-sensitivity / Multi-step

**Clarification (1 round)**:

> I want to help figure out if your CSR covers checked baggage for your
> Tokyo flight. A few things I need to trace this:
>
> 1. Which airline are you flying?
> 2. Departing from which city?
> 3. Did you book using your Chase Sapphire Reserve card?

**Research plan**:

> I'll search sequentially — first your airline's international baggage
> policy, then CSR's travel benefits for that airline, then whether they
> stack. I'll deliver as a reasoning chain so you can verify each step.

**Delivery excerpt**:

> **Short answer: No — CSR does not cover free checked bags for [airline].**
>
> Here's the chain:
> 1. [Airline] charges $XX for first checked bag on US→Tokyo routes
>    (source, 2026)
> 2. CSR's travel benefits include trip delay insurance and lounge access,
>    but **not** airline-specific baggage fee waivers (chase.com, 2026)
> 3. Unlike airline co-branded cards, CSR does not have baggage agreements
>    with individual carriers
>
> **Alternative**: [Airline]'s co-branded card does waive the first bag.
> Annual fee is $XX — worth it if you fly them 2+ times/year.
>
> ⚠ Card benefits change periodically — verify at chase.com before your trip.

---

## Example 2: Real-time Discovery with Filtering

**User**: "Find me a good sushi spot near Sunnyvale that's open now.
Must have omakase."

**Internal profile**: Decision support (discovery) / Community-led /
High time-sensitivity / Single-step

**Clarification**: Skipped — constraints already specific (location,
cuisine, dish, timing).

**Research plan**: Proceed directly — search sushi restaurants near
Sunnyvale with omakase, verify current hours, deliver as ranked shortlist.

**Delivery excerpt** (v1, delivered fast):

> Sushi restaurants near Sunnyvale with omakase, open now:
>
> 1. **Sushi Shin** — 0.8 mi, open until 9:30pm
>    Omakase confirmed ($85/person). 4.4★, 320 reviews.
>    "Best omakase in the South Bay for the price" — multiple reviewers.
>
> 2. **Kazoku Sushi** — 1.2 mi, open until 9pm
>    Omakase available ($65/person). 4.1★, 480 reviews.
>    Larger portions, more casual atmosphere per reviews.
>
> 3. **Sushi Tomi** — 2.1 mi (Cupertino), open until 10pm
>    Premium omakase ($120/person). 4.5★, 210 reviews.
>    "Most authentic" — consistently praised for fish freshness.
>
> ⚠ Hours may vary — confirm directly before going.
> Want me to check menus more closely or look at a wider radius?

---

## Example 3: Conflicting Goals + Expert-First

**User**: "I want to train for both Hyrox and a marathon. Build me a plan."

**Internal profile**: Plan creation / Expert-led / Low time-sensitivity /
Multi-factor trade-off

**Clarification (Round 1)**:

> Training plans need specific numbers, so I need a few things:
>
> 1. When are your Hyrox and marathon races? (Determines phasing)
> 2. Men's or women's division? (Hyrox weights differ — men's sled
>    push is 152kg vs women's 102kg)
> 3. What's your current training background? (Weekly frequency,
>    running base, any functional fitness experience?)
> 4. Priority — or are both equally important?

**Clarification (Round 2, informed by R1 answers)**:

> Got it — marathon in October, Hyrox in January, 4x/week with a
> running base. Two more:
>
> 1. Current longest run and approximate pace?
> 2. Done any Hyrox-specific movements — wall balls, sled, ski erg?

**Research plan**:

> I'll use Expert-First: find leading voices in concurrent endurance +
> functional fitness training, map their frameworks, then build your plan.
> Delivering as a phased schedule anchored to your race dates.

**Delivery excerpt**:

> **Direct answer**: With 6 months to marathon and 9 to Hyrox, phase it:
> build running base first, shift to Hyrox-specific work after the
> marathon while maintaining run fitness.
>
> | Phase | Weeks | Focus | Sessions/Wk | Key Workouts |
> |-------|-------|-------|-------------|--------------|
> | 1: Base | 1-8 | Aerobic + strength foundation | 5 (3 run, 2 strength) | Long run progression, compound lifts |
> | 2: Marathon | 9-20 | Marathon-specific | 5 (4 run, 1 maintenance) | Tempo, long runs to 32km |
> | 3: Taper + Intro | 21-24 | Taper + Hyrox skills | 4 (2 taper, 2 stations) | Race-pace rehearsal, technique |
> | 4: Hyrox | 25-36 | Hyrox-specific | 5 (2 run, 3 Hyrox) | Station circuits, sled, race sims |
>
> **Expert sources**: Synthesized from [Expert A] (endurance-first) and
> [Expert B] (concurrent approach). Key disagreement: A advocates strict
> phasing; B argues concurrent throughout. Your marathon-first timeline
> favors phasing.
>
> **Start now**: This week, run 3x (easy pace) + 2x full-body strength.

---

## Example 4: Multi-factor Trade-off for Novice

**User**: "我住在纽约，应该在纽约还是新泽西注册 LLC？"

**Internal profile**: Decision support (discrete) / Mixed /
Medium time-sensitivity / Multi-factor trade-off / Novice

**Clarification (Round 1)**:

> LLC registration depends on your specific situation. A few questions:
>
> 1. What type of business? (freelance, e-commerce, physical retail?)
> 2. Do you have a physical address in NJ, or is business entirely in NYC?
> 3. Roughly how much annual revenue do you expect?
>
> Worth flagging upfront: if you live in NY but register in NJ, you may
> still need to **foreign-qualify** in NY — meaning fees in both states.

**Clarification (Round 2)**:

> Freelance consulting from your NYC apartment, ~$150K revenue. Two more:
>
> 1. Is privacy important? (Some states keep names off public records)
> 2. How involved do you want to be in annual paperwork?

**Research plan**:

> I'll search both NY and NJ official sources (Secretary of State, tax
> departments) plus community experiences with cross-state LLCs. Delivering
> as a comparison matrix with "Choose X if..." at the end.

**Delivery excerpt**:

> **Short answer: For a NYC-based freelancer at $150K, New York is simpler
> and likely cheaper**, because NJ registration would still require you
> to foreign-qualify in NY.
>
> | Factor | New York | New Jersey | Winner |
> |--------|----------|------------|--------|
> | Formation fee | $200 + $9 | $125 | NJ |
> | Publication requirement | ~$300-1500 (county-dependent) ⚠ | None | NJ |
> | Annual fee | $25 biennial | $75/year | NY |
> | Dual-filing if you live/work in NY | N/A | +$250 foreign qual + NY fees | NY |
> | Privacy | Members listed publicly | Members listed publicly | Tie |
> | NYC UBT (>$100K) | Applies | Still applies — you work in NYC | Tie |
>
> **Choose NY if**: you work from NYC (avoids dual filing).
> **Choose NJ if**: you have a real NJ office and most clients are in NJ.
>
> **What you might not know**: NYC has a "publication requirement" — new
> LLCs must publish notices in two newspapers. Cost varies by county
> ($300 in some, $1500+ in Manhattan). This is the biggest hidden cost. (as of 2026)
>
> Sources: [NY DOS](link, 2026), [NJ DORES](link, 2026), [r/smallbusiness](link)

</examples>
