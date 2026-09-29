# Phishing Email Investigation Lab

A hands-on **Phishing Email Investigation & Analysis** repository focused on SOC Analyst workflows, email header analysis, authentication validation, URL investigation, IOC extraction, threat intelligence, and incident reporting.

The objective of this project is to investigate suspicious emails using real-world email evidence and document the investigation using a repeatable SOC workflow.

---

## 🎯 Objectives

This project demonstrates the ability to:

* Investigate suspicious and potentially malicious emails
* Analyze complete email headers
* Understand email delivery paths
* Analyze SPF, DKIM, and DMARC results
* Identify sender and Reply-To inconsistencies
* Extract URLs and domains from emails
* Analyze tracking and redirect URLs
* Extract and defang IOCs
* Distinguish spam, legitimate bulk email, and phishing
* Investigate suspicious attachments
* Perform basic threat-intelligence enrichment
* Map relevant activity to MITRE ATT&CK where applicable
* Build professional SOC investigation reports
* Preserve evidence and maintain an investigation timeline

---

## 🛡️ Investigation Workflow

Each case follows a repeatable investigation process:

```text
Suspicious Email
       │
       ▼
Evidence Collection
       │
       ├── Email Headers
       ├── Message Metadata
       ├── Email Body
       ├── URLs
       └── Attachments
       │
       ▼
Header Analysis
       │
       ├── From
       ├── Reply-To
       ├── Return-Path
       ├── Received Headers
       └── Message-ID
       │
       ▼
Email Authentication
       │
       ├── SPF
       ├── DKIM
       └── DMARC
       │
       ▼
URL / Domain Analysis
       │
       ├── URL Extraction
       ├── Redirect Analysis
       ├── Domain Analysis
       └── IOC Extraction
       │
       ▼
Threat Intelligence
       │
       ├── VirusTotal
       ├── AbuseIPDB
       ├── URLScan
       └── Other Relevant Sources
       │
       ▼
Behavioral Analysis
       │
       ├── Social Engineering
       ├── Credential Harvesting
       ├── Malware Delivery
       └── Financial Fraud
       │
       ▼
Verdict
       │
       ├── Benign / Legitimate
       ├── Spam
       ├── Suspicious
       └── Phishing / Malicious
       │
       ▼
SOC Investigation Report
```

---

# 📂 Repository Structure

```text
phishing-email-investigation/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── cases/
│   ├── CASE-001-compTIA-marketing/
│   ├── CASE-002/
│   ├── CASE-003/
│   ├── CASE-004/
│   └── CASE-005/
│
├── tools/
│   ├── extract_headers.py
│   ├── extract_urls.py
│   ├── decode_urls.py
│   ├── extract_iocs.py
│   └── README.md
│
├── templates/
│   ├── phishing-investigation-report.md
│   ├── investigation-checklist.md
│   └── case-template.md
│
├── datasets/
│   └── README.md
│
└── docs/
    ├── methodology.md
    ├── phishing-analysis-playbook.md
    └── investigation-workflow.md
```

---

# 🔎 Case Organization

Each investigation is stored as an individual case.

Example:

```text
CASE-001-compTIA-marketing/
│
├── README.md
│
├── evidence/
│   ├── headers-sanitized.txt
│   ├── urls.txt
│   └── iocs.csv
│
├── analysis/
│   ├── header-analysis.md
│   ├── authentication-analysis.md
│   └── url-analysis.md
│
└── report/
    └── incident-report.md
```

This structure separates:

**Evidence → Analysis → Findings → Final Report**

---

# 🧪 Investigations

## CASE-001 — CompTIA Marketing Email

**Classification:** Legitimate Bulk/Commercial Email

**Initial Source:** Gmail Spam folder

**Investigation Focus:**

* Email authentication
* Header analysis
* Sender infrastructure
* Bulk-mail indicators
* URL tracking
* Social-engineering analysis
* Spam vs phishing distinction

### Key Findings

The investigation identified:

