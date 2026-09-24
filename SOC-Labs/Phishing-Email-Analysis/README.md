```markdown
# Phishing Email Analysis

## Overview

This lab documents the analysis of a suspicious email using its raw headers, sender information, authentication results, embedded links, and external reputation checks.

The purpose was to determine whether the message was legitimate or part of a phishing attempt.

## Scenario

An employee received an email claiming that their account had been disabled because of unusual activity. However, the employee was still able to access the account normally, which made the message suspicious.

![Suspicious email scenario](01-phishing-email.png)

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

The claimed identity did not match the actual sender address. This mismatch was one of the first indicators that the email require
```
