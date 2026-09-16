# CollectWise — control failure map

Independent Forge-0 proof based on CollectWise's public debt-collection automation posture as of September 2026.

The risky layer in collections is not only whether an AI can contact someone. It is whether every action remains explainable, policy-compliant and recoverable when source data, timing or human judgment disagree.

## Five control failures worth making explicit

### 1. Wrong account state at contact time
A balance, dispute flag, payment arrangement or hardship status changes upstream after a workflow has already queued outreach.

Failure mode: contact is technically executed from stale truth.

Guardrail: high-risk actions revalidate critical account state immediately before execution.

### 2. Identity confidence is insufficient
Phone/email/address data points to a plausible person but not with enough confidence for the intended action.

Failure mode: automation treats likely identity as verified identity.

Guardrail: action thresholds vary by identity confidence, with explicit human review below threshold.

### 3. Policy says proceed, conversation context says stop
A rule permits an action, but the latest interaction includes dispute, vulnerability, legal representation or another stop condition.

Failure mode: workflow policy outruns the newest evidence.

Guardrail: conversational stop-signals have defined precedence and create a reviewable exception state.

### 4. Promise-to-pay without operational closure
A consumer commits to a date/amount, but the promise is not propagated cleanly into the system of record and follow-up state.

Failure mode: future contact ignores an existing arrangement.

Guardrail: every commitment creates an auditable state transition with owner, expiry and reconciliation against actual payment.

### 5. Human override becomes invisible
An operator changes a decision or communication path without the system preserving why.

Failure mode: later reviewers can see what happened but not the rationale.

Guardrail: human overrides require compact reason capture and preserve original recommendation + final action.

## Smallest executable version

For each outbound action, record:

`source-state snapshot -> identity confidence -> applicable policy -> latest conversational evidence -> chosen action -> human override if any -> downstream state change`

Then fail closed whenever those layers disagree in a way the current policy cannot explain.

The useful product is not more logging. It is a control surface that can answer: "why was this action allowed at that exact moment?"
