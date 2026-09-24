### Phishing Email Analysis

## Overview

This lab documents the analysis of a suspicious email using its raw headers, sender information, authentication results, embedded links, and external reputation checks.

The purpose was to determine whether the message was legitimate or part of a phishing attempt.

## Scenario

An employee received an email claiming that their account had been disabled because of unusual activity. However, the employee was still able to access the account normally, which made the message suspicious.

<img width="892" height="507" alt="Screenshot 2026-09-24 042333" src="https://github.com/user-attachments/assets/4ebbbbd5-1446-4851-bde1-6835db6c236d" />

## Investigation

### 1. Reviewing the Raw Email Header

I started by reviewing the raw email header instead of relying only on the displayed sender name.

The following details were identified:

- **Subject:** Your account has been flagged for unusual activity
- **Claimed sender:** Outlook Support Team
- **Actual sender:** `social201511138@social.helwan.edu.eg`
- **Recipient:** `dderringer@mighty-solutions.net`
- **Sender IP:** `40.107.22.60`
- **Date:** Tue, 31 Oct 2023 10:10:04 -0900
- **Content encoding:** Base64

The claimed identity did not match the actual sender address. This mismatch was one of the first indicators that the email required further investigation.

Base64 encoding is not automatically malicious, but attackers may use it to make email content harder to inspect quickly.

<img width="1527" height="517" alt="Screenshot 2026-09-24 042404" src="https://github.com/user-attachments/assets/523310d2-d77a-470c-b4f2-e9375fe28acc" />

### 2. Checking the Embedded Link

The suspicious URL found in the email was submitted to VirusTotal to check its reputation across multiple security engines.

One of the embedded URLs was classified as **Phishing** by Fortinet. This result strengthened the evidence that the message was attempting to direct the recipient to a malicious or deceptive website.

<img width="1260" height="575" alt="Screenshot 2026-09-24 042509" src="https://github.com/user-attachments/assets/189bc8eb-c4a4-436d-ac96-d2b1cf7c7d81" />

### 3. Reviewing the SPF Result

The email showed an `SPF: Pass` result.

<img width="1328" height="247" alt="Screenshot 2026-09-24 042523" src="https://github.com/user-attachments/assets/12cf8304-bc16-44a6-8fba-5ff1751435ea" />

An SPF pass only confirms that the sending server was authorized to send email for the domain used during the SMTP transaction. It does not prove that the message itself is safe or that the displayed sender identity is legitimate.

This is why email authentication results should always be reviewed together with the sender address, message content, URLs, and other available evidence.

### 4. Investigating the Sender IP

The sender IP address was reviewed using reverse DNS and WHOIS information.

- **IP address:** `40.107.22.60`
- **Reverse DNS:** `mail-am6eur05on2060.outbound.protection.outlook.com`
- **Infrastructure owner:** Microsoft

<img width="1172" height="546" alt="Screenshot 2026-09-24 042627" src="https://github.com/user-attachments/assets/0a8cd70f-0d61-4327-b46d-1fb6af94b42f" />

The IP was associated with Microsoft email infrastructure. However, legitimate cloud infrastructure can still be used by compromised accounts or abused services. Therefore, the IP ownership alone was not enough to classify the email as safe.

## Key Findings

- The email claimed to be from the Outlook Support Team.
- The actual sender address belonged to an unrelated domain.
- The message used an urgent account-related warning.
- The employee’s account was still accessible despite the message claiming it had been disabled.
- The email body used Base64 encoding.
- An embedded URL was classified as phishing by a security vendor.
- The SPF result passed, but it did not confirm that the email content was legitimate.
- The sender IP belonged to Microsoft infrastructure, but this did not remove the other suspicious indicators.

## MITRE ATT&CK Mapping

- **T1566.002 – Phishing: Spearphishing Link**

The email attempted to convince the recipient to interact with a suspicious link by using an urgent account warning.

## Final Verdict

**Phishing**

The conclusion was based on the correlation of multiple indicators rather than a single result. The sender mismatch, misleading account warning, suspicious embedded link, and URL reputation provided enough evidence to classify the email as phishing.

## Recommended Response

- Do not click any links in the email.
- Report the message to the security team.
- Block the confirmed malicious URL.
- Search email logs for other recipients of the same message.
- Review whether any users clicked the link.
- Reset credentials if interaction with the phishing page is confirmed.
- Monitor affected accounts for unusual sign-in activity.

## Lesson Learned

A passing SPF result or a sender IP belonging to a trusted provider does not automatically make an email legitimate. Phishing analysis requires correlation between the raw header, sender identity, authentication results, URLs, message content, and threat intelligence findings.


