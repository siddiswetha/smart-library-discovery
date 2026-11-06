# 03 — One-Page Spec

## Product

Smart Library Discovery — search that handles real student queries, over the library's own catalogue data only.

## Users

- **Students** doing real assignments, searching by topic, partial title, or reference-list text.
- **Librarians** at the help desk, who need to trust the results before recommending the tool.

## Problem (one line)

Students cannot find books the library already owns, because the catalogue expects exact titles and spellings.

---

## Input

The student can enter any one of these:

| Input type | Example (EXAMPLE) |
| --- | --- |
| Topic | "statistics for psychology assignments" |
| Partial title | "intro to psych…" (part of a title, half-remembered) |
| Misspelled title or author | A title or author name with a spelling mistake |
| Reference-list text | Text copied from a reference list, for example an author, year, and title |

The system must accept the input as typed. It must not require the student to fix their spelling first.

## Output

Every result must show:

- Title
- Author
- Edition — always displayed
- Shelf location — only if it is in the catalogue data
- Availability — only if it is in the catalogue data, with a timestamp showing when it was last updated

### Two clearly separated groups

**1. Exact matches**

Books that match the title, author, or edition the student asked for.

**2. Close alternatives**

Books that do not match exactly, but may still be useful. Each alternative must be labelled with a plain-language reason, for example:

- "Same topic, different author"
- "Earlier edition — check whether your assignment accepts this edition"
- "Similar title, different book"

Alternatives must never be shown as if they were exact matches.

### No-match case

If no book in the catalogue matches, the system must say so plainly:

> "Not in catalogue — here is the nearest alternative."

It must not invent a book, and it must not suggest a book from outside the catalogue as if the library held it.

---

## In scope

- Search over the provided catalogue data only.
- Topic search, partial-title search, and misspelling-tolerant search.
- Reference-list text as a search input.
- Exact matches and honestly labelled close alternatives.
- Availability and shelf location, shown only when they are in the data, with a freshness timestamp.
- Edition always displayed.
- Text search with a response in under 2 seconds (see `docs/06-cost-latency.md`).

## Out of scope

- Never state availability that is not in the data.
- Never invent a shelf location.
- Never present a book from outside the catalogue as a library holding.
- No book purchasing, no ordering, and no inter-library loan requests in this version.
- No recommendations based on a student's borrowing history.
- No chat or general question-answering beyond finding a book.

---

## Primary metric

**Successful discovery rate** — the share of searches where the student found a usable book for their assignment.

This is the metric that decides whether the product works. All other metrics support it. See `docs/05-metrics.md`.

## Pass bar (from the eval)

- **Availability accuracy: 100%.** Every availability statement must match the catalogue data. There is no partial credit here — a wrong "available" sends a student to an empty shelf.
- **Top-3 discovery: at least 85%.** In at least 85% of searches where the book is in the catalogue, the correct book must be ranked in the top 3 results.

The eval that tests this is in `docs/04-eval.md` and `evals/eval-set.csv`.

## Guardrails (summary)

Full list in `docs/07-risks-guardrails.md`. The three that shape this spec:

1. **Availability timestamp shown** on every result.
2. **Edition always displayed**, so a student does not take the wrong edition for an assignment that requires a specific one.
3. **"Check at desk" prompt** when the availability data is more than 24 hours old, instead of sending the student to a shelf on stale data.

## Open questions

1. How fresh is the availability data in practice — live, hourly, or daily?
2. How exact are shelf locations in the data — a specific shelf, or only a floor or section?
3. How should the system handle a reference list that names several books at once — one search, or one result per book?

These are answered by the librarian interview in `docs/02-research-notes.md` before building.
