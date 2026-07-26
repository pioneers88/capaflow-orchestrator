# CAPAFlow Orchestrator

A capstone prototype: an AI agent that helps a pharmaceutical Deviation/CAPA Coordinator organize evidence and draft CAPA documentation for an Out-of-Specification (OOS) investigation — while keeping every regulated decision (root cause, batch disposition, regulatory impact, CAPA closure) under explicit human approval.

**This is a prototype, not a production system.** All data is 100% synthetic and fictional — a fictional drug, fictional batches, fictional operators. It is piloted under human review, not deployed autonomously.

## What it does

The console walks one case through five stages:

1. **Input** — the OOS case details load.
2. **Context** — linked batch records, SCADA telemetry, LIMS results, prior RCA/disposition records, and the CAPA SOP policy.
3. **Decision** — the agent (and optionally a second, independent CAPAFlow Supervisor Agent) analyzes the evidence and returns a status with its reasoning.
4. **Output** — a labeled CAPA plan: batch summary, evidence reviewed, analysis, prior references, pending human decisions, and generated documents.
5. **Review** — a human coordinator must Approve, Edit, or Escalate before anything counts as final. Nothing advances without one of these three actions.

An **Evals** view records honest pass/fail verdicts across six test scenarios, including a boundary case the agent must refuse and a documented before/change/after fix.

## Running it

This is a single self-contained file — `index.html` — with no build step and no server required.

1. Open `index.html` in a browser (double-click it, or visit the hosted link).
2. Open **Settings** and paste your own Anthropic API key. It's stored only in your browser's `localStorage` — never written to any file, never sent anywhere but directly to the Anthropic API from your browser.
3. Pick a case (or a one-click eval scenario chip) and click **Run**.

No key, no agent calls — you'll see a clear first-load state pointing you to Settings instead of a blank page or an error.

## What's in this repo

```text
index.html     the entire prototype — HTML, CSS, and JavaScript, no dependencies
data/          synthetic case data and eval scenario descriptions (reference)
policies/      the SOP the agent is instructed to follow
design/        the locked design tokens and skin definitions used for styling
```

## Known limitations

- Handles only two synthetic OOS cases for one fictional product — not tested against real manufacturing data, other products, or volume.
- English-only, plain-text data in the exact embedded record shape — no file upload, OCR, or real LIMS/SCADA/ERP connection.
- One case at a time, one API call per run, no cross-session memory — Run Log and Eval results live only in the visitor's browser.
- Legal/regulatory and boundary detection depend on explicit system prompt rules and can miss novel phrasing; Anthropic's own safety classifier can also independently block a request — confirmed reproducibly on one paraphrased regulatory eval case, documented as a known constraint rather than an app defect.
- The "coordinator name" field is a plain label for log attribution, not authentication.
