# Reference: testing techniques used in the design

*Guide: name the technique next to each case or requirement (for example in the Title or Req column: "TC-03 [BVA]"). This shows the reason each case exists.*

| Technique | Family | Best for | Core idea |
| --- | --- | --- | --- |
| Equivalence partitioning (EP) | Black-box | Inputs with ranges or classes | Split inputs into classes that the system treats the same; test one value per class |
| Boundary value analysis (BVA) | Black-box | Numeric, date, length limits | Defects cluster at edges; test min-1, min, min+1, max-1, max, max+1 |
| Decision table | Black-box | Combined business rules | Enumerate condition combinations and the expected action for each rule |
| State transition | Black-box | Workflows, statuses, sessions | Test valid transitions, and try invalid ones that must be rejected |
| Use case / scenario | Black-box | End-to-end user journeys | Main flow, alternative flows, exception flows |
| Pairwise (combinatorial) | Black-box | Many parameters (browser x OS x language) | Cover every pair of values with far fewer cases than all combinations |
| Error guessing | Experience-based | Weak spots from past bugs | List likely mistakes: empty, spaces, long, special characters, double submit |
| Exploratory testing | Experience-based | New or unclear features | Timeboxed session with a charter; learn, design and execute at the same time |
| Checklist-based | Experience-based | Repeatable quality checks | Reuse a tailored list (security, accessibility, release smoke) |
| Risk-based testing | Strategy-level | Prioritising effort | Depth of testing follows likelihood x impact |
| Statement / branch coverage | White-box | Unit tests of logic | Every statement or decision outcome executed at least once |

## How to apply each one

**Equivalence partitioning**

1. List every input and the rule it must follow.
2. Define valid classes and invalid classes (wrong type, empty, out of range).
3. Pick one representative per class; combine at most one invalid value per case so failures are traceable.

*Example: age field accepts 18 to 65. Classes: under 18 (invalid), 18 to 65 (valid), over 65 (invalid), non-numeric (invalid). Test values: 10, 40, 80, "abc".*

**Boundary value analysis**

1. Take each partition edge from EP.
2. Test the edge and its two neighbours (2-value or 3-value method; state which one you use).
3. Apply to dates, lengths, amounts, counts and time limits as well as numbers.

*Example: same age field. Values: 17, 18, 19, 64, 65, 66.*

**Decision table**

1. List conditions (Yes/No) and actions.
2. Write all combinations (2 to the power of n), then merge rules with the same outcome and remove impossible ones.
3. One test case per remaining rule.

*Example: discount applies only if the customer is a member AND the cart is 100 or more AND no other coupon is used: 8 combinations reduce to 4 rules.*

**State transition**

1. Draw states and events (or write them as a table).
2. Cover every valid transition at least once; cover each state's invalid events.
3. For critical flows, also cover sequences of 2 or more transitions (for example Failed, Retry, Paid).

*Example: order states Cart, Pending, Paid, Failed. Invalid event to try: pay again while status is Paid.*

**Pairwise**

1. List parameters and their values.
2. Generate pairs with a tool (PICT, AllPairs) instead of by hand.
3. Add any known risky full combination manually.

*Example: 3 browsers x 3 OS x 3 languages = 27 combinations; pairwise needs about 9.*

**Error guessing and exploratory charters**

- Charter format: *Explore [area] with [resources or data] to discover [risk or information]*, 60 to 90 minutes.
- Record notes, bugs, questions, and areas not covered; turn valuable findings into permanent automated cases.

## Which technique for which requirement (example)

| Requirement | Technique | Reason |
| --- | --- | --- |
| Quantity 1 to 10 | EP + BVA | Single numeric range |
| Free shipping from 50.00 | BVA | Threshold with money at stake |
| One promo code per order, expiry, single use | Decision table | Several conditions combine |
| Payment pending, paid, failed, retry | State transition | Statuses and illegal sequences |
| Checkout journey on mobile | Use case + exploratory | Cross-screen flow, UX unknowns |
| Browser, OS, language support | Pairwise | Too many combinations to run all |
| Double click, back button, tab switching | Error guessing | Known weak spots in web flows |
