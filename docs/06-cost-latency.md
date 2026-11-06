# 06 — Cost & Latency Estimate

## Purpose

Show where AI adds value, where plain search is enough, and what each search costs — so the product uses AI only where it earns its cost.

## The key idea: route, don't always use AI

Catalogue search itself is cheap. AI query-understanding is the cost.

That leads to a simple rule:

- **Use plain search** when it is enough.
- **Use AI** only when plain search is likely to fail — misspellings, partial titles, and topic expansion.

This is the routing decision. It is recorded below, with the evidence to check, so it can be challenged and changed.

## Routing decision

| Search type | Route | Why |
| --- | --- | --- |
| Exact title and author, correctly spelled | **Plain search** | Plain search already finds it. AI adds cost and no value. |
| Misspelled title or author | **AI** | Plain search fails on spelling. AI can correct the spelling and match the intended book. |
| Partial title only | **AI** | Plain search needs more of the title. AI can expand a partial title to likely full titles, then check them against the catalogue. |
| Topic-only | **AI** | There is no title to match. AI expands the topic into likely titles and subjects, then checks them against the catalogue. |
| Reference-list text | **AI** | The input is unstructured text. AI extracts the title, author, and year, then plain search checks the catalogue. |
| No-match check | **Plain search (after AI, if AI was used)** | The final answer — "not in catalogue" — must come from the catalogue data, not from the AI. |

**Decision in one line:** AI understands the query; the catalogue decides the answer. AI never invents availability, location, or a book.

### Routing log — template (blank, to fill in during the pilot)

| Week | Total searches | Plain search | AI search | Share routed to AI | Discovery rate (plain) | Discovery rate (AI) |
| --- | --- | --- | --- | --- | --- | --- |
| Pilot week 1 |  |  |  |  |  |  |
| Pilot week 2 |  |  |  |  |  |  |

Use this log to test the routing decision. If plain search discovers almost as well as AI on a category, move that category to plain search. If AI discovers much better, keep it on AI — and record the cost of that improvement.

## Latency

| Search type | Target | Notes |
| --- | --- | --- |
| Text search | **Under 2 seconds** | Measured from the student submitting the query to results appearing. |
| Plain search | Under 2 seconds | Catalogue lookup is fast; this should be easy to meet. |
| AI search | Under 2 seconds | This is the harder target. If AI understanding takes longer, say so honestly and measure it — do not claim under 2 seconds without timing real searches. |

**Status: latency NOT measured yet.** Time real searches in the pilot and record the results below. Do not claim a latency number until it has been timed.

### Latency log — template (blank, to fill in)

| Search type | Searches timed | Median latency | Slowest search | Under 2 seconds? (Yes / No) |
| --- | --- | --- | --- | --- |
| Plain search |  |  |  |  |
| AI search |  |  |  |  |

## Cost estimate — template (blank, to fill in with real prices)

Costs depend on which AI service is used, how it is priced, and how many searches run. Do not invent a price. Fill in this table with the real pricing of the service you would use, and keep the source and date of the price.

| Item | Unit price (with source and date) | Searches per month (estimate) | Monthly cost (estimate) |
| --- | --- | --- | --- |
| Catalogue / plain search |  |  |  |
| AI query-understanding (per search) |  |  |  |
| Total |  |  |  |

### Cost per search and cost per success — template (blank, to fill in)

| Measure | Formula | Result |
| --- | --- | --- |
| Cost per search | Total monthly cost ÷ total searches | TBD |
| Cost per successful discovery | Total monthly cost ÷ successful discoveries | TBD |
| Cost per search — plain only | Plain-search cost ÷ plain searches | TBD |
| Cost per search — AI only | AI cost ÷ AI searches | TBD |

**Worked example of the thinking (EXAMPLE, not a real price):**

If AI costs more per search than plain search, but AI searches succeed far more often on misspelled and topic-only queries, the cost per *successful* discovery may still be lower with AI on those categories — because a failed plain search costs the student time and may end in a book purchase. That is the comparison to make: cost per success, not cost per search. Use real prices and real pilot discovery rates to do it.

## Where AI adds value, and where it does not

| Situation | AI adds value? | Evidence to check in the pilot |
| --- | --- | --- |
| Exact title, correct spelling | No — plain search is enough | Discovery rate for exact searches, plain vs. AI |
| Misspelled title or author | Yes — plain search fails on spelling | Discovery rate for misspelled searches, plain vs. AI |
| Partial title | Yes — plain search needs more text | Discovery rate for partial-title searches |
| Topic-only | Yes — there is no title to match | Discovery rate for topic-only searches |
| Availability or location | No — that is catalogue data, not AI | Availability accuracy must be 100% either way |

## What to do if costs are too high

1. Route more searches to plain search, starting with exact-title searches.
2. Use AI only for the first step (understanding the query), then plain search for the catalogue lookup — never AI for the whole search.
3. Limit AI to the categories where the pilot shows it clearly improves discovery.
4. If AI still costs more than the value it adds, say so in the portfolio write-up. A product manager who can say "we should not use AI here" is doing the job well.

## Status

- Routing decision: **written above — to be tested in the pilot.**
- Real prices collected: **No — TO DO.**
- Latency measured: **No — TO DO.**
- Cost per successful discovery calculated: **No — TO DO, after the pilot.**
