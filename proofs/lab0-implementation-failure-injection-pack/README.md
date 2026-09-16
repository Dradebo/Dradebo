# Lab0 — implementation failure-injection pack

Independent Forge-0 proof based on Lab0's public implementation automation posture as of September 2026.

If the product is trying to automate discovery, configuration, integrations, testing and go-live, then the valuable edge is not only completing those stages. It is deliberately injecting the kinds of bad states that normally survive until production.

## Five failure injections worth institutionalizing

### 1. Discovery omission
A critical dependency, stakeholder constraint or exception path is absent from discovery.

Test: remove one required assumption and verify the implementation process detects that the plan is under-specified before build.

### 2. Configuration contradiction
Two requested settings are individually valid but mutually incompatible.

Test: inject conflicting requirements and require an explicit contradiction state rather than silent precedence.

### 3. Integration partial success
Transport succeeds but only a subset of required fields/events are valid.

Test: pass structurally valid but semantically incomplete data and require the system to distinguish partial success from readiness.

### 4. Test coverage blind spot
The scripted test suite passes, but a realistic customer-specific exception path was never exercised.

Test: compare discovered workflow branches against test coverage and fail readiness when meaningful branches remain untested.

### 5. Go-live rollback ambiguity
Production behavior degrades and the system can detect it, but there is no unambiguous rollback boundary or owner.

Test: inject a post-launch regression and require the implementation record to identify rollback point, decision owner and preserved state.

## Smallest executable version

For each implementation stage, maintain:

`required assumptions -> observed evidence -> contradiction set -> tested branches -> go-live readiness -> rollback contract`

Then deliberately corrupt one layer at a time and assert that the system stops for the right reason.

The useful artifact is not another checklist. It is a failure-injection harness for the implementation process itself.