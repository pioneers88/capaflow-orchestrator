# CAPAFlow Orchestrator Discovery PRD

## User

The user is a Deviation/CAPA Coordinator in a fictional pharmaceutical manufacturing site. The coordinator is responsible for managing an Out of Specification investigation after a manufactured drug batch fails a potency test. The coordinator uses the agentic workflow to organize evidence, coordinate investigation stages, prepare CAPA documentation, track approvals, and present closure-readiness materials for human review.

## Workflow

The workflow is an OOS-triggered CAPA investigation for a fictional oral antibiotic product called Xorbitacycline. The agentic system acts as an Orchestrator Agent that guides the coordinator through four bounded workflow slices in sequence:

1. Intake, triage, and containment checklist
2. Investigation evidence organization and root-cause hypothesis support
3. CAPA action-plan drafting and owner/deadline tracking
4. Effectiveness-check tracking and closure-readiness checklist

Each slice produces a structured handoff artifact. The coordinator reviews and approves the output before the Orchestrator Agent passes it to the next slice.

## Trigger

The workflow starts when fictional batch `XB-2026-546067`, process order `65467432`, fails a QC potency test. The batch result is 87.5 mg/mL potency against a minimum expected specification of 95.0-105.0 mg/mL. This triggers an OOS investigation and CAPA workflow.

## Current Process

Today, the coordinator manually manages the CAPA investigation across disconnected systems and teams.

1. Verify that QC has completed the initial lab investigation and confirmed the issue is not a simple laboratory error.
2. Open a CAPA record and manually enter batch number, material ID, product name, failed potency result, and deviation metadata.
3. Confirm containment by checking quarantine status, batch hold status, and warehouse handling records.
4. Gather evidence from separate sources such as SCADA logs, batch manufacturing records, QC assay reports, maintenance records, operator interviews, and training records.
5. Coordinate cross-functional review with Production, Engineering, Quality Assurance, Validation, and Regulatory Affairs.
6. Document the approved root cause after human investigation and review.
7. Draft corrective and preventive action items with owners, due dates, dependencies, and change-control flags.
8. Track execution of maintenance fixes, SOP updates, training completion, and change-control closure.
9. Monitor effectiveness checks across future batches.
10. Assemble the final CAPA package for QA Director review and formal closure decision.

## Pain Points

The biggest pain point is evidence traceability. Critical information is scattered across paper records, SCADA exports, QC reports, approval logs, CAPA logs, change-control tasks, and training records. The coordinator spends too much time hunting for documents and manually proving which evidence supports each CAPA decision.

A second pain point is slow handoff between teams. Investigation tasks, signatures, reviews, and approvals are coordinated through emails, meetings, physical folders, and spreadsheets, making it hard to know who has completed what.

A third pain point is weak visibility into downstream dependencies. CAPA actions may depend on change control, equipment repair, SOP updates, operator training, and future effectiveness checks, but those activities are often tracked separately.

A fourth pain point is audit preparation. Preparing an FDA-style audit package requires manually assembling evidence, sign-offs, timestamps, CAPA status, and effectiveness results into a coherent record.

## Agent Opportunity

The agentic opportunity is to create an Orchestrator Agent that coordinates four subsidiary workflow assistants. The agent does not make regulated decisions. Instead, it helps the coordinator by organizing evidence, checking completeness, preparing draft artifacts, and managing handoffs.

The Orchestrator Agent can:

1. Summarize the OOS event and intake metadata.
2. Build a containment and missing-information checklist.
3. Extract relevant facts from synthetic SCADA logs, batch records, and QC assay reports.
4. Create an evidence traceability table linking each finding to a source document.
5. Draft root-cause hypotheses for human review.
6. Draft CAPA action items with owners, due dates, and dependencies.
7. Flag when change control, training, or effectiveness monitoring may be needed.
8. Track approved handoffs from one workflow slice to the next.
9. Produce a draft CAPA record and audit-facing approval checklist.

## Synthetic Data Plan

The demo will use only fictional and synthetic data. The synthetic dataset will include:

1. OOS event record for fictional product Xorbitacycline.
2. Batch record for process order `65467432` and batch `XB-2026-546067`.
3. QC assay report showing potency of 87.5 mg/mL against a minimum expected 95.0-105.0 mg/mL.
4. SCADA historian excerpt showing a temperature sensor communication issue and suppressed alarm state.
5. Operator batch manufacturing record showing a manual temperature reading of 31.4 C against a 37.0 C target.
6. In-process QC assay report suggesting a temperature-excursion-related process impact.
7. CAPA workflow log showing stage status, generated artifacts, and coordinator approvals.
8. Approval log showing who reviewed each handoff and when.
9. Change-control task records for alarm repair, PLC alarm review, SOP updates, and training.
10. Effectiveness-check records showing later synthetic batches meeting defined potency criteria after corrective and preventive actions.

## Human Boundary

The agent cannot make autonomous decisions about batch disposition, root cause approval, regulatory impact, product release, product rejection, product destruction, or CAPA closure.

The agent may suggest actions, organize evidence, draft documentation, and prepare checklists, but a qualified human must approve all regulated conclusions and all workflow transitions. The coordinator or appropriate QA authority must approve the root cause, CAPA plan, batch disposition, effectiveness criteria, and final CAPA closure. The agent must log who approved each step, what was approved, and when.

## Success Metric

The primary success metric is evidence traceability: the percentage of CAPA draft sections, recommendations, checklist items, and handoff artifacts that are linked back to a specific synthetic evidence source.

Secondary metrics are faster handoffs of accurate data between workflow stages and improved simulated CAPA closure time. In the demo, this can be shown by comparing a manual checklist-style process against the agent-assisted workflow dashboard.

## Initial Demo Idea

The demo will show a dashboard with the four workflow slices arranged in sequence. The coordinator starts with the synthetic OOS event for Xorbitacycline batch `XB-2026-546067`. The Orchestrator Agent processes the intake package, creates a containment checklist, and waits for human approval. After approval, it hands the approved package to the investigation assistant, which organizes the synthetic SCADA log, batch record, and QC assay report into an evidence table and draft root-cause hypothesis. After human approval, the CAPA planning assistant drafts corrective and preventive actions, owners, deadlines, and change-control flags. After approval, the effectiveness assistant prepares monitoring criteria and a closure-readiness checklist.

The visible final output will be a four-stage dashboard, handoff artifacts between stages, a draft CAPA record, an evidence traceability table, and a human approval checklist suitable for a fictional FDA-style audit package.

Discovery is complete. Stop here and wait for the Design guide before moving forward.
