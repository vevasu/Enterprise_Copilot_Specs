# Scope Boundary Spec

What the system will not do, and how it says so — distinct from a missing or invalid field, because the request itself falls outside what one policy can represent.

| Boundary | Rule | Required behavior / message |
|---|---|---|
| Multiple policies in one request | This system creates exactly ONE leave policy per request. | If a request asks for more than one policy (multiple leave types, or an explicit count like "create 2 policies"), return `status = unsupported`. `rejection_reasons` must state that this system creates one policy at a time and the user should submit each as a separate request. |
| Priority over other missing fields | This check takes priority over collecting other missing fields when both problems exist at once (e.g. country is given, but employment type/leave type are also missing AND the request implies multiple policies). | Do not also ask about employment type, leave type, etc. in the same turn — report the scope violation first, before anything else. |

**Note:** only these two entries exist so far. Encashment, scope drift, and other undefined-scenario rules are intentionally not included yet.
