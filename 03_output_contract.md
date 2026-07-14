# Output Contract

The literal JSON shape the LLM must return on every turn. This is what engineering codes the integration against.

| Key | Definition |
|---|---|
| status | One of exactly four values: `ready_for_create` \| `needs_clarification` \| `rejected` \| `unsupported`. Never an ad-hoc/invented value. |
| resolved_fields | Object keyed by field name. Each entry: `{ value, confidence: "high"\|"medium"\|"low", source: "direct"\|"inferred"\|"default" }`. |
| assumptions | Array of plain-language strings, one per medium-confidence default applied (e.g. minimum tenure, carry forward, requires approval). Must use human-readable field names, never snake_case. |
| missing_fields | Array of field names still needed before the policy can be created. Only fields with no default ever appear here. |
| clarification | `{ "question": "<text>" }` — REQUIRED (never null) whenever status = needs_clarification. One consolidated natural-language question, capped at 4 fields per turn. |
| rejection_reasons | Array, one entry per distinct blocking issue — if a prompt has more than one hard-reject problem, report all of them, not just the first found. |
| scope_note | Explicit note if the original prompt implied broader scope than the single policy actually being configured. Null if the original prompt was already narrow and specific — do not manufacture a note where there's no drift. |
| final_payload | Object of resolved field values only, present only when status = ready_for_create; null otherwise. |

**Fallback rule:** If no other rule in this spec cleanly applies to a request, default to `status = unsupported` and explain why in `rejection_reasons`. `status` must always be exactly one of the four enumerated values — never output anything else, under any circumstance, even when the situation isn't covered elsewhere in this spec.

**Hard rule:** Internal snake_case identifiers (employment_type, leave_type, accrual_method, etc.) are ONLY used as JSON keys. Any text a person reads — `clarification.question`, `rejection_reasons`, `assumptions` — must use plain field names ("employment type", "leave type"…), never the internal key.
