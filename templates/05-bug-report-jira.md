# Bug Report Template (Jira)

*Guide: one bug per ticket. Replace every [bracketed placeholder]. A developer who has never seen the feature should be able to reproduce the bug from the ticket alone.*

## 1. Jira fields

| Field | What to enter | Example |
| --- | --- | --- |
| Project | [Project key] | SHOP |
| Issue Type | Bug | Bug |
| Summary | [Component]: [what is wrong] when [condition] (see rules below) | Checkout: free shipping not applied when subtotal is exactly 50.00 |
| Priority | Business urgency of the fix: Highest, High, Medium, Low, Lowest | High |
| Severity (custom field) | Technical impact: S1 Critical, S2 Major, S3 Minor, S4 Trivial | S2 Major |
| Affects Version/s | [Build or release where the bug was found] | 2.4.0-rc3 |
| Fix Version/s | Leave empty; the team sets it at triage | |
| Component/s | [Feature area] | Checkout |
| Environment | [Env, build, browser/device, OS] | QA, 2.4.0-rc3, Chrome 130, Windows 11 |
| Labels | [regression, mobile, payment, found-in-automation, ...] | regression, pricing |
| Assignee | Leave empty (triage assigns) or [dev lead] | |
| Reporter | [You] | |
| Linked issues | [Blocks / is caused by / relates to <KEY-123>] | relates to SHOP-101 (REQ story) |
| Attachments | Screenshot or video, logs, HAR file, API response | |

### Summary rules

- Pattern: `[Component]: [wrong behaviour] when [condition]`.
- State the symptom, not the guess at the cause ("total is wrong", not "rounding bug").
- No ticket numbers, names, or words like "urgent", "please fix" in the summary.
- Search Jira for duplicates before creating (use words from the summary, the component and the error text).

### Severity vs priority

| Severity | Definition | Typical priority | Example |
| --- | --- | --- | --- |
| S1 Critical | No core flow, data loss, money wrong, security hole | Highest | Customer charged twice |
| S2 Major | Main flow broken, workaround exists | High | Promo code fails on Safari |
| S3 Minor | Secondary function wrong | Medium | Wrong label on order summary |
| S4 Trivial | Cosmetic | Low | 2px misalignment |

Severity is the technical impact (set by QA). Priority is how soon the business needs the fix (confirmed by PM at triage). They can differ: a typo in the company name on the homepage is S4 but may be High priority.

## 2. Description (Jira wiki markup)

*Guide: paste this into the Description field. In Jira Cloud, switch the editor to text mode, or use the Markdown version in section 3.*

```
h3. Summary
[One or two sentences: what is wrong, where, and the impact.]

h3. Environment
* *Environment:* [QA / Staging / Prod]
* *Build / version:* [2.4.0-rc3]
* *Browser / device / OS:* [Chrome 130, Windows 11]
* *User / account type:* [guest / registered / admin, test account name]
* *Test data:* [cart contents, promo code, card number from sandbox list]

h3. Preconditions
* [State the system must be in before step 1]

h3. Steps to reproduce
# [Step 1: exact action and input]
# [Step 2]
# [Step 3]

h3. Expected result
[What should happen, with reference to the requirement: REQ-xx / SHOP-123]

h3. Actual result
[What happens instead, with exact values, messages and codes]

h3. Reproducibility
[Always / 3 of 5 attempts / Once]. Also reproduced on: [other browsers, builds, environments]. Not reproduced on: [...]

h3. Evidence
* Screenshot / video: [attached file name]
* Logs / console errors: {code}[paste relevant lines only]{code}
* API request and response: [attached HAR or snippet]

h3. Impact
[Who is affected, how many, financial / legal / data risk, workaround if any]

h3. Additional information
* Found by: [test case TC-xx / exploratory session / customer report]
* First seen in: [build], last good: [build]
* Suspected cause (optional, clearly marked as a guess): [...]
```

## 3. Description (Markdown, for the Jira Cloud editor)

```markdown
### Summary
[One or two sentences: what is wrong, where, and the impact.]

### Environment
- **Environment:** [QA / Staging / Prod]
- **Build / version:** [2.4.0-rc3]
- **Browser / device / OS:** [Chrome 130, Windows 11]
- **User / account type:** [guest / registered / admin]
- **Test data:** [cart contents, promo code, sandbox card]

### Preconditions
- [State the system must be in before step 1]

### Steps to reproduce
1. [Step 1: exact action and input]
2. [Step 2]
3. [Step 3]

### Expected result
[What should happen, with reference to REQ-xx / SHOP-123]

### Actual result
[What happens instead, with exact values, messages and codes]

### Reproducibility
[Always / 3 of 5 attempts / Once]. Also reproduced on: [...]. Not reproduced on: [...]

### Evidence
- Screenshot / video: [attached file name]
- Logs / console errors: [relevant lines only]
- API request and response: [attached HAR or snippet]

### Impact
[Who is affected, how many, financial / legal / data risk, workaround if any]

### Additional information
- Found by: [test case TC-xx / exploratory session]
- First seen in: [build], last good: [build]
- Suspected cause (optional, marked as a guess): [...]
```

## 4. Filled example

**Summary:** Checkout: free shipping not applied when subtotal is exactly 50.00

| Field | Value |
| --- | --- |
| Issue Type / Priority / Severity | Bug / High / S2 Major |
| Affects Version/s | 2.4.0-rc3 |
| Component/s | Checkout |
| Labels | regression, pricing, found-in-automation |
| Environment | QA, Chrome 130, Windows 11 |

**Description**

- **Summary:** Standard delivery shows a 4.99 fee when the cart subtotal is exactly 50.00, although requirement REQ-04 says shipping is free from 50.00.
- **Preconditions:** Signed-in test user; empty cart.
- **Steps to reproduce:**
  1. Add items so the cart subtotal is 50.00.
  2. Go to the Delivery step.
  3. Select Standard delivery.
- **Expected result:** Shipping = 0.00, total = 50.00 (REQ-04: free at 50.00 or more).
- **Actual result:** Shipping = 4.99, total = 54.99.
- **Reproducibility:** Always (5 of 5). Subtotals 49.99 (fee 4.99) and 50.01 (free) behave correctly.
- **Evidence:** Screenshot of the order summary; API response `/api/checkout/quote` returns `shipping: 0.00`, so the UI shows a different value than the API.
- **Impact:** Every customer with a subtotal of exactly 50.00 overpays by 4.99; legal risk for advertised free shipping.
- **Additional information:** Found by automated case TC-08. Suspected cause (guess): UI compares with "greater than" instead of "greater than or equal".

## 5. Quality checklist before you click Create

- [ ] Summary follows the pattern and describes the symptom.
- [ ] Reproduced at least twice; steps tested by following them exactly as written.
- [ ] Expected result points to a requirement, a design, or a documented rule.
- [ ] Exact values, messages and build number are included (no "some", "wrong", "etc.").
- [ ] Attachments show the failure and contain no passwords, tokens or real personal data.
- [ ] Duplicate search done; related issues are linked.
- [ ] Severity set by impact, priority proposed by urgency, and neither is used to push the ticket.
- [ ] One bug per ticket; separate symptoms are separate tickets.

## 6. Lifecycle reminder

New (Open) → Triaged / To Do → In Progress → Ready for Test (Resolved) → Verified → Closed, with Reopened if the retest fails. When retesting, comment with the build number, steps repeated, and result; attach new evidence if the bug is reopened.
