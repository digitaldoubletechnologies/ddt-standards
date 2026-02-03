# C2PA Performer Consent & Digital Likeness Usage Extension — v0.1 (Skeleton)

**Status:** Draft (Standards Seed)  
**Posture:** Informational / Non-Enforcing  
**Target Forum:** C2PA Technical Working Group (Exploratory)

---

## 1. Purpose

Define a conservative, C2PA-compatible mechanism for expressing **visibility-only signals** related to:
- performer consent scope
- digital double permissions
- training usage signals
- revocation references

This extension does **not** enforce behavior or imply legal determinations.

---

## 2. Non-Enforcement Doctrine (Normative)

This extension MUST be interpreted as **informational only**.

It MUST NOT be used for:
- moderation
- ranking
- suppression
- enforcement
- takedowns
- behavioral or policy decisions

It expresses declared consent and usage visibility, not compliance, legality, or obligation.

---

## 3. Claim Categories (Draft)

### 3.1 Performer Consent Assertion
Visibility claim indicating consent scope at time of capture.

Examples:
- capture_only
- editorial_use
- promotional_use
- synthetic_generation_allowed: false

Non-meaning:
- not ownership
- not compliance
- not guarantee of downstream behavior

---

### 3.2 Digital Double Declaration
Visibility claim indicating whether captured material may be used for synthetic representation.

Non-meaning:
- not an enforcement promise

---

### 3.3 Training Permission Signal
Advisory signal for machine learning usage:
- allow / deny / unspecified

Non-meaning:
- not an automated enforcement instruction

---

### 3.4 Revocation Reference
Reference to updated consent state or audit trail.

Non-meaning:
- not takedown
- not retroactive erasure
- not platform obligation

---

## 4. Privacy Requirements

- No plaintext PII or raw biometrics
- Indirect references only (hashed/tokenized)
- Opt-in only

---

## 5. Open Questions

- Minimal viable claim set for v0.1
- Posthumous consent escalation paths
- Multi-party ensemble consent modeling
- Cross-jurisdiction conflicts

---

## 6. Next Steps

- Map claims to C2PA extension patterns
- Produce example manifests (standard capture / denied / revoked / training excluded)
- Legal and abuse-risk review of semantics
- Prepare submission memo for C2PA TWG
