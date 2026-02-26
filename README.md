# DDT Standards
### Digital Double Technologies — Identity Permission Infrastructure

*The missing operational layer for consent-governed digital identities.*

---

This repository contains **public standards-track proposals and specifications** for Digital Double Technologies (DDT).

DDT is a non-enforcing, informational system for binding creator-declared consent and 
identity context to media using C2PA / Content Credentials — and for enabling 
revocation-aware permission verification at the moment of use.

---

## The Gap DDT Addresses

The ecosystem for digital content provenance has made remarkable progress:

- **C2PA** logs provenance
- **CAWG** defines identity and authority  
- **JPEG Trust** expresses rights terms

What none of them currently address is the live operational question at the moment of use:

> *"Is this identity use authorized right now?"*

That question cannot be answered by provenance metadata or a rights vocabulary alone. 
It requires a live, revocation-aware system that knows the current permission state of 
a specific identity and can respond at the moment of use.

DDT is building that infrastructure — starting with two primitives:

**CRO — Consent Receipt Object**  
A portable, machine-verifiable record that permission existed at a specific point in 
time. Hashed for tamper-evident reference. Auditable across its full lifecycle.

**IPS — Identity Permission State**  
A live, cryptographically verifiable permission-state endpoint. The closest analogy 
is OCSP for TLS certificates — except instead of answering "is this certificate 
still valid?", IPS answers "is this identity permission still valid right now?"

---

## C2PA Extension Proposal

DDT has filed a formal C2PA extension proposal for the `org.c2pa.digital-likeness` 
assertion namespace.

The proposal introduces no new cryptographic primitives inside C2PA. It defines 
structured pointer fields and optional hash references that any conformant permission 
authority can support. Designed to be fully complementary to CAWG and JPEG Trust.

→ [Issue #3 — Proposal: org.c2pa.digital-likeness](https://github.com/digitaldoubletechnologies/ddt-standards/issues/3)

---

## Non-Enforcement Posture (Core)

DDT standards are **informational only**.

They MUST NOT be used for:
- moderation
- ranking
- suppression
- enforcement
- takedowns
- behavioral or policy decisions

DDT expresses declared consent and usage visibility, not compliance, legality, 
or obligation.

---

## What Lives Here

- Draft specifications (v0.x)
- Public proposals and discussion issues
- Non-enforcement and platform-safety clarifications
- C2PA-aligned extension exploration (consent/rights visibility)

## What Does NOT Live Here

- Private implementations
- Internal automation outputs
- Sensitive operational details
- Enforcement mechanisms
- Legal determinations

---

## Structure

- `docs/` — specifications and public explainers
- `proposals/` — proposal drafts and supporting materials
- `specs/README.md` — standards-track specifications and schemas

## Contributing

Standards collaboration is welcome.  
Open an issue to propose changes or request discussion.

---

*All concepts and materials © 2026 DDT / Digital Double Technologies. 
Proprietary & Confidential.*