* SPF authentication passed
* DKIM authentication passed
* DMARC authentication passed
* From and Reply-To addresses were consistent
* The message was delivered through Sailthru infrastructure
* Bulk-mail indicators were present
* List-Unsubscribe headers were present
* Marketing/tracking infrastructure was present
* The message used urgency-based promotional language
* No malicious attachment was identified
* No clear credential-harvesting behavior was established from the available evidence

### Preliminary Verdict

```text
LEGITIMATE BULK / COMMERCIAL EMAIL
```

The message being located in the Gmail Spam folder does **not by itself establish that the email is phishing**.

This case is included specifically to demonstrate an important SOC investigation principle:

> Spam ≠ Phishing

An analyst should evaluate authentication, infrastructure, URLs, content, sender identity, and other evidence before reaching a conclusion.

---

# 🧰 Tools & Technologies

## Email Analysis

* Gmail "Show Original"
* Python `email` module
* Regular expressions
* Email header analysis

## Authentication

* SPF
* DKIM
* DMARC
* ARC

## IOC Analysis

* URLs
* Domains
* IP addresses
* Email addresses
* Message IDs
* Hashes
* Attachments

## Threat Intelligence

Potential enrichment sources include:

* VirusTotal
* AbuseIPDB
* URLScan
* AlienVault OTX
* WHOIS/RDAP
* DNS information

## Security Frameworks

* MITRE ATT&CK
* Incident Response lifecycle
* IOC-based investigation

---

# 🐍 Python Automation

The `tools/` directory contains scripts used to automate repetitive investigation tasks.

Planned utilities include:

### Header Extraction

```bash
python tools/extract_headers.py email.eml
```

Extracts:

* From
* To
* Reply-To
* Return-Path
* Subject
* Date
* Message-ID
* Received headers
* Authentication results

### URL Extraction

```bash
python tools/extract_urls.py email.eml
```

Extracts URLs from:

* Plain-text content
* HTML content

### URL Analysis

```bash
python tools/decode_urls.py urls.txt
```

Used to identify:

* Tracking parameters
* Encoded values
* Redirect destinations
* Domains
* Suspicious URL structures

### IOC Extraction

```bash
python tools/extract_iocs.py email.eml
```

Produces structured IOC information.

Example:

```text
IOC Type       Value
-------------  --------------------------
Email          attacker@example.com
Domain         example.com
IP             192.0.2.10
URL            hxxps://example[.]com/login
Hash           SHA256...
```

---

# 📊 Investigation Methodology

Every case should answer five major questions:

### 1. Who sent the email?

Analyze:

* From
* Reply-To
* Return-Path
* Display name
* Sender domain

### 2. Did the email actually originate from the claimed infrastructure?

Analyze:

* SPF
* DKIM
* DMARC
* Received headers
* Sending IP
* Mail infrastructure

### 3. What is the email trying to make the recipient do?

Look for:

* Credential submission
* Payment
* Attachment execution
* Link clicking
* MFA approval
* Account verification
* Password reset
* Data submission

### 4. What technical indicators are present?

Extract:

* Domains
* URLs
* IP addresses
* Email addresses
* File names
* Hashes
* Redirects

### 5. What is the final classification?

Possible classifications:

```text
Legitimate
Spam
Suspicious
Phishing
Malware Delivery
Business Email Compromise
Credential Harvesting
Financial Fraud
```

The final classification must be based on documented evidence rather than a single indicator.

---

# 📝 Investigation Reports

Each case contains a professional investigation report covering:

1. Executive Summary
2. Incident Metadata
3. Email Metadata
4. Header Analysis
5. Authentication Analysis
6. Sender Infrastructure
7. URL Analysis
8. IOC Analysis
9. Social Engineering Analysis
10. Threat Intelligence
11. MITRE ATT&CK Mapping
12. Timeline
13. Impact Assessment
14. Verdict
15. Recommended Actions
16. Evidence

---

# 📚 Datasets

This project may use publicly available email datasets for controlled investigation exercises.

Potential sources include:

