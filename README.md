# Publicly Accessible Database Backup — Mediroza Hospital

**NETWORKWALKS Cybersecurity Internship — Final Project**

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Objectives](#project-objectives)
- [Environment and Tools](#environment-and-tools)
- [Assessment Journey](#assessment-journey)
  - [1. Reconnaissance](#1-reconnaissance)
  - [2. Directory Discovery](#2-directory-discovery)
  - [3. Database Backup Exposure](#3-database-backup-exposure)
  - [4. Database Inspection](#4-database-inspection)
  - [5. Vulnerability Documentation](#5-vulnerability-documentation)
- [Attack Path](#attack-path)
- [Vulnerability Findings](#vulnerability-findings)
- [Security Impact](#security-impact)
- [Remediation Priorities](#remediation-priorities)
- [What I Learned](#what-i-learned)
- [Project Deliverables](#project-deliverables)
- [Repository Structure](#repository-structure)
- [Evidence and Disclosure](#evidence-and-disclosure)
- [Ethical Scope](#ethical-scope)
- [Author](#author)

---

## Project Overview

This project documents an individual black-box web application security assessment conducted as the final project of the Networkwalks Cybersecurity Internship.

The assessment involved performing passive and active reconnaissance against the Mediroza General Hospital website to identify potential security weaknesses.

During reconnaissance, I inspected the website's publicly accessible `robots.txt` file and discovered a reference to an old application directory. Further investigation revealed that the directory contained a publicly accessible SQL database backup.

The backup file could be opened directly through a web browser without authentication. Inspection of the SQL dump revealed database structures and records containing sensitive employee and shareholder information.

This finding demonstrated how improperly exposed legacy directories and database backups can lead to significant sensitive information disclosure.

> **Public Disclosure Note:** This repository is intended to serve as a sanitised cybersecurity portfolio project. Personal information, individual database records, national identification numbers, contact details, salary values and other sensitive information must not be published.

## Project Objectives

The assessment focused on the following objectives:

- Perform passive and active reconnaissance against the target website.
- Examine publicly accessible resources for information disclosure.
- Inspect the website's `robots.txt` file.
- Identify potentially exposed directories and files.
- Investigate discovered resources for security misconfigurations.
- Verify whether sensitive resources were accessible without authentication.
- Examine the exposed SQL backup and identify sensitive database structures.
- Document the vulnerability, potential impact and recommended remediation.

## Environment and Tools

The assessment was performed using Kali Linux.

**Tools and techniques used:**

- Kali Linux
- Web Browser
- `robots.txt` Inspection
- Directory Browsing and Enumeration
- Browser-Based SQL File Inspection
- HTTP Response Observation
- Manual Vulnerability Analysis
- Technical Evidence Collection
- Security Vulnerability Reporting

---

## Assessment Journey

### 1. Reconnaissance

The assessment began with passive and active reconnaissance against the target website.

During this phase, I examined publicly accessible resources to identify potentially sensitive information and exposed application directories.

One resource I inspected was the website's `robots.txt` file.

The inspection revealed an old directory referenced under a `Disallow` directive.

**Key Observation:** A directory that was not intended for search engine crawling was publicly discoverable through the website's `robots.txt` file.

### 2. Directory Discovery

After identifying the directory in `robots.txt`, I navigated to the directory through my web browser.

The directory exposed a listing of its contents, which included a database backup file named:

```text
mediroza_db_backup_2019.sql
```

This discovery indicated that directory indexing was enabled and that a potentially sensitive backup file was exposed through the web server.

**Finding:** Publicly accessible legacy directory exposing sensitive files.

### 3. Database Backup Exposure

I selected the SQL backup file from the directory listing.

The file opened directly in my web browser without requiring a username, password or any form of authentication.

This confirmed that the database backup was retrievable by an unauthenticated visitor.

**Exposed Resource:**

```text
mediroza_db_backup_2019.sql
```

**Finding:** Publicly accessible database backup without authentication.

### 4. Database Inspection

After accessing the backup, I inspected the SQL file directly in the browser.

The database information identified in the backup included:

| Attribute | Details |
|---|---|
| Database Name | `mediroza_hr` |
| Database Type | MySQL |
| Backup Date Indicated | 27 August 2019 |

Two tables containing sensitive information were identified.

**Staff Table (`staff`)**

The table contained employee-related information, including:

- Employee ID
- Full Name
- Job Title
- Department
- Email Address
- Telephone Number
- National Identification Number
- Monthly Salary
- Employment Commencement Date

**Shareholders Table (`shareholders`)**

The table contained shareholder-related information, including:

- Shareholder Name
- Percentage of Ownership
- Number of Shares Held
- Share Classification

**Database Statistics:**

- 30 staff records
- 10 shareholder records

Individual records and personal values are intentionally excluded from this public documentation.

### 5. Vulnerability Documentation

Following the discovery and inspection, I documented the vulnerability in a technical security report.

The report covered:

- Vulnerability Description
- Affected Resource
- Technical Discovery Process
- Steps to Reproduce
- Observed and Expected Results
- Security Impact
- Recommended Remediation
- Supporting Screenshots and Evidence

The finding was classified as **High (Provisional)** due to the sensitivity of the information exposed.

---

## Attack Path

The discovery process followed this sequence:

```text
Target Website
      |
      v
Passive and Active Reconnaissance
      |
      v
robots.txt Inspection
      |
      v
Discovery of Legacy Directory
      |
      v
Public Directory Listing
      |
      v
SQL Database Backup Discovered
      |
      v
Unauthenticated Browser Access
      |
      v
SQL Backup Inspection
      |
      v
Sensitive Staff and Shareholder
Information Identified
      |
      v
Vulnerability Documentation
```

The vulnerability was demonstrated through ordinary web browsing and inspection of the publicly accessible SQL backup.

No authentication bypass, server-side shell, malware deployment, persistence or destructive modification was required to demonstrate this finding.

## Vulnerability Findings

The primary finding documented in this assessment was:

| ID | Severity | Finding |
|---|---|---|
| F01 | High (Provisional) | Publicly accessible database backup exposing sensitive information |

### Vulnerability Classification

- **Category:** Sensitive Information Disclosure
- **CWE:** CWE-530 – Exposure of Backup File to an Unauthorized Control Sphere
- **OWASP:** A05:2021 – Security Misconfiguration
- **Authentication Required:** None observed

## Security Impact

The exposure of the database backup could have several security implications.

### Identity Theft

Exposure of employee national identification numbers and personal information could facilitate identity fraud.

### Targeted Phishing

Employee names, departments, job titles and email addresses could be used to construct convincing phishing campaigns.

### Privacy Violations

Disclosure of employee contact information and salary records could compromise personal privacy.

### Corporate Information Disclosure

Shareholder identities, ownership percentages and share classifications could expose confidential organizational information.

### Social Engineering

The disclosed information could be used to impersonate employees or manipulate organizational personnel.

---

## Remediation Priorities

### Immediate Actions

- Remove the exposed database backup from the publicly accessible web directory.
- Restrict public access to the affected directory.
- Preserve and review relevant web server access logs.
- Assess whether unauthorized parties accessed or downloaded the backup.

### Short-Term Actions

- Store database backups outside the web root.
- Implement appropriate access controls and authentication for backup storage.
- Disable directory indexing where it is not required.
- Review the web server for other exposed backup files and sensitive resources.
- Restrict public access to sensitive file extensions and backup directories.

### Long-Term Actions

- Implement a secure database backup management policy.
- Encrypt backups at rest and during transfer.
- Conduct periodic security assessments.
- Introduce continuous monitoring for exposed sensitive resources.
- Establish appropriate data protection and incident response procedures.

> **Important:** Removing a directory or filename from `robots.txt` does not resolve the underlying vulnerability. The database backup itself must be removed from public access.

---

## What I Learned

### Reconnaissance Can Reveal More Than Expected

The inspection of a seemingly ordinary `robots.txt` file led to the discovery of a publicly accessible legacy directory and a sensitive database backup.

### Information Disclosure Is a Serious Security Issue

A database backup does not need to be actively exploited to create a security risk. Making sensitive information publicly accessible is itself a significant security weakness.

### Directory Indexing Can Expose Sensitive Resources

Improperly configured directory listings can reveal files that should only be available to authorised personnel.

### Evidence-Based Reporting Matters

Identifying a vulnerability is only one part of penetration testing. Documenting the discovery process, demonstrating accessibility, explaining the potential impact and providing actionable remediation recommendations are equally important.

### Security Misconfigurations Can Expose Critical Information

This assessment reinforced the importance of secure backup storage, appropriate access controls and proper web server configuration.

---

## Project Deliverables

A technical Security Vulnerability Report documenting the publicly accessible database backup, including:

- Vulnerability Overview
- Executive Summary
- Technical Details
- Steps to Reproduce
- Security Impact
- Recommended Remediation
- Supporting Screenshots and Evidence
- Conclusion and Severity Assessment

The report is included in this repository in a sanitised format.

## Repository Structure

```text
networkwalks-B082-week4-mediroza-pentest/
│
├── evidence/
│   ├── 01-robots-txt-directory-disclosure.png
│   ├── 02-public-directory-listing.png
│   └── 03-database-backup-structure-redacted.png
│
├── report/
│   └── Security_Vulnerability_Report.pdf
│
└── README.md
```

## Evidence and Disclosure

The evidence included in this repository should be sanitised to demonstrate the vulnerability without exposing personal or confidential information.

The following information must not be published:

- Employee national identification numbers
- Employee telephone numbers and email addresses
- Individual salary records
- Shareholder personal information
- Raw SQL database backups
- Other confidential organisational information

The original database contents are not included in this repository.

## Ethical Scope

This project was conducted as an individual cybersecurity assessment under the Networkwalks Cybersecurity Internship.

The documentation describes the activities performed and observations recorded during the assessment.

The project is presented for educational and defensive cybersecurity purposes. Sensitive information and unnecessary live-target details are excluded from the public repository.

## Author

**Chimezie Uche Samuel**

Networkwalks Cybersecurity Internship  
Final Individual Penetration Testing Project

**GitHub:** (https://github.com/its-overlord)

---

**Project Focus:** Web Application Security | Reconnaissance | Directory Enumeration | Sensitive Information Disclosure | Vulnerability Assessment | Security Reporting
