# DDT C2PA Assertion Binding Specification v0.1.0
**Assertion Payload Name:** `ddt.cro_binding`  
**Spec Version:** 0.1.0  
**Status:** Standards-track (public)  
**Governing Doctrine:** DDT-000 (Non-Enforcing, Informational-Only Signaling)

---

## 0. Canonical posture (read first)
This specification defines a *privacy-preserving, reference-only* payload intended to be carried inside a C2PA custom assertion.

**DDT signals describe context. They do not determine outcomes.**  
This assertion payload:
- **references** an authoritative Consent Receipt Object (CRO),
- **does not grant consent**, and
- **does not assert legality, wrongdoing, or required action**.

A verifier MUST treat CRO lifecycle state as the sole authority for whether consent is valid.

---

## 1. Purpose
DDT’s goal is to ensure consent and identity context remain *cryptographically referencable* and *auditable* downstream, without embedding sensitive data inside media.

The `ddt.cro_binding` payload enables:
- binding a media asset’s provenance manifest to an authoritative CRO via **ID + receipt_hash**
- optional binding to an identity context object via **ID + identity_hash**
- machine-resolvable post-distribution checks of CRO lifecycle state (active/revoked/expired/superseded)
- forward-compatible evolution via an `extensions` bucket

---

## 2. Non-goals (explicit)
This specification does NOT define:
- DRM, playback blocking, degradation, or access control
- takedowns, moderation triggers, or enforcement instructions
- legal determinations or ownership claims
- a guarantee that metadata survives (platform stripping is real)
- prevention of screen-record / recapture attacks

---

## 3. Normative requirements

### 3.1 Privacy requirements
1) The payload MUST NOT contain plaintext PII.  
2) The payload MUST NOT contain raw biometrics.  
3) Identifiers MUST be opaque/tokens and MUST NOT be directly identifying.

### 3.2 Consent authority requirements
1) Consent validity MUST be determined exclusively by the CRO’s lifecycle state.  
2) The payload MUST reference CROs by:
   - `consent_receipt_id` (UUID), and
   - `receipt_hash` (digest of the CRO)
3) Any system that cannot validate the CRO reference MUST treat the asset as **non-DDT-compliant**.

### 3.3 Deterministic failure semantics (normative)
A verifier MUST mark the asset **non-DDT-compliant** if:
- required fields are missing or malformed
- the C2PA manifest is missing or signature verification fails
- CRO resolution fails (when required for a compliance determination)
- CRO hash mismatch is detected
- CRO lifecycle state is `revoked`, `expired`, or `superseded`

Unknown fields:
- MUST be safely ignored if placed under `extensions`

---

## 4. Payload schema and field semantics
The canonical JSON Schema for this payload is:

`specs/c2pa-binding/v0.1.0/ddt.cro_binding.schema.json`

### 4.1 Required fields
- `assertion_name` MUST equal `ddt.cro_binding`
- `spec_version` MUST be semver (e.g., `0.1.0`)
- `consent_receipt_ref` MUST contain:
  - `consent_receipt_id` (UUID)
  - `receipt_hash` (base64url digest)
  - `hash_alg` (currently `sha-256`)
- `extensions` MUST exist (empty object allowed)

### 4.2 Optional fields
- `identity_context_ref` MAY be present to reference an identity context object:
  - MUST be opaque (no PII)
  - MUST include `identity_hash` with `sha-256`
- `usage_policy_summary` MAY be present:
  - MUST be informational-only
  - MUST NOT be treated as a grant, a contract, or an instruction
- `revocation_reference` MAY be present:
  - provides a status endpoint for CRO lifecycle checking
  - does not override verifier-configured resolvers
- `media_binding` MAY be present:
  - optional integrity hints (never replaces C2PA signature validation)

---

## 5. Canonicalization and hashing (normative)

### 5.1 Canonical serialization
The `receipt_hash` MUST be computed over a canonical serialization of the CRO.

**Required rule:** use a deterministic canonical JSON serialization (e.g., JSON Canonicalization Scheme / JCS).  
All implementations MUST:
- produce a byte-identical canonical JSON encoding for the same CRO content
- treat whitespace, key order, and floating formatting deterministically per the chosen canonicalization

### 5.2 Hash algorithm
- `hash_alg` MUST be `sha-256` for v0.1.0
- digests MUST be base64url encoded (no padding), and stored as ASCII

### 5.3 What the hash means
A matching hash means only:
- “the referenced CRO content is the same as the canonical CRO resolved by the verifier.”

It does NOT mean:
- “use is authorized,”
- “rights are granted,” or
- “a platform must act.”

---

## 6. Resolution model (normative)
Verifiers MUST resolve CRO lifecycle state through one or more trusted methods:
- configured resolver(s) (recommended)
- optionally, `resolver_hint` and/or `revocation_reference.status_url` as hints

If a verifier cannot resolve required state to determine DDT compliance, it MUST fail closed for compliance purposes (asset is non-DDT-compliant), while still allowing a UI to present “unverifiable” as a descriptive outcome.

---

## 7. Verification order (recommended)
1) Verify C2PA manifest signature and integrity  
2) Extract the `ddt.cro_binding` payload  
3) Validate payload schema against `ddt.cro_binding.schema.json`  
4) Resolve CRO by `consent_receipt_id`  
5) Canonicalize resolved CRO and compute digest  
6) Compare digest to `receipt_hash`  
7) Check CRO lifecycle state
   - if `revoked` / `expired` / `superseded` → non-DDT-compliant
8) If present, resolve identity context and validate `identity_hash`

---

## 8. Examples and test vectors
Examples live at:

`specs/c2pa-binding/v0.1.0/examples/`

Notes:
- The `vector-*` files include **non-normative** conformance hints under `extensions.ddt_test_vector`.
- These hints are for testing only and MUST NOT be treated as authoritative state in production systems.

---

## 9. Evolution strategy
- Backward-compatible additions go to `extensions` or optional fields → MINOR bump
- Any change to required fields, meanings, or hashing rules → MAJOR bump
- Never change v0.1.0 behavior in place; publish v0.1.1 / v0.2.0 / v1.0.0 as new folders

---

## 10. Relationship to DDT canon
- DDT-000 governs “informational only, non-enforcing” posture.
- CRO lifecycle state remains the sole authority for consent validity.
- C2PA provides provenance integrity; DDT adds consent/identity *references* aligned with that model.
