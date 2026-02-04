# C2PA Binding Spec — v0.1.0

**Spec name:** DDT C2PA Assertion Binding Specification  
**Payload name:** `ddt.cro_binding`  
**Version:** 0.1.0  
**Posture:** Non-enforcing, informational-only (see DDT-000)

This spec defines a **privacy-preserving, reference-only** payload intended to be carried inside a C2PA custom assertion. It references an authoritative Consent Receipt Object (CRO) by **ID + receipt hash** and supports machine-resolvable lifecycle checking (active / revoked / expired / superseded) via external resolution.

Nothing in this spec grants consent, asserts legality, or requires platform action.

---

## Files

- Full spec: `c2pa_assertion_binding_v0_1.md`
- Schema: `ddt.cro_binding.schema.json`
- Examples & vectors: `examples/`

---

## Quick start (implementers)
1) Read the spec (`c2pa_assertion_binding_v0_1.md`).  
2) Validate payload JSON against `ddt.cro_binding.schema.json`.  
3) Treat CRO lifecycle as the sole authority for consent validity.  
4) Unknown future fields must go under `extensions` and be safely ignored.
