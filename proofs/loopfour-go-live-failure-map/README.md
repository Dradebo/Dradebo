# LoopFour — go-live failure map

Independent Forge-0 proof based on LoopFour's public Forward Deployed Engineer / implementation posture as of September 2026.

If implementation, imports, customer communication, production issues and go-live all sit in one role, the dangerous seam is the transition from 'configured' to 'operationally safe.'

## Five go-live failure modes worth making explicit

### 1. Import succeeded, semantics did not
Data loads without errors but enum meanings, dates, ownership, historical status or customer-specific conventions are wrong.

Guardrail: semantic reconciliation sample before cutover, not only row-count validation.

### 2. Configuration drift between staging and production
Final customer-specific changes exist in one environment but not the other.

Guardrail: pre-go-live diff of configuration, integrations and credentials boundaries.

### 3. Production incident has no fast rollback decision
A launch issue appears but the team lacks a defined threshold for revert vs patch-forward.

Guardrail: explicit rollback triggers, owner and reversible checkpoint before release.

### 4. Customer communication lags technical state
Engineering knows the issue is understood or mitigated, but the customer does not know current impact, next update or workaround.

Guardrail: incident state object with customer-safe status, next action and next communication checkpoint.

### 5. Successful launch hides unresolved debt
The system goes live, but manual exceptions and temporary workarounds remain invisible.

Guardrail: post-launch exception register with owner, expiry/decision date and productization candidate flag.

## Smallest executable version

A go-live readiness object with five gates:

`semantic data check -> environment diff -> rollback decision -> communication state -> residual exception register`

The point is to make 'ready to launch' an inspectable state rather than a judgment that only exists in the FDE's head.