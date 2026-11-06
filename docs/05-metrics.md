# 05 — Metrics Plan

## Purpose

Decide in advance what "working" means, so success is measured, not assumed. Every metric below has a definition, a target, and a source of data. If a metric has no source of data, it cannot be measured — and it does not count.

## The one metric that matters most

**Successful discovery rate** — the share of searches where the student found a usable book for their assignment.

- **Definition:** (Searches where the student found a usable book) ÷ (All searches).
- **How to measure it:** Ask the student after the search — "Did you find a book you can use for this assignment?" — and record Yes or No. Do not guess from clicks alone. A click is not a usable book.
- **Target:** Set the target after the baseline is measured (see "Baseline" below). The eval pass bar is ≥ 85% top-3 discovery on the 40-search test set; the live target should be set from real pilot data, not copied from the eval.

## Metrics, grouped

### 1. Task success — did the student find what they needed?

| Metric | Definition | Target | Source |
| --- | --- | --- | --- |
| Successful discovery rate | Searches ending with a usable book ÷ all searches | TBD after baseline | Student answer after search + pilot log |
| Zero-result rate | Searches returning no usable result ÷ all searches | Lower than the catalogue-alone baseline | Search log |
| Top-3 discovery rate | Correct book in the top 3 ÷ searches where the book is in the catalogue | ≥ 85% (eval); live target TBD after pilot | Eval + search log |
| Time to find a book | Minutes from first search to a usable book found | Faster than catalogue alone | Timed observation in the pilot |

### 2. Quality — were the results correct and honest?

| Metric | Definition | Target | Source |
| --- | --- | --- | --- |
| Availability accuracy | Results with correct availability ÷ all results checked | **100%** | Eval + librarian log in the pilot |
| Location accuracy | Results with correct shelf location ÷ all results checked | Record all failures; fix before expanding | Eval + librarian log |
| Edition accuracy | Results showing the correct edition ÷ all results checked | Record all failures; fix before expanding | Eval + librarian log |
| Alternatives honestly labelled | Alternatives shown with a plain-language reason ÷ all alternatives shown | 100% | Eval + pilot review |

Availability accuracy has a 100% target because a single wrong "available" sends a student to an empty shelf. That is a harm, not a minor error. See `docs/07-risks-guardrails.md`.

### 3. Cost per success — what did each successful discovery cost?

| Metric | Definition | Target | Source |
| --- | --- | --- | --- |
| Cost per search | Total search cost ÷ all searches | See `docs/06-cost-latency.md` | Cost log |
| Cost per successful discovery | Total search cost ÷ successful discoveries | Lower than the cost of a failed search that ends in a book purchase or a help-desk visit | Cost log + discovery rate |
| Share of searches routed to AI | AI-handled searches ÷ all searches | As low as possible while keeping discovery high — AI only where it adds value | Routing log |

Cost per success matters more than cost per search. A cheap search that fails is not cheap — it costs the student time, and may cost them the price of a book.

### 4. Harm — what went wrong for the student?

| Metric | Definition | Target | Source |
| --- | --- | --- | --- |
| False-availability incidents | Students sent to a shelf for a book that was not there | **0** | Librarian log in the pilot; student reports |
| Wrong-edition incidents | Students who took or cited the wrong edition for an assignment requiring a specific edition | **0** | Librarian log; student reports |
| Students who gave up | Students who stopped searching and went without a source | Lower than the catalogue-alone baseline | Pilot observation + follow-up |
| Students who bought a book the library held | Students who bought a book that was in the catalogue but not found | Lower than the baseline; aim for 0 in the pilot | Pilot follow-up question |

Harm metrics are counted in the pilot by the librarian, who logs every wrong result. See `docs/08-release-portfolio.md`.

## Baseline — measure the catalogue alone first

Before claiming any improvement, measure the current catalogue on the same things:

| Baseline measure | How to get it | Status |
| --- | --- | --- |
| Discovery success rate with the catalogue alone | Observe the 5 students in `docs/02-research-notes.md` | TO COLLECT |
| Zero-result rate with the catalogue alone | Log their 25 real queries | TO COLLECT |
| Time to find a book with the catalogue alone | Time their searches | TO COLLECT |
| Students who bought a book or used a weaker source after failing | Ask after each failed search | TO COLLECT |

**Status: baseline NOT measured yet.** Do not claim an improvement until the baseline and the pilot are both measured on the same definitions.

## Results — template (blank, to fill in after the pilot)

| Metric | Baseline (catalogue alone) | Pilot result | Target | Met? |
| --- | --- | --- | --- | --- |
| Successful discovery rate | TBD | TBD | TBD | TBD |
| Zero-result rate | TBD | TBD | TBD | TBD |
| Time to find a book | TBD | TBD | TBD | TBD |
| Availability accuracy | TBD | TBD | 100% | TBD |
| Cost per search | TBD | TBD | See doc 06 | TBD |
| Cost per successful discovery | TBD | TBD | TBD | TBD |
| False-availability incidents | TBD | TBD | 0 | TBD |
| Wrong-edition incidents | TBD | TBD | 0 | TBD |

## What not to measure

- **Number of searches.** More searches can mean more confusion, not more success.
- **Clicks.** A click does not mean the book was usable.
- **"User satisfaction" with no definition.** If it is measured, define the exact question asked, and record the answers — do not report a single unexplained score.

## Review rhythm

- **During the pilot (2 weeks):** librarian logs every wrong result daily; review the log weekly.
- **At the end of the pilot:** compare pilot metrics with the baseline on the same definitions, then decide whether to expand to student self-service.
- **After expansion:** review discovery rate, zero-result rate, availability accuracy, and cost per success monthly.
