# Formance connector contract stress pack

Independent Forge-0 proof for outbound research. Based on Formance's public connector, Payments, Flows and Reconciliation documentation as of September 2026.

## Why this exists

Formance's value proposition depends on making heterogeneous payment providers behave like one coherent system. That pushes a lot of risk into the connector contract: different rails expose different capabilities, timing, identifiers, retries, reversals and failure semantics.

The useful test is not "does this connector work on the happy path?" but "does the normalized contract stay truthful when the provider behaves badly?"

## Five failure cases worth making explicit

### 1. Duplicate provider events
- Provider delivers the same webhook/event more than once.
- Expected contract: idempotent ingestion, preserved provider identity, no double-ledger side effect.
- Evidence to surface: dedupe key, replay history, resulting ledger/payment object.

### 2. Delayed status reversal
- A payment appears settled/successful and later reverses or is corrected by the upstream rail.
- Expected contract: status transition is representable without mutating historical truth; downstream consumers can distinguish correction from replacement.
- Evidence to surface: transition timeline, provider payload, ledger/reconciliation consequence.

### 3. Capability asymmetry
- One connector can ingest balances but cannot initiate payouts; another supports both.
- Expected contract: capability differences are machine-inspectable rather than discovered at runtime.
- Evidence to surface: connector capability matrix / contract test that fails before orchestration is deployed.

### 4. Provider-reference loss or mismatch
- Upstream identifiers are missing, reused, reformatted or no longer match an internal object cleanly.
- Expected contract: unmatched or ambiguous events become explicit exceptions, not silent best guesses.
- Evidence to surface: original payload, matching decision, exception state, reconciliation status.

### 5. Retry + reconciliation drift
- A transfer retries after an ambiguous timeout; upstream executed once but application state is uncertain.
- Expected contract: retries cannot create hidden duplication and reconciliation can explain the final state from first principles.
- Evidence to surface: attempt IDs, provider IDs, ledger postings, reconciliation result.

## Suggested executable form

Turn each case into a provider-agnostic conformance fixture:

`fixture -> connector adapter -> normalized Payments event -> optional Flow -> Ledger consequence -> Reconciliation assertion`

A connector passes only if the resulting system state is explainable and the original provider evidence remains inspectable.

## What this could become

- reusable connector conformance suite
- failure-injection pack for the Generic Connector framework
- pre-release checklist for new rails
- machine-readable capability/guarantee manifest per connector

The point is not more documentation. The point is to make the hidden contract executable.