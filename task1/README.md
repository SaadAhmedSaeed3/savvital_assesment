# Task 1 — AI-Powered Estate Planning Intake Triage

## Overview

An n8n workflow that accepts estate planning client profiles via an interactive web form (single client) or batch file upload (CSV / JSON / XLSX), sends each profile to the Groq LLM API, and returns `recommended_instruments`, `rationale`, and `urgency_flag` per client.

---

## Prompt Design Choices

The prompt uses a two-part structure: a **system message** that locks in the advisor persona and enforces JSON-only output before any client data arrives, and a **user message** that presents the profile in a consistent labelled format. Instruments are enumerated explicitly — rather than letting the model invent names — so every recommendation maps to a real legal document. Urgency criteria are embedded directly with concrete thresholds (age 65+, 2+ complicating factors, under-40 with no dependents) so the model applies deterministic triage logic rather than guessing. Temperature is set to 0.1 for near-deterministic, auditable output across repeated runs.

## One Production Change

Replace prompt-based JSON parsing with Groq's native JSON mode (`response_format: { type: "json_object" }`), which enforces the output schema at the inference level. This eliminates the regex fallback entirely and guarantees all required fields are present — a fragility that is unacceptable at production volume.

## Human-Review Step

After parsing the output, an IF node checks `urgency_flag === "High"`. For High-urgency cases, a **Email** delivers the structured recommendation and rationale to the estate planning team with an approve/modify button. An n8n **Wait node** pauses execution pending attorney sign-off via webhook callback. Approved recommendations route to the client; rejected ones send the attorney's revised version instead. Medium cases receive async email review only; Low cases auto-approve immediately.
