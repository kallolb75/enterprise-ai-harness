# Controls register

Every control in the harness, with the reason it exists and the condition under which it is reviewed. The rule is in [ADR-000](adr/ADR-000-how-decisions-are-made.md): a control without an expiry condition is a defect.

A control is anything that constrains what the harness or an agent may do: an approval gate, a policy check, a rate limit, a denied tool, a required human in the loop.

| ID | Control | Reason | Expiry condition | Owner | Introduced | Status |
|---|---|---|---|---|---|---|
| | | | | | | |

No controls yet. The first ones arrive with the policy gate ring, and each one lands here in the same pull request that adds it.

## How a row changes

- **Active** when the control is in the code or the configuration and its eval passes.
- **Under review** from the day its expiry condition is met. The review closes within the next cycle.
- **Retired** with a date and one line on what replaced it, or why nothing needed to. The row stays.

A control is never renewed without a new expiry condition.
