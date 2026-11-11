# Test Design: [Feature]

*Guide: per feature. Answers "which concrete cases prove each requirement?"* See [04-testing-techniques.md](04-testing-techniques.md) for how to apply each technique.

## 3.1 Choose the technique

| If the requirement has... | Use | Typical cases to derive |
| --- | --- | --- |
| A numeric or length limit, a range, a threshold | Equivalence partitioning + boundary values | Min-1, min, min+1, max-1, max, max+1; one value per invalid class |
| Several conditions that combine into one outcome (rules, permissions, discounts) | Decision table | One case per rule (column) |
| A workflow with states (order, payment, account) | State transition | Each valid transition, plus invalid ones that must be blocked |
| A user journey across screens | Use-case / scenario testing | Main path, alternative paths, error paths |
| Input formats or free text | Error guessing, pairwise for combinations | Empty, spaces, long, special characters, emoji, duplicates |
| New or unclear behaviour | Exploratory charter (timeboxed) | Mission, area, time, notes, bugs found |

## 3.2 Requirements

| ID | Requirement (testable wording) | Priority | Risk |
| --- | --- | --- | --- |
| REQ-01 | [Actor] can [action] when [condition]; result is [observable outcome] | [Must/Should] | [R-xx] |

*Guide: if you cannot write an expected result, the requirement is not testable yet. Ask before designing.*

## 3.3 Conditions and partitions

| Input / condition | Valid classes | Invalid classes | Boundary values |
| --- | --- | --- | --- |
| [Field or rule] | [ ] | [ ] | [ ] |

## 3.4 Decision table (if applicable)

| Rule | [Condition 1] | [Condition 2] | [Condition 3] | Expected result |
| --- | --- | --- | --- | --- |
| 1 | [Yes/No] | [Yes/No] | [Yes/No] | [ ] |
| 2 | [ ] | [ ] | [ ] | [ ] |

## 3.5 Test case catalogue

*Guide: one check per case, a clear title ("<action> <condition> -> <result>"), exact data, exact expected result. Priority: P1 = release blocker, P2 = important, P3 = nice to have. Type: M = manual, A = automated.*

| TC | Title | Req | Priority | Type | Preconditions | Steps | Expected result |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-01 | [Positive: valid input] | [REQ-xx] | [P1] | [A] | [State, data, user] | [1. ... 2. ...] | [Exact value / message / state] |
| TC-02 | [Boundary: limit value] | [REQ-xx] | [P2] | [A] | [ ] | [ ] | [ ] |
| TC-03 | [Negative: invalid input] | [REQ-xx] | [P2] | [A] | [ ] | [ ] | [Error text; nothing saved] |
| TC-04 | [Interruption: double click, back, timeout] | [REQ-xx] | [P1] | [M] | [ ] | [ ] | [No duplicate; state consistent] |

**Detailed case format (for P1 cases):**

1. Preconditions: [user, data, environment, mocks]
2. Action: [exact input values]
3. Expected: [UI result, stored data, API/integration result, side effects such as email]
4. Cleanup: [what to delete or refund]

## 3.6 Traceability matrix

| Requirement | Test cases | Risk | Coverage |
| --- | --- | --- | --- |
| [REQ-xx] | [TC-xx to TC-xx] | [R-xx] | [Full / Partial (why) / None (why)] |

*Guide: any Must requirement with no cases, or P1 risk with no cases, is a gap to raise before testing starts.*

## 3.7 Bug report template

| Field | Value |
| --- | --- |
| ID / title | [BUG-xx: what is wrong, where, under what condition] |
| Severity / priority | [S1-S4 / High-Medium-Low] |
| Environment | [Env, build, browser/device, OS] |
| Found by | [Test case or exploratory session, date] |
| Steps | [1. ... 2. ... 3. ...] |
| Expected | [Per REQ-xx] |
| Actual | [What happened, exact values] |
| Analysis | [Suspected cause, scope, does it reproduce always?] |
| Evidence | [Screenshot, logs, API response, video] |
| Impact | [Who is affected, money/legal/data risk] |
