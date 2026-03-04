# Offensive Security Intro – TryHackMe

## Objective
Understand how attackers identify and exploit vulnerabilities in web applications, and how these actions can be detected and mitigated from a Blue Team perspective.

---

## Task 1 – Thinking Like an Attacker

### Key Concepts
- Attackers search for weaknesses in systems to gain unauthorized access.
- Ethical hackers simulate attacks in controlled environments to identify vulnerabilities.

### Blue Team Insight
- Understanding attacker behavior is essential to proactively defend systems.
- Defensive teams must anticipate attack patterns and implement monitoring strategies.

---

## Task 2 – Starting the Lab (Fakebank)

### Actions Performed
- Accessed the Fakebank application via the virtual desktop.
- Identified account number: **8881** displayed on the login page.
- Noted that sensitive information is exposed directly on the page.

### Observations
- Exposed account numbers represent a serious vulnerability.
- This highlights the importance of securing sensitive fields in web applications.

### Evidence

**Fakebank account identification (account 8881):**
![Fakebank Account](fakebank-account.png)

### Blue Team Insight
- Sensitive data exposure should trigger immediate review and patching.
- Web applications must validate and limit what information is displayed to unauthorized users.

---

## Task 3 – Find Hidden Pages

### Actions Performed
- Performed directory enumeration using `dirb` to discover hidden endpoints.
- Objective: identify potential vulnerabilities and exposed sensitive resources.

### Findings
- `/bank-transfer` → HTTP 200 (accessible sensitive function)
- `/images` → HTTP 301 (redirected resource)

### Observations
- Hidden endpoints may expose critical functionalities to attackers.
- Directory enumeration is a common reconnaissance technique used by attackers.

### Evidence

**Directory Enumeration using dirb:**
![Dirb Scan](dirb-scan.png)

### Blue Team Insight
- Monitor unusual request patterns (e.g., directory brute-forcing).
- Implement logging and access controls on sensitive endpoints.

---

## Task 4 – Attacking the Admin Page

### Actions Performed
- Accessed the Admin Page of the Fakebank application.
- Observed sensitive information, including bank accounts.
- Successfully performed a transaction (deposit) to account **8881**.

### Findings
- Admin panel accessible without proper authentication controls.
- Critical functionality exposed to unauthorized users.

### Impact
- Unauthorized access to sensitive financial data
- Potential financial fraud
- Full compromise of application integrity

### Risk Level
- **High / Critical**

### Blue Team Analysis
- This vulnerability represents a critical security failure.
- Should be prioritized for immediate triage and escalation.

### Recommended Mitigations
- Implement strong authentication (username + password)
- Enforce Multi-Factor Authentication (MFA/2FA)
- Restrict access to admin endpoints
- Monitor and log all admin activity
- Apply least privilege principle

### Evidence

**General view of Admin Page:**
![Admin Page](admin-page.png)

**Admin panel access and unauthorized transaction to account 8881:**
![Admin Panel Unauthorized Transfer](admin-panel-unauthorized-transfer.png)

### Blue Team Insight
- Critical assets must be protected with layered security controls.
- Continuous monitoring is essential to detect unauthorized access attempts.

---

## Final Thoughts

This lab demonstrated how attackers move from reconnaissance to exploitation.  
From a Blue Team perspective, understanding this process is essential to detect, prevent, and respond to real-world threats.
