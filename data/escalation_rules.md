Here are the five strict human escalation rules for the CAPAFlow Orchestrator agent, mapping out the precise system triggers and the exact architectural actions it takes to hand the work back to the human coordinator safely.
------------------------------
##  Human Escalation Rules Matrix

[System Loop Execution]
          │
          ├──► 1. MISSING DATA ───────► Abort Loop ──► Generate Gap Summary & Alert
          ├──► 2. LOW CONFIDENCE ─────► Stop Staging ──► Highlight Contradictory Rows
          ├──► 3. REGULATORY LANGUAGE ─► Inject Task ──► Flag Dossier & Alert Legal Board
          ├──► 4. OUT-OF-BOUNDARY ────► Block Entry ──► Wipe Context & Issue Warning
          └──► 5. HIGH-STAKES DECISION ─► Lock State ──► Render Form UI & Force Signature

------------------------------
##  Detailed Escalation Triggers & Agent Actions## 

1. Missing Data Trigger (Completeness Failure)

* The Trigger: The agent executes the Run_SOP_Gap_Check tool on oos_events.csv and finds that a potency OOS entry has a phase_1_status marked as "Open" or the lab_manager_signoff field is entirely blank/null.
* What CAPAFlow Does: The agent immediately aborts further data collection from the SCADA logs or batch records. It changes the local QMS record status to PENDING_LAB_CLOSURE, flags the record in red on the dashboard, and delivers an alert to the coordinator stating: "Automation halted. Cannot process CAPA for Batch XB-2026-546067 until QC Laboratory Management signs off on Phase I Lab Error assessment."

## 2. Low Confidence Trigger (Evidence Contradiction)

* The Trigger: The agent executes the Analyze_Evidence_Consistency tool and detects a flat numerical or textual contradiction between data silos. For example, batch_records.csv has an operator entry stating "Temp stable at 37C," but scada_historian.csv shows an active drop to 31.4C at that exact timestamp.
* What CAPAFlow Does: The agent ceases automated report drafting. It creates a special "Data Discrepancy Payload" that highlights the conflicting rows side-by-side using amber visual markers. It hands the file to the coordinator with an interactive prompt: "Evidence conflict detected between manual floor log and machine telemetry. Human adjudication required to determine true process timeline."

## 3. Legal / Regulatory Language Trigger (High-Risk Phrases)

* The Trigger: While scanning human-entered text strings or processing field data, the agent's NLP parser identifies critical GxP trigger words or codes, such as "FDA", "Health Canada", "FAR", "Recall", "Patient Harm", or a regulatory_impact value of "Critical_Field_Alert_Required".
* What CAPAFlow Does: The agent instantly escalates the record's priority to Critical. It automatically injects a mandatory, non-deletable sub-task into its draft checklist ([ ] Submit FDA Field Alert Report Form 3331a within 3 working days). It copies the event details and routes an automated high-priority email notification directly to the site’s Regulatory Affairs and Legal Counsel distribution boards.

## 4. Out-of-Boundary Request Trigger (Scope Guardrail)

* The Trigger: A user prompts the agent via an interface chatbox to perform an action outside its defined cGMP boundaries (e.g., "Change the target calibration temperature limit for Reaction Vessel 2 from 37°C to 34°C in the system configuration file" or "Delete row SCADA-4003 from the data historian").
* What CAPAFlow Does: The agent invokes a strict security block. It outputs a hardcoded system message: "Action denied. CAPAFlow Orchestrator is unauthorized to modify master equipment setpoints or delete historical data logs per ALCOA+ data integrity rules." It logs the unauthorized request, username, and timestamp to a hidden security audit trail, then wipes its short-term conversational context memory to prevent prompt injection.

## 5. High-Stakes Decision Trigger (Material Disposition)

* The Trigger: The workflow reaches the final sub-step of Stage 2 (Investigation) or Stage 4 (Effectiveness), where rows must be committed to rca.csv or batch_disposition.csv to choose the physical fate of the drug product (Release vs. Destruction).
* What CAPAFlow Does: The agent completely locks the workflow state inside the backend database, preventing further pipeline automation. It generates a Human Approval Payload which renders a modal form on the coordinator's screen. The agent stands down and waits passively until the coordinator manually selects a dropdown option, types their justification comments, and inputs their official electronic signature password to execute the file append.

------------------------------


