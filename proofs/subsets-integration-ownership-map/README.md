# Subsets — integration ownership map

Independent Forge-0 proof based on Subsets' public Solutions Engineer / customer implementation posture as of September 2026.

When a customer-facing technical role owns goals, data flows, integrations and model behavior, the hidden risk is not just integration failure. It is ambiguity about who owns the next decision when systems disagree.

## Four ownership failures worth making explicit

### 1. Customer goal and implementation metric drift apart
The customer wants a business outcome, but the implementation gets optimized around an easier technical proxy.

Failure mode: successful integration, unsuccessful outcome.

Guardrail: every implementation metric should map back to an explicit customer objective and owner.

### 2. Data contract changes silently
A source system changes schema, field meaning or event timing without breaking transport.

Failure mode: pipeline still runs while model/input semantics degrade.

Guardrail: semantic contract checks, not only transport health checks.

### 3. Integration exception has no decision owner
An edge case appears that could be solved by product, customer configuration or one-off transformation.

Failure mode: issue bounces between teams because nobody owns the tradeoff.

Guardrail: exceptions should expose current decision owner, available resolution classes and deadline.

### 4. Model behavior changes after implementation
A model/config/version change alters output characteristics for an already-live customer.

Failure mode: implementation assumptions become stale without a formal trigger to revisit them.

Guardrail: versioned model/config dependency record with regression checks against the customer-specific acceptance criteria.

## Smallest executable version

Represent each live implementation as:

`customer objective -> data contract -> integration state -> model/config version -> acceptance criteria -> unresolved exception owner`

Then alert only on changes that break one of those relationships.

The useful asset is not another project tracker. It is a compact ownership graph that makes it obvious which team owns the next decision when implementation reality changes.