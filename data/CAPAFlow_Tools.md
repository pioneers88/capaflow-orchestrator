The specific tools CAPAFlow will call during its lifecycle loop include:
1.	 Data Gathering & Analysis Tools
•	Read_Silo_Records (CSV Reader): Connects to the read-only file system to pull data rows from oos_events.csv, batch_records.csv, and lims_results.csv matching a specific batch number. It acts as the agent's primary sensory input.
•	Query_SCADA_Time_Window (Telemetry Filter): Instructs the backend database script to filter the massive scada_historian.csv file using the specific start and end timestamps extracted from the manufacturing batch log. It isolates the exact slice of hardware telemetry when the failure occured.
2.	 Compliance & Auditing Tools
•	Run_SOP_Gap_Check (SOP Compliance Evaluator): Parses the text constraints within capa_sop.md and runs an automated validation check against the collected data. It ensures mandatory variables—such as the lab manager's signature and the physical maintenance ticket link—are present before allowing the workflow to advance.
•	Analyze_Evidence_Consistency (Conflict Detector): Compares manual operator entries in the batch log against the automated SCADA telemetry data. If it detects a mismatch (e.g., the operator logs a normal status while the machine log captures a temperature plunge), it flags a systemic data conflict.
3.	Content Generation & Staging Tools
•	Generate_Draft_CAPA_Record (Artifact Synthesizer): Takes the unstructured data strings from the consolidated evidence loop and maps them into a structured, formal Markdown narrative layout matching the blueprint requirements specified in output_examples.md.
•	Prepare_Human_Approval_Payload (UI State Stager): Bundles the compiled evidence binder, the draft narratives, the anomaly highlights, and the required regulatory compliance alert tasks into a single structured JSON object. It delivers this payload to the web interface to render the human coordinator's decision dashboard.
4.	 Transactional Write Tools
•	Append_Human_RCA_Record (RCA Writer): Triggers an atomic file-write execution to append a row containing the coordinator's verified root cause analysis into rca.csv. This execution automatically injects the secure system timestamp and active user session data.
•	Commit_Batch_Disposition (Disposition Finalizer): Executes a secure row injection into batch_disposition.csv. Simultaneously, if a regulatory alert is flagged as critical, this tool communicates with the ERP mockup code to alter the batch status across the site's deployment tracker.
