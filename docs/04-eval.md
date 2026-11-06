# 04 — Eval Test Set, Rubric, and Results

## Purpose

Test whether the product actually helps a student find the right book — before any student uses it.

The test set is in `evals/eval-set.csv`. This document explains how it is built, how to score it, and what counts as a pass.

## Test set

**40 searches in total**, in four categories:

| Category | Count | What it tests |
| --- | --- | --- |
| Exact | 15 | The student knows the exact title and author. The system must find it. |
| Misspelled / partial | 10 | The title is misspelled or only partly remembered. The system must still find it. |
| Topic-only | 10 | The student only has a topic, no title. The system must find a usable book. |
| No-match | 5 | The book is not in the catalogue. The correct answer is "not in catalogue + nearest alternative." |
| **Total** | **40** |  |

> All 40 queries are labelled EXAMPLE. The expected books, availability, and locations in the CSV are EXAMPLE catalogue entries. They show the shape of a test set. Replace them with real catalogue entries from the library you are working with before running the eval.

The CSV columns are:

`id, category, query, expected_book, expected_availability, expected_location, rubric, result, notes`

- `result` is left blank / TBD. **Do not invent results.** Fill it in only after running each search.
- `expected_book` for a no-match row is the nearest alternative, not a book the library holds. The rubric for those rows checks that the system said "not in catalogue" honestly.

## Rubric

Score every search on the same four checks:

| Check | What "correct" means |
| --- | --- |
| **Correct book ranked in top 3** | For exact, misspelled / partial, and topic-only searches: the expected book appears in the first 3 results. For no-match searches: the system says "not in catalogue" and offers the nearest alternative. |
| **Availability correct** | The availability shown matches the catalogue data exactly, with a timestamp. |
| **Location correct** | The shelf location shown matches the catalogue data exactly. If the data has no location, the system says so — it does not invent one. |
| **Alternatives honestly labelled** | Any close alternative is clearly separated from exact matches, with a plain-language reason why it is an alternative. |

### Scoring a single search

| Outcome | Meaning |
| --- | --- |
| Pass | All four rubric checks are correct. |
| Fail — discovery | The correct book is not in the top 3 (or, for no-match, the system did not say "not in catalogue"). |
| Fail — availability | The availability shown does not match the data, or no timestamp is shown. |
| Fail — location | The location shown does not match the data, or a location was invented. |
| Fail — labelling | An alternative was shown as if it were an exact match, or no reason was given for why it is an alternative. |

A search can fail on more than one check. Record every failure reason — that is what the failure analysis is for.

## Pass bar

- **Availability accuracy: 100%.** Every one of the 40 searches must show availability correctly. If even one is wrong, the eval fails. A wrong "available" sends a student to an empty shelf.
- **Top-3 discovery: at least 85%.** The correct book must be in the top 3 in at least 34 of the 40 searches (85% of 40 = 34). For the 5 no-match searches, "correct" means the system said "not in catalogue" and offered the nearest alternative.

Location accuracy and honest labelling are also recorded for every search. They do not have a separate percentage pass bar, but any failure in either one must be listed in the failure analysis and fixed before release.

## How to run the eval

1. Use the real catalogue data for the library, not the EXAMPLE entries, for the expected answers.
2. Run each of the 40 queries exactly as written in the CSV. Do not fix spelling first.
3. Record the top 3 results for each query, plus the availability, location, and timestamp shown.
4. Score each query against the rubric above.
5. Fill in the `result` column in the CSV only with what actually happened: Pass, or Fail with the reason.
6. Do not re-run a failed query with a "better" spelling to make it pass. The failure is the finding.

## Results — template (blank, to fill in after running the eval)

**Status: NOT RUN YET. Results are TBD. Do not fill this in with invented numbers.**

| Measure | Result | Pass bar | Pass / Fail |
| --- | --- | --- | --- |
| Availability accuracy | TBD | 100% | TBD |
| Top-3 discovery | TBD (___ / 40) | ≥ 85% (34 / 40) | TBD |
| Location accuracy | TBD (___ / 40) | Record and fix all failures | TBD |
| Alternatives honestly labelled | TBD (___ / 40) | Record and fix all failures | TBD |

### Results by category — template (blank, to fill in)

| Category | Searches | Top-3 correct | Availability correct | Location correct |
| --- | --- | --- | --- | --- |
| Exact (15) | 15 | TBD | TBD | TBD |
| Misspelled / partial (10) | 10 | TBD | TBD | TBD |
| Topic-only (10) | 10 | TBD | TBD | TBD |
| No-match (5) | 5 | TBD | TBD | TBD |
| **Total** | **40** | **TBD** | **TBD** | **TBD** |

## Failure analysis — template (blank, to fill in)

Group failures by reason, so the same root cause is not counted as five separate problems.

| Failure reason (grouped) | Count | Query IDs | What happened | Fix planned |
| --- | --- | --- | --- | --- |
| EXAMPLE: Misspelling not handled |  |  |  |  |
| EXAMPLE: Topic too broad — wrong book ranked first |  |  |  |  |
| EXAMPLE: Wrong edition ranked above the required edition |  |  |  |  |
| EXAMPLE: Availability shown without a timestamp |  |  |  |  |
| EXAMPLE: Alternative shown as an exact match |  |  |  |  |
| EXAMPLE: No-match not stated plainly |  |  |  |  |

> The rows above are EXAMPLE failure-reason labels, to show how to group failures. They are not real results.

### Questions to answer from the failure analysis

1. Which category fails most — exact, misspelled / partial, topic-only, or no-match?
2. Is there one root cause behind several failures, or many different causes?
3. Which failures are a search problem, and which are a data problem (for example, missing edition or stale availability)?
4. What is the smallest fix that would remove the largest group of failures?

## Sign-off

A librarian must review this eval before any student sees the product. See `docs/08-release-portfolio.md` for the sign-off template. Do not start the pilot until that review is complete.
