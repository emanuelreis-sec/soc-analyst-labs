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

<img width="1362" height="767" alt="fakebank-accounts-sensitive-information png" src="https://github.com/user-attachments/assets/3b1135bb-2799-4ef0-8188-680902e8e9fe" />


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

<img width="1364" height="766" alt="dirb-scan png" src="https://github.com/user-attachments/assets/52bab304-029e-4b8d-b4a7-c31630e40d7b" />

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

<img width="1365" height="767" alt="admin-page png" src="https://github.com/user-attachments/assets/1558e188-34c9-4b00-8001-acbb6634e2af" />

**Admin panel access and unauthorized transaction to account 8881:**

<img width="1364" height="767" alt="admin-panel-unauthorized-transfer png" src="https://github.com/user-attachments/assets/d57391ea-c973-425f-9c38-328ff08d1f39" />


### Blue Team Insight
- Critical assets must be protected with layered security controls.
- Continuous monitoring is essential to detect unauthorized access attempts.

---

## Final Thoughts

This lab demonstrated how attackers move from reconnaissance to exploitation.  
From a Blue Team perspective, understanding this process is essential to detect, prevent, and respond to real-world threats.
