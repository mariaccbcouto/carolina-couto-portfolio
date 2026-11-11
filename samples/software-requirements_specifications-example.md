# Software Requirements & Functional Specification (SRS)
## **Medical Imaging Platform: Automated DICOM Anonymization Module**

**Document ID:** SRS-MED-2026-02  
**Version:** 2.0  
**Date:** 01/10/2026  
**Author:** Carolina Couto  
**Document Type:** Public Portfolio Sample  
**Status:** Approved  

---

### **1. System Overview & Objective**
The purpose of this module is to automatically sanitize incoming DICOM (Digital Imaging and Communications in Medicine) datasets by stripping or replacing Protected Health Information (PHI) metadata tags prior to cloud storage or cross-institution sharing, ensuring strict compliance with GDPR and HIPAA frameworks.

### **2. Scope & User Roles**
* **In Scope:** Automated tag scrubbing, audit log generation, and manual review queue for flagged anomalies.
* **Out of Scope:** Image pixel data modification (pixel masking/burning) and manual DICOM viewer editing.
* **User Roles:** 
  * *System Administrator:* Configures global anonymization profiles.
  * *Clinical Data Officer:* Reviews quarantined files and approves audit reports.

---

### **3. Functional Requirements (SRS)**

| Requirement ID | Module / Feature | Description | Priority |
| :--- | :--- | :--- | :--- |
| **REQ-01** | DICOM Tag Parsing | The system must ingest `.dcm` and compressed `.zip` study archives and parse standard DICOM dictionary headers (Part 6). | **High** |
| **REQ-02** | PHI Data Scrubbing | The system must automatically empty or pseudonymize Level 2 safety tags (e.g., PatientName `(0010,0010)`, PatientID `(0010,0020)`). | **Critical** |
| **REQ-03** | Audit Log Trail | Every anonymization action must generate an immutable log entry containing timestamp, user ID, and modified tag keys. | **High** |
| **REQ-04** | Quarantine Exception | If a parsing error or unrecognised private tag occurs, the dataset must be immediately moved to a secure quarantine bucket. | **Medium** |

---

### **4. Data Flow & Logic**
```text
[ Incoming DICOM File ]
|
v
{ REQ-01: Parse Header } —(Error/Invalid)—> [ Quarantine Bucket (REQ-04) ]
|
(Valid)
v
{ REQ-02: Scrub PHI Tags } —> [ Sanitized DICOM Output ]
|
v
{ REQ-03: Generate Immutable Audit Log }
```

---

### **5. Error Handling & Edge Cases**
* **Corrupted Metadata:** If a file lacks mandatory DICOM headers, the ingestion pipeline aborts the process for that specific file, flags an error code (`ERR_DICOM_PARSE_01`), and routes it to the quarantine queue.
* **Network Interruption:** In case of sudden storage failure during the scrubbing process, transactions must roll back automatically to prevent partial or corrupted state persistence.  

---

> ⚠️ **COMPLIANCE NOTE:** All pseudogenerated IDs must use a cryptographic hashing algorithm (SHA-256) mapped securely against an internal, encrypted lookup table to allow authorized clinical re-identification if legally mandated.

---

*Public Portfolio Sample - Software Requirements & Functional Specification*