* Enron Email Dataset
* CEAS-08
* Nazario Phishing Corpus
* Nigerian Fraud Dataset
* SpamAssassin Public Corpus
* Ling-Spam

Dataset usage and licensing information should be documented in:

```text
datasets/README.md
```

Private emails are **not** intended to be published in this repository.

---

# 🔐 Privacy & Security

This repository is intended for cybersecurity education and portfolio demonstration.

Before publishing an investigation:

* Remove personal email addresses
* Remove personal names where unnecessary
* Remove phone numbers
* Remove private message content
* Remove authentication tokens
* Remove tracking identifiers where appropriate
* Sanitize Message-IDs when necessary
* Do not publish passwords or credentials
* Do not publish private attachments
* Do not publish sensitive mailbox information

Private/raw evidence should remain local.

Public GitHub repositories should contain sanitized evidence and analysis.

---

# ⚠️ Safe Analysis Practices

Suspicious URLs should **not** be opened directly in a normal browser.

Investigation should preferably use:

```text
Extract
   ↓
Defang
   ↓
Decode
   ↓
Analyze
   ↓
Threat Intelligence
```

Example:

```text
https://malicious.example.com/login
```

should be represented in reports as:

```text
hxxps://malicious[.]example[.]com/login
```

This reduces the chance of accidental interaction with malicious infrastructure.

---

# 🎓 Learning Outcomes

After completing this project, I aim to be able to:

* Investigate phishing emails independently
* Read and interpret email headers
* Explain SPF, DKIM, and DMARC
* Identify email spoofing indicators
* Analyze sender infrastructure
* Extract and investigate IOCs
* Analyze suspicious URLs
* Recognize common phishing techniques
* Differentiate spam from phishing
* Produce professional SOC investigation reports
* Automate repetitive email-analysis tasks with Python
* Communicate investigation findings clearly

---

# 🚀 Project Roadmap

## Phase 1 — Email Fundamentals

* [x] Gmail Show Original
* [x] Email header collection
* [x] SPF analysis
* [x] DKIM analysis
* [x] DMARC analysis
* [x] Received-header analysis

## Phase 2 — Investigation

* [x] Case 001
* [ ] Case 002
* [ ] Case 003
* [ ] Case 004
* [ ] Case 005

## Phase 3 — Threat Intelligence

* [ ] VirusTotal enrichment
* [ ] AbuseIPDB enrichment
* [ ] URLScan investigation
* [ ] WHOIS/RDAP analysis
* [ ] DNS analysis

## Phase 4 — Automation

* [ ] Header extraction script
* [ ] URL extraction script
* [ ] URL decoding
* [ ] IOC extraction
* [ ] Automated report generation

## Phase 5 — SOC Integration

* [ ] Convert email IOCs into SIEM queries
* [ ] Build phishing triage checklist
* [ ] Create detection rules
* [ ] Create response playbook
* [ ] Integrate investigation workflow with SOC tooling

---

# 💼 SOC Skills Demonstrated

This project demonstrates practical experience with:

```text
Email Security
       │
       ├── Phishing Investigation
       ├── Header Analysis
       ├── SPF / DKIM / DMARC
       ├── IOC Extraction
       ├── URL Analysis
       ├── Threat Intelligence
       ├── Social Engineering Analysis
       ├── Incident Documentation
       └── Python Automation
```

These skills are relevant to:

* SOC Analyst L1
* SOC Analyst L2
* Security Operations
* Incident Response
* Threat Detection
* Email Security
* Threat Intelligence
* Blue Team Operations

---

# 👨‍💻 Author

**Suhas Jadhav**

Cybersecurity | SOC Analyst | Blue Team | Threat Detection

Focus areas:

* Security Operations
* SIEM
* Incident Response
* Threat Detection
* Email Security
* Python Automation
* MITRE ATT&CK

---

# ⚠️ Disclaimer

This repository is intended for educational, defensive-security, and authorized security-analysis purposes.

All investigations should be performed only on emails, systems, datasets, and infrastructure that you are authorized to analyze.
