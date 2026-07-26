The four mandatory Human Approval Gates positioned at the boundary of each lifecycle stage. For a cGMP-compliant system, the agent cannot advance to the next step until the human coordinator physically signs off at these points.
________________________________________
The 4 Human Approval Gates in the CAPAFlow Loop
1.	[Stage 1: Intake]  
2.	GATE 1: CONTAINMENT SIGN-OFF 
3.	[Stage 2: Investigation]
4.	GATE 2: RCA & DISPOSITION LOCK
5.	[Stage 3: CAPA Plan] 
6.	GATE 3: PLAN AUTHORIZATION 
7.	[Stage 4: Effectiveness] 
8.	GATE 4: SYSTEM CLOSURE
________________________________________
Detailed Gate Specifications & User Actions
Gate 1: Containment & Ingestion Sign-Off (End of Stage 1)
•	The Artifacts Reviewed: The Agent-compiled OOS Summary, the completed Missing-Info Checklist, and the simulated ERP Quarantine Confirmation.
•	What the Human Can Do:
o	Approve: Confirms that containment is successful and the correct material batch is locked down in the simulated ERP system. This officially advances the system to Stage 2 (Investigation).
o	Edit: Corrects any parsed batch metadata or manually forces data fields if the agent flagged them as missing but the human has them physically on hand.
o	Reject: Declares the intake invalid (e.g., if the lab mistakenly sent a testing run alert instead of a true commercial batch failure). This cancels the record.
o	Escalate: If the agent flags that the simulated warehouse inventory block failed to execute over the API, the human escalates a priority ticket to IT Operations and Warehouse Security to manually lock the physical cage.
Gate 2: RCA & Batch Disposition Lock (End of Stage 2)
•	The Artifacts Reviewed: The Chronological Evidence Table, compiled Interview Summaries, and the prioritized Root-Cause Hypotheses (e.g., the PLC jumper wire).
•	What the Human Can Do:
o	Approve: Selects and confirms the definitive root cause category, signs the final Batch Disposition Decision (Reject/Destroy), and appends rows to rca.csv and batch_disposition.csv. This unlocks Stage 3.
o	Edit: Rewrites or appends notes to the agent-generated interview text blocks to reflect missing nuances from the manufacturing floor.
o	Reject: Disagrees with the agent's top hypotheses, ordering a manual re-investigation or supplementary lab testing.
o	Escalate: Triggers an immediate escalation if the regulatory_impact field dictates a Field Alert Report (FAR) or Product Recall. This loops in Site Executives, Legal Counsel, and Regulatory Affairs boards within the statutory window. 
Gate 3: CAPA Plan Authorization (End of Stage 3)
•	The Artifacts Reviewed: The draft Corrective and Preventive Actions matrix, assigned Task Owners, Milestone Deadlines, and Change-Control (CC) Flags.
•	What the Human Can Do:
o	Approve: Locks the action items, targets, and dates, pushing the formal drafts into active Change Control tracking. This transitions the record into Stage 4 (Active Monitoring).
o	Edit: Modifies deadlines based on plant resource availability, or changes task ownership assignments (e.g., swapping engineers).
o	Reject: Sentences the plan back to draft mode if the corrective actions do not mathematically or scientifically solve the root cause verified in Gate 2.
o	Escalate: Escalates to Plant Operations Management (simulated) if a required preventive action requires significant capital expenditure (CAPEX) or extended facility downtime or sectional quarantine.
Gate 4: Closure Readiness & System Release (End of Stage 4)
•	The Artifacts Reviewed: The completed Monitoring Checklist (verifying the next 3 consecutive Xorbitacycline batches passed OOS criteria in the simulated LIMS), closed Change Controls, and the absolute audit-facing Closure-Readiness Summary.
•	What the Human Can Do:
o	Approve: Verifies the Effectiveness Check passed flawlessly. Applying an electronic signature here permanently shifts the simulated QMS status to CLOSED and archives the entire data lineage for regulatory inspectors.
o	Edit: Adds final closing remarks or cross-references future preventative maintenance log IDs for long-term tracking.
o	Reject: If a validation batch fails during the monitoring window, the human Rejects closure readiness. This forces the system to loop back to Stage 2 to re-investigate why the initial fix failed.
o	Escalate: Escalates to Global Quality Directors if systemic, multi-site pattern failures are identified during the evaluation window. 
