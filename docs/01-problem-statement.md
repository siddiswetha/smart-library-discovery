# 01 — Problem Statement with Evidence

## The problem, in one sentence

Students cannot find books the library already owns, because the catalogue expects exact titles and correct spellings, while students search by topic, partial titles, or copied reference lists.

## Who has this problem?

**Primary users: students doing real assignments.**

They are under time pressure, they may be new to university libraries, and they may not know the exact title or author of the book they need. A first-year student and a final-year student face the same catalogue, but not the same advantage.

**Secondary users: librarians at the help desk.**

They answer the same failed searches again and again, and they see the cost when a student gives up.

## What happens today?

A typical failure looks like this:

1. A student types a topic or a half-remembered title into the catalogue.
2. The catalogue returns no useful result, or a long list of unrelated books.
3. The student concludes "the library doesn't have it."
4. The student buys the book, uses a weaker free online source, or goes without the source.

The catalogue did not say the book was missing. The student inferred it, because the search gave them nothing usable.

## Why this matters

### For the student

- Money: buying a book they could have borrowed for free.
- Quality: citing a weak online source instead of a proper book.
- Time: repeating searches, asking at the desk, or starting again.

### For the library

- Lost usage: a book that is borrowed counts as use. A book that is never found does not.
- Lost evidence: usage data helps justify the library budget. Failed discovery hides real demand.
- Lost trust: a student who concludes "the library doesn't have it" is less likely to try again.

### Why it is an equity problem

Students who already know how catalogues work — exact titles, author spellings, edition numbers — get more value from the same library. Students who do not know those conventions get less. The library is the same. The access is not.

## Evidence to collect (do not skip this)

A problem statement is only a claim until it is tested. Collect this evidence before building anything:

| Evidence | What to collect | Target |
| --- | --- | --- |
| Real queries | Log of actual student catalogue searches | 25 queries, including failures |
| Observed searches | Watch students search (with permission) during real assignments | 5 students |
| Librarian view | Interview on what catalogue data can and cannot show | 1 librarian |
| Failure pattern | Group the failed queries by cause: spelling, partial title, topic-only, wrong edition, no match | All 25 queries grouped |
| Cost of failure | What students did instead: bought, used a weaker source, went without | Recorded for each failure |

**Status of the evidence in this folder: TO COLLECT.**

The tables in `docs/02-research-notes.md` are blank templates. No real student has been interviewed yet for this project, and no real query has been logged. Do not present the EXAMPLE queries in `evals/eval-set.csv` as evidence. They are test inputs, not research findings.

## What success looks like

A student with a topic, a partial title, or a reference-list entry finds a usable book for their assignment — and can see its edition, shelf location, and whether it is actually available right now.

The primary measure is the **successful discovery rate**: the share of searches where the student found a usable book for their assignment. The full metrics plan is in `docs/05-metrics.md`.

## What this project will not do

- It will not invent availability or shelf locations.
- It will not search the wider internet and present those results as library holdings.
- It will not hide the difference between an exact match and a close alternative.

Those limits are part of the product, not a later fix. They are defined in `docs/03-spec.md` and protected by the guardrails in `docs/07-risks-guardrails.md`.

## Open questions

1. How often do students search by topic rather than by title? The 25-query log will answer this.
2. Which failure is most common: spelling, partial title, or topic-only search?
3. How often is the book actually in the catalogue, but missed by the search?
4. How fresh is the availability data the library can provide, and how often is it more than 24 hours old?

Answer these from real data before deciding how much AI the product needs. That routing decision is recorded in `docs/06-cost-latency.md`.
