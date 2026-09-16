# Screenpipe — privacy boundary checklist

Independent Forge-0 proof based on Screenpipe's public local-first desktop activity capture model as of September 2026.

The product gets more valuable as it sees more of a user's activity. That makes the trust boundary itself part of the product.

## Boundary questions a serious user should be able to answer quickly

### 1. What is captured?
- screen frames
- OCR/text
- audio/transcripts
- window/app metadata
- user-created pipes/automations

The UI should make current capture scope visible without requiring documentation archaeology.

### 2. Where does each class of data live?
For every data class, expose:
- local path/store
- retention policy
- whether any derived representation leaves the device
- which feature or integration can cause egress

### 3. What crosses the boundary when AI features run?
A local-first architecture can still invoke remote models or external APIs.

Useful guardrail: before any external call, expose exactly which payload leaves the device, destination/provider, and whether the action is user-triggered or automatic.

### 4. What can third-party pipes access?
Plugins/extensions are effectively another trust domain.

Useful guardrail: capability manifest per pipe — e.g. read OCR, read audio, network access, filesystem write, background execution — with user-visible permission changes.

### 5. How can a user verify the claim?
Trust improves when privacy is inspectable rather than promised.

Potential proof surfaces:
- live outbound-request log
- per-feature data-flow panel
- permission manifest for each pipe
- retention/deletion inspector
- one-click export of privacy-relevant events

## Smallest useful artifact

A single "Privacy Boundary" panel:

`captured locally -> stored locally -> processing path -> external egress (if any) -> retention/deletion`

Each arrow should be inspectable and linked to the actual event/request that caused it.

The proposition is simple: local-first is strongest when the user can audit the boundary without trusting marketing copy.