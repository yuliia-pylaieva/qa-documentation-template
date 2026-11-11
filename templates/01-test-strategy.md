# Test Strategy: [Product]

*Guide: one to three pages, reviewed yearly. Answers "how do we test here, in general?"*

## 1.1 Objectives

*Guide: 3 measurable outcomes tied to business goals, not to testing activity.*

- [Prevent <worst business failure>, e.g. wrong charges]
- [Protect <key metric> at or above <value>]
- [Give feedback within <N> minutes of each merge]

## 1.2 Scope

| In scope | Out of scope |
| --- | --- |
| [Features, platforms, browsers, integrations] | [What other teams own, what is deferred, and why] |

## 1.3 Test levels and ownership

*Guide: who tests what, and how much automation is expected at each level.*

| Level | What is tested | Owner | Target |
| --- | --- | --- | --- |
| Unit | [Business logic] | [Developers] | [Coverage % on <module>] |
| API / integration | [Services, third parties] | [Dev + QA] | [Every endpoint: contract + negative] |
| UI end-to-end | [Critical journeys only] | [QA] | [N tests, under M minutes] |
| Exploratory | [New or risky areas] | [QA] | [Sessions per release] |
| UAT | [Business flows] | [PM / client] | [One session] |

## 1.4 Test types

*Guide: tick what applies, delete what does not, and add one line of how for each.*

- [ ] Functional: [technique(s)]
- [ ] Regression: [when it runs: PR / nightly]
- [ ] Performance: [load profile, thresholds]
- [ ] Security: [checklist, e.g. OWASP Top 10]
- [ ] Accessibility: [standard, tool]
- [ ] Compatibility: [browser/device matrix]
- [ ] Data / migration / integration: [what is checked]

## 1.5 Risk register

*Guide: score = Likelihood (1-3) x Impact (1-3). 6 to 9: automation + exploratory. 3 to 4: automated happy path + key negatives. 1 to 2: exploratory only. Aim for 6 to 10 risks.*

| ID | Risk | L | I | Score | Treatment |
| --- | --- | --- | --- | --- | --- |
| R-01 | [What can go wrong, in business words] | [1-3] | [1-3] | [L x I] | [Which tests and levels] |
| R-02 | [ ] | [ ] | [ ] | [ ] | [ ] |

## 1.6 Automation strategy

- **Automate:** [criteria, e.g. stable, repeatable, high risk]
- **Do not automate:** [criteria]
- **Stack:** [UI, API, load, accessibility, CI tool]
- **Practices:** [patterns, test data approach, flaky test policy with deadline]

## 1.7 Environments and data

| Environment | Purpose | Data |
| --- | --- | --- |
| [Dev] | [ ] | [Synthetic] |
| [QA/Staging] | [ ] | [Anonymised, sandbox integrations] |
| [Pre-production] | [ ] | [Production-like volume] |

*Guide: state the rule for personal data and for third-party sandboxes.*

## 1.8 Defect management

| Severity | Definition | Example | Response |
| --- | --- | --- | --- |
| S1 Critical | [No core flow, data loss, money wrong] | [ ] | [Fix now, stop release] |
| S2 Major | [Main flow broken, workaround exists] | [ ] | [Fix before release] |
| S3 Minor | [Secondary function] | [ ] | [Next sprint] |
| S4 Trivial | [Cosmetic] | [ ] | [Backlog] |

Lifecycle: [New, Triaged, In progress, Ready for retest, Verified, Closed, Reopened]. Triage: [when, who].

## 1.9 Metrics

*Guide: each metric needs a target and a decision it supports. Drop vanity metrics.*

| Metric | Target | Decision it supports |
| --- | --- | --- |
| [Requirement coverage] | [100% of must-haves] | [Is design complete?] |
| [Escaped defects per release] | [0 S1/S2] | [Is the strategy working?] |
| [Defect removal efficiency] | [90% or more] | [Are we finding bugs early enough?] |
| [Flaky-test rate] | [under 2%] | [Can we trust the suite?] |
