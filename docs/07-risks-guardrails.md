# 07 — Risk & Guardrails List

## Purpose

Name what can go wrong for a student, how likely it is, how bad it is, and what stops it from happening. A risk with no guardrail is a hope, not a plan.

## The two risks that matter most

### Risk 1 — False availability

**What happens:** The system says a book is available. The student walks to the shelf. The book is issued out, or on another shelf.

**Harm:** Wasted time, a missed deadline, and lost trust in the library. A student who is sent to an empty shelf once is less likely to trust the next result.

**Guardrails:**

- Availability is shown only when it is in the catalogue data, with a timestamp.
- Availability accuracy must be 100% in the eval (`docs/04-eval.md`). Any failure blocks release.
- If the data is more than 24 hours old, show "check at desk" instead of an availability claim.
- The librarian logs every wrong result in the pilot, including every false-availability incident. Target: 0.

### Risk 2 — Edition confusion

**What happens:** The system shows the wrong edition, or does not make the edition clear. The student uses the 3rd edition when the assignment requires the 4th, and cites pages or chapters that do not match.

**Harm:** Wrong citations, lost marks, and a student who did the work but used the wrong book.

**Guardrails:**

- Edition is always displayed on every result, exact match or alternative.
- If the required edition is not available, the alternative is labelled plainly — for example, "Earlier edition — check whether your assignment accepts this edition."
- The eval checks edition accuracy on every search, and every edition failure is listed in the failure analysis.

## Full risk list

| # | Risk | Who is harmed | Likelihood (before guardrails) | Harm if it happens | Guardrail | Owner |
| --- | --- | --- | --- | --- | --- | --- |
| R1 | False availability — student sent to an empty shelf | Student | Medium — availability data goes stale | High — wasted trip, lost trust | Availability only from data, with timestamp; "check at desk" if data is > 24h old; 100% accuracy bar in the eval | Librarian / product owner |
| R2 | Edition confusion — wrong edition used for an assignment | Student | Medium — editions look alike in search results | High — wrong citations, lost marks | Edition always displayed; alternatives labelled with edition difference | Product owner |
| R3 | Invented shelf location — student sent to a shelf that does not exist | Student | Low, if the guardrail holds; high if the system is allowed to guess | High — wasted trip, lost trust | Never invent a location; if the data has no location, say so | Product owner |
| R4 | Alternative shown as an exact match — student cites the wrong book | Student | Medium — alternatives look like matches | Medium — wrong source cited | Alternatives clearly separated, each with a plain-language reason | Product owner |
| R5 | "Not in catalogue" not stated — student keeps searching for a book the library does not hold | Student | Medium — systems prefer to show something rather than nothing | Medium — wasted time, then a purchase or a weaker source | No-match case must say "not in catalogue + nearest alternative" plainly | Product owner |
| R6 | Stale data presented as live — availability or location is out of date but looks current | Student | Medium — depends on how often the catalogue updates | High — same harm as R1 | Timestamp on every result; "check at desk" prompt when data is > 24h old | Librarian |
| R7 | Topic search returns a plausible but unusable book — student does not realise it is the wrong book | Student | Medium — topic matches are approximate | Medium — weak source for the assignment | Alternatives labelled; exact matches separated; student confirms "usable for my assignment" in the pilot | Product owner |
| R8 | Over-trust — students stop checking edition and availability because the tool "usually works" | Student | Low in the pilot; higher after expansion | Medium — R1 and R2 harms happen without the student checking | Keep edition, timestamp, and "check at desk" visible on every result; do not hide them for a cleaner design | Product owner |
| R9 | Library budget harm — if discovery fails, usage data stays low and budgets are harder to justify | Library | Medium, if the product does not work | Medium — long-term funding | Measure discovery rate and zero-result rate against the baseline; do not expand if the pilot does not improve them | Product owner / librarian |

## Guardrails — checklist

These guardrails must hold in every version, including the pilot. If a guardrail cannot be met, the feature does not ship.

- [ ] Availability shown only when it is in the catalogue data.
- [ ] Availability timestamp shown on every result.
- [ ] "Check at desk" prompt shown when availability data is more than 24 hours old.
- [ ] Edition always displayed on every result.
- [ ] Shelf location shown only when it is in the catalogue data; never invented.
- [ ] Exact matches and close alternatives clearly separated, with a plain-language reason for each alternative.
- [ ] No-match case says "not in catalogue" plainly, with the nearest alternative.
- [ ] No book from outside the catalogue presented as a library holding.
- [ ] Librarian reviews the 40-search eval before any student sees the product.
- [ ] Librarian logs every wrong result during the 2-week pilot.

## What to do when a guardrail fails

| Situation | Action |
| --- | --- |
| Availability is wrong in the eval | Eval fails. Do not start the pilot. Fix the data or the display, then re-run the eval. |
| A false-availability incident happens in the pilot | Log it the same day. Tell the student at the desk. Check whether the data was stale, and whether the "check at desk" prompt should have shown. Pause expansion until the cause is fixed. |
| An edition failure happens in the pilot | Log it. Check whether the edition field in the data is clear enough, and whether the display makes it obvious. |
| A location was invented or guessed | Treat it as a serious failure. Find where the guess came from and remove it. Re-run the affected eval searches. |
| The librarian does not sign off | Do not start the pilot. Record what must change, change it, and ask for review again. |

## Incidents log — template (blank, to fill in during the pilot)

| Date | Incident | What the student saw | What was actually true | Harm | Cause | Fix |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |

**Target: 0 false-availability incidents and 0 wrong-edition incidents in the pilot.** Any incident is recorded here, not hidden.
