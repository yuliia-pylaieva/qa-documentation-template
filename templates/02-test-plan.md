# Test Plan: [Product] [Release]

*Guide: one to two pages per release. Answers "what, when, who, and when are we done?"*

| Field | Value |
| --- | --- |
| Plan ID | [TP-<area>-<release>] |
| Version / status | [1.0, approved by <names>] |
| Author | [Owner] |
| References | [Strategy, requirements, designs, API spec] |

## 2.1 Features

- **To be tested:** [feature (REQ-xx), feature (REQ-xx)]
- **Not tested, and why:** [feature: deferred / unchanged / owned by other team]

## 2.2 Approach summary

*Guide: only what differs from the Strategy for this release.*

- [When test design starts relative to development]
- [What is automated first, what stays manual]
- [Exploratory and bug-bash plan]
- [Non-functional checks and where they run]

## 2.3 Schedule and milestones

| Date | Milestone | Owner |
| --- | --- | --- |
| [Date] | [Requirements reviewed, cases drafted] | [ ] |
| [Date] | [Environment and test accounts ready] | [ ] |
| [Date range] | [Functional testing and automation] | [ ] |
| [Date] | [Code freeze] | [ ] |
| [Date range] | [Full regression and non-functional] | [ ] |
| [Date] | [UAT and go/no-go] | [ ] |
| [Date] | [Release and production smoke] | [ ] |

## 2.4 Resources and effort

| Role | People | Responsibility | Effort (days) |
| --- | --- | --- | --- |
| [QA] | [ ] | [ ] | [ ] |
| [Developers] | [ ] | [ ] | [ ] |
| [DevOps / PM] | [ ] | [ ] | [ ] |

*Guide: state the buffer (about 20%) openly and what you cut first if time runs out.*

## 2.5 Entry criteria

- [ ] [Requirements reviewed, no open "TBD"]
- [ ] [Build deployed, smoke suite green]
- [ ] [Test data and third-party sandbox accounts ready]
- [ ] [Unit tests passing in CI]

## 2.6 Exit criteria

*Guide: every criterion must be measurable by someone other than you.*

- [ ] [% of must-have cases executed, % passed]
- [ ] [No open S1/S2; owners and target dates for S3]
- [ ] [Automated regression green N times in a row]
- [ ] [Performance thresholds: p95 under X ms, errors under Y%]
- [ ] [Accessibility / security items closed]
- [ ] [UAT sign-off recorded]

## 2.7 Suspension and resumption

Suspend when: [smoke fails on a new build / environment down for more than N hours / more than N blockers open]. Resume when: [fixed build passes smoke].

## 2.8 Project risks

| ID | Risk | Probability | Impact | Mitigation |
| --- | --- | --- | --- | --- |
| PR-01 | [Unstable sandbox or environment] | [L/M/H] | [L/M/H] | [Mocks, contract tests] |
| PR-02 | [Requirements change] | [ ] | [ ] | [Traceability shows impact] |
| PR-03 | [Single point of failure in the team] | [ ] | [ ] | [Shared docs, pairing] |
| PR-04 | [Late code freeze] | [ ] | [ ] | [Risk-based cut list agreed with PM] |

## 2.9 Deliverables

[Strategy, this plan, test cases, automation code, daily status note, defect reports, test summary report with go/no-go recommendation]
