# Two-Coast Degree Planner

A single-page planner for a **part-time Harvard Ed.M. (LDIT)** taken while working a
full-time job across both Pacific and Eastern hours.

**Live:** https://yaseeny933.github.io/harvard-degree-planner/

## What it does

- **Term map** — every selected course drawn across its real start and end dates, so you can
  see what actually overlaps and where the load lands.
- **Two-coast week grid** — courses are pinned to Eastern; the gutter reads every row in
  Pacific *and* Eastern at once. Your 40 work hours are treated as a flexible budget and
  poured into whatever gaps the classes leave.
- **Degree tracking** — 42 credits, 16 letter-graded, Foundations, the Program Core
  Experience, the ≤16 cross-registration and ≤8 field-experience ceilings, and the
  part-time 10-credit term cap.
- **Session-aware collisions** — overlap is tested on date ranges *and* clock times, so a
  Fall 1 and a Fall 2 course sharing a slot never falsely conflict.

Your plan is stored in your own browser (localStorage). Nothing is uploaded.

## Data

13,599 sections — 12 Harvard schools plus MIT, Fall 2026 and Spring 2027.

- 3,987 publish a day-and-time pattern and can be placed on the calendar.
- 10,652 carry a date range.
- **No room or building data exists** in the source catalogue; the closest is instruction
  mode (in person / online), and only where the registrar filled it in.

HGSE Fall 2026 dates come from my.harvard course detail pages directly, because the bulk
catalogue's `session_dates` column is unreliable there. Verified session envelopes:

| Session | Runs |
|---|---|
| Fall 1 | Sep 2 – Oct 19, 2026 |
| Fall 2 | Oct 20 – Dec 4, 2026 |
| Full Term | Sep 2 – Dec 4, 2026 |

Individual courses vary within those windows: 147 of 167 start *and* end on one of their own
meeting weekdays, so the dates are the first and last actual class meeting rather than the
administrative boundary. The planner keys off per-course dates.

## Caveats

Degree rules follow the HGSE Student Handbook as summarised in the source kit — **re-verify
against the 2026-27 handbook** before relying on them. Course data changes right up to
enrolment.

## Rebuilding

```bash
python3 build_catalog.py    # merge sources, repair dates
python3 encode_catalog.py   # dictionary-encode (6.4 MB -> 1.4 MB)
python3 build2.py           # inject into template2.html -> site/index.html
```
