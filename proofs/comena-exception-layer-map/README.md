# Comena — exception layer map

Independent Forge-0 proof based on Comena's public positioning around automating operational work without forcing teams to redesign their existing processes first.

If that promise holds, the highest-risk layer is not the happy path. It is the moment when the automation becomes uncertain and has to hand control back to a person.

## Four exception states worth making explicit

### 1. Missing context
The automation reaches a decision point without enough information to continue safely.

Bad outcome: guessing, silent defaulting, or sending a vague task to a human.

Better state: `BLOCKED — missing X`, with the smallest next action needed to resume.

### 2. Conflicting evidence
Two connected systems disagree about the same customer, order, document, status, or policy condition.

Bad outcome: one source silently wins.

Better state: `CONFLICT — source A vs source B`, with provenance and an explicit decision owner.

### 3. Policy ambiguity
The workflow reaches a case that falls outside a known rule or matches more than one rule.

Bad outcome: encode an accidental business policy in automation logic.

Better state: `REVIEW — rule boundary`, capturing the human decision so it can later become a deliberate rule if repeated.

### 4. External dependency failure
A third-party API, person, vendor or system does not respond or returns an ambiguous outcome.

Bad outcome: endless retries, duplicate actions, or a workflow that looks complete when it is not.

Better state: `WAITING — external dependency`, with retry policy, evidence and timeout/escalation owner.

## The useful exception object

Every exception should carry five fields:

`what happened -> why automation stopped -> evidence -> current owner -> smallest next action`

That turns exceptions from ad-hoc Slack messages into structured operational data.

## Why this matters

The happy path proves automation can run.

The exception layer proves the business can trust it.

If repeated exception classes are recorded cleanly, they become the training data for the next round of process improvement rather than disappearing into human workarounds.