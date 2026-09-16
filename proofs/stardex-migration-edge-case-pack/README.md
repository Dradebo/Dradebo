# Stardex — migration edge-case pack

Independent Forge-0 proof based on Stardex's public Customer Success Engineer / migration posture as of September 2026.

For an ATS/CRM migration, the dangerous failure is rarely 'the CSV would not import.' It is preserving operational truth when old systems carry messy history, ambiguous ownership and state that does not map cleanly.

## Five migration edge cases worth making explicit

### 1. Duplicate candidate identities
The same person exists under multiple emails, phone numbers or imported profiles.

Guardrail: deterministic merge rules plus a review queue for ambiguous identity collisions.

### 2. Historical stage semantics do not map 1:1
Old pipeline stages encode customer-specific meaning that the target system does not share.

Guardrail: stage translation table with explicit lossy mappings and human approval for ambiguous states.

### 3. Ownership points to departed or invalid users
Records reference recruiters/managers who no longer exist in the destination workspace.

Guardrail: orphaned-owner policy with reassignment evidence and audit trail.

### 4. Notes/attachments import but lose context
Free text and files migrate while chronology, author, candidate/job relationship or visibility permissions do not.

Guardrail: sampled provenance check across note/file types before cutover.

### 5. Incremental delta after dry run diverges from baseline
A test migration succeeds, but users continue editing the source before final cutover.

Guardrail: explicit delta strategy: freeze window, change capture or reconciled second pass with conflict report.

## Smallest executable version

Run every migration through five gates:

`identity reconciliation -> semantic mapping -> ownership repair -> provenance sampling -> delta reconciliation`

The useful output is a migration exception report that says exactly what cannot be moved cleanly before the customer discovers it after go-live.