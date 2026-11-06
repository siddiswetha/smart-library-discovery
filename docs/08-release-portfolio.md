# 08 — Staged Release + Portfolio Write-up

## Purpose

Release the product in stages, so a mistake affects a few students at a help desk — not every student at once — and so the portfolio shows real evidence, not claims.

## Staged release plan

### Stage 0 — Before any student sees it

**Gate: librarian review of the 40-search eval.**

- Run the full eval in `docs/04-eval.md` on the real catalogue data.
- The librarian reviews every result, especially availability, edition, and location.
- The eval must pass its bars: 100% availability accuracy, and at least 85% top-3 discovery.
- If it does not pass, fix the failures and re-run the eval. Do not move to Stage 1.

**Librarian sign-off note — template (blank, to fill in)**

> I have reviewed the 40-search eval for Smart Library Discovery.
>
> - Availability accuracy: ___ / 40
> - Top-3 discovery: ___ / 40
> - Location accuracy: ___ / 40
> - Alternatives honestly labelled: ___ / 40
> - Failures I am concerned about: ___
> - Changes I need before the pilot: ___
>
> Decision: [ ] Approved for pilot at one help desk / [ ] Not approved — changes needed
>
> Name: ___
> Role: ___
> Date: ___

Do not start the pilot without a signed "Approved for pilot" note.

### Stage 1 — Pilot at one help desk, 2 weeks

- The tool is available only at one help desk, with a librarian present.
- The librarian helps the student use it, and watches what happens.
- **The librarian logs every wrong result** — every false availability, wrong edition, wrong location, and misleading alternative — in the incidents log in `docs/07-risks-guardrails.md`.
- At the end of each week, review the log: what failed, why, and what to fix.
- Ask each student after their search: "Did you find a book you can use for this assignment?" Record Yes or No. That is the successful discovery rate.

**What counts as a good pilot:**

- Availability accuracy stays at 100%, with 0 false-availability incidents.
- Discovery rate is higher than the catalogue-alone baseline.
- Every failure has a named cause and a planned fix.

**What stops the pilot:**

- Any false-availability incident that is not explained and fixed.
- Discovery rate no better than the catalogue alone.
- The librarian withdraws support.

### Stage 2 — Expand to student self-service

Only after Stage 1, and only if:

- [ ] The pilot discovery rate beats the baseline.
- [ ] Availability accuracy was 100% in the pilot, with 0 false-availability incidents.
- [ ] Every failure in the pilot has a fix, or a written reason why it is acceptable.
- [ ] The librarian agrees to expand.
- [ ] Cost per successful discovery is known and acceptable (see `docs/06-cost-latency.md`).

In Stage 2, students use the tool without a librarian present. Keep the guardrails visible on every result: edition, availability timestamp, and the "check at desk" prompt when data is stale.

### Stage 3 — Review and decide

After one month of self-service, review the metrics in `docs/05-metrics.md` against the baseline and decide:

- Keep and improve it,
- Change the routing (more plain search, or more AI), or
- Stop it, if it does not improve discovery or costs more than it is worth.

A decision to stop is a valid outcome. Record it honestly.

## Rollback plan

If the pilot or self-service stage goes wrong:

1. Remove the tool from student use and return to the catalogue alone.
2. Keep the help desk open, with the librarian helping students search as before.
3. Record what went wrong, using the incidents log and the failure analysis.
4. Do not re-release until the cause is fixed and the eval is re-run.

## Portfolio write-up

Write this section only after the research, eval, and pilot are real. Do not write it from the EXAMPLE data in this folder.

### What to include

**1. Query log analysis**

- The 25 real queries, grouped by failure cause, from `docs/02-research-notes.md`.
- The main finding in one or two sentences: which failure was most common, and how often the book was actually in the catalogue.

**2. Eval table with failure reasons grouped**

- The 40-search results from `docs/04-eval.md`, with the results-by-category table filled in.
- Failures grouped by reason, not listed one by one. The question to answer: "What is the one fix that removes the most failures?"

**3. Librarian sign-off note**

- The completed sign-off note from Stage 0 above, with the librarian's name, role, and date.
- If the librarian asked for changes, list them and what was done.

**4. Routing decision (AI vs. plain search) with cost evidence**

- The routing table from `docs/06-cost-latency.md`.
- The pilot routing log: how many searches went to AI, how many to plain search, and the discovery rate for each.
- Cost per search and cost per successful discovery, with real prices, sources, and dates.
- The conclusion in plain language: where AI earned its cost, and where plain search was enough.

### Portfolio write-up — template (blank, to fill in after the work is real)

**Problem:** ___

**Who I talked to:** 5 students doing real assignments, and 1 librarian. (Record what you actually learned — no invented quotes.)

**What I found in the query log:** ___

**What I built (as a spec):** ___

**Eval result:** Availability ___ / 40. Top-3 discovery ___ / 40. (Pass bars: 100% availability, ≥ 85% top-3.)

**Biggest failure group, and the fix:** ___

**Routing decision:** ___ (AI for ___, plain search for ___, with cost per successful discovery of ___.)

**What I would do next:** ___

**What I learned about being an AI Product Manager:** ___

### How to present this project

- Show the problem, the evidence, the eval, and the decision — in that order.
- Be honest about what did not work. A grouped failure analysis is stronger evidence than a perfect score with no failures listed.
- Do not claim results that are still TBD. Say "not run yet" where that is true, and say what you will do next.

## Status

- Eval run: **No — TBD**
- Librarian sign-off: **No — TBD**
- Pilot (2 weeks, one help desk): **No — TBD**
- Expansion to self-service: **No — TBD**

---

*End of the 8 PM artefacts. The full set is: 01 problem statement, 02 research notes, 03 spec, 04 eval, 05 metrics, 06 cost & latency, 07 risks & guardrails, 08 release & portfolio.*
