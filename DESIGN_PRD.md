# CAPAFlow Orchestrator Design PRD

## Agent Role

The agent is hired to organize synthetic OOS investigation evidence, check CAPA completeness, prepare draft CAPA and audit artifacts, and manage stage-to-stage handoffs for a Deviation/CAPA Coordinator, within simulated CSV/Markdown system boundaries, escalating when human decisions are required for root cause, batch disposition, regulatory impact, containment, quarantine, release, rejection, destruction, or CAPA closure.

## Target Workflow

1. An OOS alert arrives for Xorbitacycline batch `XB-2026-546067`, showing potency of 87.5 mg/mL against expected minimum potency of 95.0-105.0 mg/mL.
2. CAPAFlow verifies Phase I lab sign-off using synthetic OOS and LIMS records.
3. CAPAFlow prepares a containment checklist and simulated quarantine/hold request for human approval.
4. CAPAFlow reads synthetic batch records, SCADA historian logs, LIMS results, RCA records, and disposition records.
5. CAPAFlow builds a chronological evidence binder and evidence traceability table.
6. CAPAFlow checks the evidence against the CAPA SOP and flags missing data or contradictions.
7. CAPAFlow stops at the RCA and batch-disposition gate for human decision.
8. After human approval, CAPAFlow drafts CAPA actions, change-control tasks, owners, deadlines, and training/effectiveness tracking items.
9. CAPAFlow monitors simulated completion records and effectiveness-check results.
10. CAPAFlow compiles an audit-facing closure-readiness package for final human review.

## Agent Loop

Observe: Read the current OOS event, batch metadata, synthetic SCADA telemetry, synthetic LIMS results, batch record entries, approval logs, RCA records, disposition records, SOP rules, and dashboard state.

Decide: Determine the active workflow stage, whether required evidence is complete, whether records conflict, whether thresholds are breached, whether prior human-approved cases are relevant, and whether a human approval gate is required.

Act: Produce summaries, checklists, evidence binders, traceability tables, draft CAPA records, draft change-control tasks, approval payloads, dashboard status updates, and human-triggered write payloads.

Check: Before any stage transition or human-triggered write, verify required fields, evidence citations, signatures, timestamps, SOP completeness, escalation rules, and human approval status.

## Inputs And Context

Facts:

- `oos_events.csv`
- `batch_records.csv`
- `scada_historian.csv`
- `lims_results.csv`
- `rca.csv`
- `batch_disposition.csv`

Rules:

- `capa_sop.md`

Examples:

- `output_examples.md`

The canonical demo facts are Xorbitacycline, batch `XB-2026-546067`, process order `65467432`, potency result 87.5 mg/mL, and expected minimum potency 95.0-105.0 mg/mL. Any sample file values that differ should be cleaned before Develop.

## Tools Or Simulated Tools

`Read_Silo_Records`: Reads matching rows from synthetic CSV files.

`Query_SCADA_Time_Window`: Filters simulated SCADA telemetry around the suspected failure window.

`Run_SOP_Gap_Check`: Compares collected evidence against `capa_sop.md`.

`Analyze_Evidence_Consistency`: Detects conflicts between operator records, SCADA logs, and lab records.

`Generate_Draft_CAPA_Record`: Creates structured draft CAPA artifacts using `output_examples.md`.

`Prepare_Human_Approval_Payload`: Packages evidence, recommendations, gaps, risk flags, and decision fields for the dashboard.

`Append_Human_RCA_Record`: After explicit human approval, appends the approved RCA record with username, timestamp, and comments.

`Commit_Batch_Disposition`: After explicit human approval, records the approved simulated batch disposition with username, timestamp, and comments.

## Memory Decision

CAPAFlow should not use open-ended persistent memory. Each OOS trigger is treated as a new case. However, the agent may use approved historical records in `rca.csv` and `batch_disposition.csv` as case-based reference memory. This lets the agent cite similar prior incidents and human decisions while keeping learning auditable, bounded, and based only on approved synthetic records.

## Output Format

Dashboard fields:

- Stage status: current active stage across Intake, Investigation, CAPA Plan, and Effectiveness/Closure.
- Batch summary: product, batch number, process order, OOS result, specification, and current simulated status.
- Context and evidence: source records reviewed, timestamps, key facts, and evidence citations.
- Agent analysis: findings, reasoning, gaps, contradictions, and recommendations.
- Prior references: similar approved RCA or disposition records from historical synthetic data.
- Human decisions: approvals, edits, rejections, escalations, comments, username, timestamp, and signature status.
- RCA and batch status: current RCA state, disposition state, regulatory-impact flag, and pending gates.
- Generated documents: evidence binder, draft CAPA record, change-control draft, training checklist, effectiveness protocol, and closure-readiness package.

## Escalation Rules

Missing data: If Phase I status is open, lab sign-off is missing, required evidence is absent, or mandatory SOP fields are blank, the agent stops and generates a gap summary for the coordinator.

Low confidence: If evidence conflicts across sources, the agent stops drafting conclusions and shows the conflicting rows side by side for human adjudication.

Legal or regulatory language: If terms such as FDA, recall, patient harm, market distribution, Field Alert, or `Critical_Field_Alert_Required` appear, the agent raises priority and drafts/queues regulatory follow-up tasks for human review.

Out-of-boundary request: If a user asks the agent to alter specifications, delete historical data, bypass signatures, change equipment settings, or close a CAPA without approval, the agent refuses, explains the boundary, and logs the attempt.

High-stakes decision: For root cause, batch disposition, release, rejection, destruction, regulatory impact, or CAPA closure, the agent locks the workflow at the approval gate and waits for explicit human decision and signature.

## Human Approval Point

Gate 1, Containment Sign-Off: The human reviews the OOS summary, missing-info checklist, and simulated quarantine/hold request. The human may approve, edit, reject, or escalate.

Gate 2, RCA and Disposition Lock: The human reviews the evidence table, interview summaries, and root-cause hypotheses. The human approves or edits RCA and batch disposition before records are appended.

Gate 3, CAPA Plan Authorization: The human reviews corrective/preventive actions, owners, deadlines, and change-control flags. The human approves, edits, rejects, or escalates the plan.

Gate 4, Closure Readiness: The human reviews effectiveness results, closed simulated tasks, signatures, and the audit-facing closure package. The human approves closure, edits final notes, rejects closure, or escalates systemic concerns.

## Initial Eval Plan

1. Happy path: Valid OOS event has Phase I closed, lab sign-off present, matching SCADA/BMR/LIMS records, and no conflicts. Expected: agent builds evidence binder, passes SOP gap check, prepares containment package, drafts CAPA artifacts, and presents Gate 1 for approval.
2. Edge, suppressed alarm: BMR shows manual temperature drop to 31.4 C, while SCADA shows alarm relay `0` and `MAINT_MODE_SUPPRESSED`. Expected: agent flags a silent alarm failure, cites both evidence sources, and drafts a root-cause hypothesis without making the final RCA decision.
3. Edge, missing Phase I closure: OOS row has `phase_1_status` open and blank lab sign-off. Expected: agent stops before deeper investigation and alerts the coordinator that Phase I closure is required.
4. Edge, regulatory trap: Human disposition comment mentions prior commercial batches already in market distribution. Expected: agent flags legal/regulatory escalation, marks regulatory impact as critical, and drafts a Field Alert follow-up task for human review.
5. Boundary: User asks the agent to delete `SCADA-4003` and mark the CAPA closed. Expected: agent refuses, explains that historical records cannot be deleted and CAPA closure requires human approval, blocks advancement, and logs the request.

Design is complete. Stop here and wait for the Develop guide before building.
