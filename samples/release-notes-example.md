# Release Notes & Product Updates
## **Medical Imaging Platform: Version 2.1.0**

**Release Date:** October 20, 2026  
**Document ID:** RN-MED-2026-2.1  
**Target Audience:** System Administrators, Clinical Data Officers, and IT Integration Teams  

---

### 🚀 **Overview**
We are thrilled to announce the release of **Version 2.1.0** of the Medical Imaging Platform. This update introduces the long-awaited **Automated DICOM Anonymization Module**, alongside critical performance enhancements for cloud storage synchronization and improved security patches for HIPAA/GDPR compliance.

---

### ✨ **New Features**

* **Automated DICOM Anonymization Module (REQ-02):**
  * Introduced background pipeline processing to automatically strip and pseudonymize Level 2 safety tags (such as Patient Name and ID) upon ingestion.
  * Added a secure configuration panel for System Administrators to customize scrubbing rules per institutional department.

* **Secure Quarantine Bucket (REQ-04):**
  * Files lacking mandatory DICOM headers or containing unrecognised private tags are now automatically intercepted and safely routed to an isolated quarantine queue for manual review.

---

### 🛠️ **Improvements & Enhancements**

* **Audit Trail Immutability (REQ-03):** 
  * Enhanced the logging service to generate immutable timestamped trails for every batch anonymization process, ensuring complete audit readiness.
* **Ingestion Speed:** 
  * Optimized multi-threaded `.zip` study archive parsing, reducing bulk upload processing time by approximately 35%.

---

### 🐛 **Bug Fixes**

* **`ERR_DICOM_PARSE_01` Handling:** Resolved an edge-case bug where corrupted metadata streams occasionally caused pipeline timeouts. Systems now cleanly abort and log parsing exceptions without crashing service workers.
* **UI Toolbar Alignment:** Fixed a responsive layout bug in the Web Viewer toolbar on high-resolution diagnostic displays.

---

### ⚠️ **Upgrading & Breaking Changes**

* **Database Schema Migration:** Upgrading to v2.1.0 requires an automatic migration of the internal encrypted lookup table. Ensure database backups are performed prior to running the deployment script.
* **API Deprecation Notice:** Legacy endpoints under `/api/v1/scrub` are officially deprecated and will be removed in version 3.0. Please transition your integration scripts to `/api/v2/anonymize`.

---
**For technical support or assistance with this deployment, please contact our engineering support desk.**

---

*Public Portfolio Sample - Release Notes and Product Updates*
