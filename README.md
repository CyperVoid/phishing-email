#  Phishing Email Security Assessment Report

This repository documents a security analysis project focused on **phishing detection**. The workflow systematically compares a malicious email against a legitimate baseline, using an 8-step process to confirm the attack. The findings highlight critical failures in technical authentication and expose classic social engineering tactics.

Tasks List 

1.Obtain a sample phishing email (many free samples online).
2.Examine sender's email address for spoofing.
3.Check email headers for discrepancies (using online header analyzer).
4.Identify suspicious links or attachments.
5.Look for urgent or threatening language in the email body.
6.Note any mismatched URLs (hover to see real link).
7.Verify presence of spelling or grammar errors.
8.Summarize phishing traits found in the email.

---

### 1. Key Findings Summary

The email is **conclusively malicious** based on a complete failure of email authentication protocols and the use of classic social engineering tactics designed for credential theft.

| Threat Category | Finding | Status |
| :--- | :--- | :--- |
| **Authentication** | SPF, DKIM, and DMARC checks **FAIL**. | **Critical** |
| **Infrastructure** | Sender IP is **Actively Blacklisted** (Known Spam/Botnet source). | **High Risk** |
| **Call-to-Action** | Link redirects to a **Mismatched, Fraudulent URL**. | **High Risk** |
| **Social Engineering** | Uses high-pressure language and poor grammar/spelling. | **Confirmed** |

---
### 3. Technical Evidence & Analysis (Tasks 2, 3, 4)

The analysis of the email header provides the technical proof of fraud:

* **Authentication Failure (Task 3):** The sending domain fails all three primary security protocols, confirming the message is unauthorized:
    * **SPF (Sender Policy Framework):** The sending server's IP was unauthorized by the legitimate domain's security record.
    * **DKIM (DomainKeys Identified Mail):** The cryptographic signature was invalid or missing.
    * **DMARC (Policy):** The email failed the domain's configured authentication policy check.
* **Infrastructure & Blacklisting (Task 3):** The email originated from a low-reputation, disposable **Virtual Private Server (VPS)** whose IP address was found on public blacklists, identifying it as a known source of malicious traffic.
* **Spoofing (Task 2):** The visible sender's display name mimicked the legitimate company, but the underlying `Return-Path` address belonged to an unrelated, untrusted third-party domain.

### 3. Authentication Results Comparison (Technical Proof)

The table below summarizes the technical verification of the email's legitimacy based on header analysis (Task 3). This highlights the fundamental difference between trusted and malicious infrastructure.

| Security Feature | Legitimate Email | Phishing Email | Implication |
| :--- | :--- | :--- | :--- |
| **Sender Server** | High-reputation (e.g., Amazon SES) | Unknown, disposable **VPS** | Phisher uses throwaway infrastructure. |
| **SPF** (Sender Authorization) | **PASS** | **FAIL** / Missing | Sender is unauthorized to use the domain. |
| **DKIM** (Content Integrity) | **PASS** | **NONE** / Invalid | Content cannot be verified as authentic. |
| **Blacklist Status** | Clean / Trusted | **Actively Blacklisted** | Sender IP is a known source of spam/malware. |
| **Conclusion** | **TRUSTED** | **MALICIOUS** | Confirmed security threat. |
---

### 4. Social Engineering & Attack Vector (Tasks 5, 6, 7)

The content analysis confirms the attack relies on manipulation to succeed:

* **Mismatched URL (Task 6):** The core attack vector is a fraudulent link. The visible text claims to link to the official website, but inspection shows the actual destination is a **credential harvesting site** on a non-affiliated domain.
* **Urgency & Threat (Task 5):** The body uses coercive phrases ("Immediate Action Required," "Account Will Be Suspended") to evoke **panic**. This tactic bypasses the user's critical thinking, forcing a fast click.
* **Quality Indicators (Task 7):** The presence of **spelling errors, awkward phrasing, and inconsistent formatting** confirms the lack of professional quality control typically seen in legitimate corporate communications.

---

### 5. Summary of Workflow Completion (Task 1 & 8)

The analysis successfully completed the 8-step workflow, moving from sample acquisition (Task 1) through technical verification and social engineering analysis, culminating in this conclusive summary (Task 8).
