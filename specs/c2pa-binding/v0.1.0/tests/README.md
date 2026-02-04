# Conformance & Example Vectors

This directory contains **illustrative conformance vectors** for the
DDT C2PA Assertion Binding Specification.

These files are not executable tests and do not define enforcement behavior.

---

## Purpose

The examples in this directory exist to:
- Demonstrate correct payload structure
- Illustrate lifecycle states (active, revoked, expired, superseded)
- Support human review and early interoperability discussion
- Aid implementers in understanding expected field semantics

They do **not**:
- Determine validity of content usage
- Assert compliance or non-compliance
- Require platform action or moderation
- Imply legal or contractual meaning

---

## Validation Expectations

Implementations MAY:
- Validate payloads against the published JSON Schema
- Resolve referenced CROs to evaluate lifecycle state
- Ignore unknown fields under `extensions`

Implementations MUST NOT:
- Treat payload presence as authorization
- Infer wrongdoing from lifecycle state
- Enforce or automate decisions based on these signals

---

## Relationship to DDT-000

All examples operate under the constraints defined in **DDT-000**  
(Non-Enforcing, Informational-Only Consent Signaling).
