# Enterprise Copilot Specs

A reference specification for building enterprise AI copilots that convert complex configuration pages into natural language workflows.

The goal of this repository is not to build an LLM application, but to document the product specifications required to reliably translate user intent into deterministic enterprise configurations.

---

## Problem

Enterprise products expose hundreds of configuration options through complex forms.

Traditional UI requires users to understand:

- field names
- dependencies
- enums
- mandatory inputs
- validation rules
- business constraints

Modern copilots should instead allow users to simply describe what they want.


The copilot should convert that request into a valid configuration without requiring the user to navigate multiple forms.

Building this reliably requires much more than prompting an LLM.

---

## What this repository contains

This repository documents the specification layer required before an LLM can successfully automate enterprise configuration.

Current documents include:

| File | Purpose |
|-------|----------|
| `01_field_spec.md` | Canonical definition of every configurable field |
| `02_scope_boundary.md` | Defines what the copilot can and cannot perform |
| `03_output_contract.md` | Structured output schema returned by the LLM |
| `golden_dataset_leave_policy_copilot.xlsx` | Evaluation dataset for prompt and model testing |

---

## Why these specifications matter

Large Language Models understand language.

Enterprise systems require precision.

Between these two lies a translation layer.

Typical responsibilities include:

- Intent extraction
- Entity resolution
- Canonical field mapping
- Enum normalization
- Validation
- Ambiguity detection
- Clarification handling
- Output schema enforcement
- Confidence estimation

Without these specifications, enterprise copilots become unreliable and difficult to evaluate.

---

## Repository Structure

```
Enterprise_Copilot_Specs/

├── 01_field_spec.md
├── 02_scope_boundary.md
├── 03_output_contract.md
└── golden_dataset_leave_policy_copilot.xlsx
```

---

## Intended Audience

This repository is useful for:

- Product Managers
- AI Product Managers
- Solution Architects
- Prompt Engineers
- LLM Application Developers
- Enterprise Platform Teams

---

## Design Philosophy

The repository follows a deterministic approach to enterprise AI.

```
Natural Language
        ↓
Intent Detection
        ↓
Entity Resolution
        ↓
Canonical Field Mapping
        ↓
Validation
        ↓
Structured Output
        ↓
Enterprise API
```

Rather than relying on prompt engineering alone, the specifications define explicit contracts between user language and enterprise systems.

---

## Example

User:

> "Create a leave policy that gives new employees 12 casual leaves after probation."

Expected output:

```json
{
  "policy_name": "New Employee Leave Policy",
  "leave_type": "Casual Leave",
  "eligibility": "Post Probation",
  "annual_entitlement": 12
}
```

The LLM should generate only valid fields defined by the specification.

---

## Evaluation

The repository includes a golden dataset for evaluating:

- Field extraction accuracy
- Intent resolution
- Enum mapping
- Missing field detection
- Clarification generation
- Structured output correctness

This enables repeatable evaluation across prompt versions and model upgrades.

---

## Future Additions

Planned documents include:

- Intent Catalogue
- Entity Resolution Specification
- Prompt Design Guide
- Guardrail Specification
- Clarification Strategy
- Tool Calling Specification
- Validation Rules
- Confidence Framework
- Error Recovery Strategy
- Evaluation Framework
- Architecture Reference

---

## License

This repository is intended as a reference implementation for designing enterprise AI copilots and natural-language configuration systems.
