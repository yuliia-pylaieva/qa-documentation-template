# QA Documentation Template

A reusable set of fill-in templates for the three core QA documents: **Test Strategy**, **Test Plan** and **Test Design**, plus a reference of testing techniques and a pre-share checklist.

## Contents

| File | Purpose | When to use |
| --- | --- | --- |
| [templates/01-test-strategy.md](templates/01-test-strategy.md) | How we test in general: levels, types, risks, automation, environments, defects, metrics | Once per product, review yearly |
| [templates/02-test-plan.md](templates/02-test-plan.md) | What, when, who and when are we done for one release | Once per release |
| [templates/03-test-design.md](templates/03-test-design.md) | Requirements, partitions, decision table, test cases, traceability, bug report | Once per feature |
| [templates/04-testing-techniques.md](templates/04-testing-techniques.md) | Reference: equivalence partitioning, boundary values, decision tables, state transition, pairwise, etc. | While designing cases |
| [templates/05-bug-report-jira.md](templates/05-bug-report-jira.md) | Jira bug ticket: fields, summary rules, description in wiki markup and Markdown, filled example, checklist | Every time you log a defect |

## How to use

Copy the files for each new product or release, replace every `[bracketed placeholder]`, and delete the italic *Guide:* lines when done. Fill in this order, because each document feeds the next:

1. **Risks first** (Strategy 1.5): they decide depth of testing everywhere else.
2. **Strategy** (long-lived): rewrite only when the product, team or tooling changes.
3. **Plan** (per release): scope, dates, people, entry and exit criteria.
4. **Design** (per feature): requirements, techniques, cases, traceability.

**Conventions:** IDs are `REQ-xx` (requirement), `R-xx` (product risk), `PR-xx` (project risk), `TC-xx` (test case), `BUG-xx` (defect). Every TC points to at least one REQ; every P1 risk has at least one TC.

| Placeholder | Fill with | Example |
| --- | --- | --- |
| [Product] | Name of the system under test | ShopEasy |
| [Release] | Version or sprint under test | v2.4 |
| [Owner] | Person accountable | QA engineer |
| [Date] | Concrete date, not "soon" | 11 Dec 2026 |

## Quality checklist before sharing

- [ ] No [placeholder] or *Guide:* line is left.
- [ ] Every objective, exit criterion and metric has a number or a date.
- [ ] Every Must requirement has at least one test case; every risk scored 6 or more has cases at more than one level.
- [ ] Out-of-scope items are listed with a reason.
- [ ] Risks, dates and owners agree between Strategy, Plan and Design.
- [ ] One P1 test case is written in full detail, with data, expected result and cleanup.
- [ ] A colleague who did not write it can run any case without asking you.
- [ ] Known gaps are stated openly (they read as honesty, not weakness).
