# Standard Operating Procedure (SOP): Deviation and CAPA Management

**SOP ID**: QA-SOP-0042  
**Version**: 4.0  
**Effective Date**: January 15, 2026  
**Applicability**: Global Quality Management Systems  

## 1. Objective
To define the automation, ingestion, processing, and closure routing requirements for Out-of-Specification (OOS) investigations. 

## 2. Agent Execution Constraints (Boundaries)
The automated system (CAPAFlow Orchestrator) is authorized to ingest telemetry, execute data aggregation, audit documentation completeness, and issue temporary ERP isolation holds. 

### 2.1 Critical Human Escalation Gates
The agent MUST pause execution and hand the workflow over to the human Deviation/CAPA Coordinator if any of the following parameters are encountered:
1. **Root Cause Analysis (RCA)**: The agent may correlate data anomalies, but the final designation of a systemic root cause requires human adjudication.
2. **Material Disposition**: Any decision to **Release**, **Reject**, **Quarantine**, or **Destroy** commercial manufacturing batches requires explicit human coordinator validation.
3. **Regulatory Impact**: Cross-contamination risks or multi-product manufacturing line exposure decisions must be human-led.

## 3. Mandatory Checklist for Ingestion Completeness
Before drafting a CAPA record, the system must verify the presence of:
* Confirmed Phase I Laboratory Investigation Status = `Closed_Confirmed`.
* Validated digital signature from the Laboratory Manager.
* Manufacturing batch log matching the timestamp of the telemetry exception.
