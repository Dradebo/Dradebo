# Nixo — handoff fracture map

Independent Forge-0 proof based on Nixo's public FDE operations product surface as of September 2026.

Nixo's public promise is unusually clear: capture customer context, connect product work, surface relevant code/history, and reduce duplicate work across FDE teams.

That means the critical system question is not only whether context is collected, but whether it stays coherent as it moves across Slack/CRM/tickets/code and over time.

## Four fracture points worth making explicit

### 1. Customer context changed after intake
A customer changes environment, stack, constraint or goal after the intake agent captured the original state.

Failure mode: stale context remains attached to current work and looks authoritative.

Useful guardrail: every critical context field should have source, timestamp, confidence and supersession history.

### 2. Ticket says one thing, code says another
Linear/Zendesk indicates a request is open while a merged PR or deployed config already partially solved it.

Failure mode: duplicate engineering or misleading prioritization.

Useful guardrail: resolution state should be inferred from multiple evidence types and disagreements surfaced explicitly.

### 3. Past solution is similar but unsafe to reuse
Code intelligence finds an 80% match from another account, but security model, region, infrastructure or customer-specific assumptions differ.

Failure mode: similarity becomes accidental authorization to copy.

Useful guardrail: reusable solution cards should expose the assumptions that made the prior solution valid.

### 4. Ownership changes during a handoff
A customer request moves from intake -> FDE -> product engineering -> customer success, with pieces of context living in different systems.

Failure mode: nobody owns the unresolved decision even though every system has a record.

Useful guardrail: every active issue should expose current decision owner, next required action and the evidence that triggered the handoff.

## Smallest executable version

Represent each active customer problem as a context graph with four mandatory layers:

`customer claim -> current technical environment -> active work -> resolved evidence`

Then run a contradiction check whenever any connected source updates.

The useful product is not another task tracker. It is a system that can say: "these two pieces of context now disagree, and this person owns resolving the disagreement."
