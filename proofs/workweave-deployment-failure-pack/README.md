# Workweave — deployment failure pack

Independent Forge-0 proof based on Workweave's public FDE/onboarding posture as of September 2026.

If the same team owns onboarding, issue reproduction, architecture explanation and de-risking deployment, then the reusable asset is not only documentation. It is a failure pack that turns repeated deployment pain into explicit checks.

## Five failure cases worth institutionalizing

### 1. Environment mismatch
A customer reproduces the nominal setup but has a different runtime, permissions model, network boundary or dependency version.

Failure mode: the deployment looks like a product bug when it is really an environment-contract mismatch.

Guardrail: machine-readable environment manifest captured before go-live, with hard/soft compatibility checks.

### 2. Happy-path onboarding passes, production load breaks
Initial data and traffic succeed; realistic volume, concurrency or customer-specific edge cases do not.

Failure mode: onboarding declares success before the risky state has been exercised.

Guardrail: minimum production-shaped smoke pack tied to the customer's actual usage profile.

### 3. Reproduced issue loses customer context
The technical bug is reproduced internally but the account-specific constraint that made it damaging disappears from the ticket.

Failure mode: technically correct fix, operationally wrong resolution.

Guardrail: reproduction record must preserve business impact, triggering state and affected workflow—not only stack trace.

### 4. Architecture knowledge lives in the FDE's head
Deployment works because one engineer knows the exceptions and sequence.

Failure mode: future incident response starts from archaeology.

Guardrail: generate a compact deployment contract after go-live: dependencies, assumptions, ownership, exception paths, rollback points.

### 5. Repeated issue never becomes reusable prevention
A similar failure appears across customers but is treated as separate support work.

Failure mode: FDE headcount scales with recurring preventable complexity.

Guardrail: every repeated incident gets classified as product gap, documentation gap, automated preflight candidate or customer-specific exception.

## Smallest executable version

For each deployment, produce a five-part artifact:

`environment manifest -> production-shaped smoke tests -> reproduction capsule -> deployment contract -> recurrence classification`

The useful outcome is not "better notes." It is knowing which deployment risks can be detected before an FDE has to rediscover them manually.