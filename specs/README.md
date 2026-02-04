# DDT Standards — Specs Index

This directory contains **standards-track** specifications for Digital Double Technologies (DDT).

All specs in this repository operate under **DDT-000** (Non-Enforcing, Informational-Only Signaling).  
DDT signals describe context. They do not determine outcomes.

---

## Published (standards-track)

### C2PA Binding (Consent Reference-Only) — v0.1.0
**Purpose:** Define a privacy-preserving, reference-only payload intended to be carried inside a C2PA custom assertion, binding media to an authoritative Consent Receipt Object (CRO) via **ID + receipt hash** (no PII, no biometrics).

- Spec: `specs/c2pa-binding/v0.1.0/c2pa_assertion_binding_v0_1.md`
- Schema: `specs/c2pa-binding/v0.1.0/ddt.cro_binding.schema.json`
- Examples & vectors: `specs/c2pa-binding/v0.1.0/examples/`

---

## Contributing
- If you are reviewing as a standards body/vendor/platform partner: please start with **DDT-000**.
- If you are implementing: start with the spec doc above, then validate payloads against the schema.
