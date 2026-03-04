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
- Identified account number: **8881**

### Directory Enumeration
- Used `dirb` to discover hidden directories.

### Findings
- `/bank-transfer` → HTTP 200 (accessible sensitive function)
- `/images` → HTTP 301 (redirected resource)

### Observations
- Hidden endpoints may expose critical functionalities.
- Directory enumeration is a common reconnaissance technique used by attackers.

### Evidence
- Screenshot of enumeration results

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

### Blue Team Insight
- Critical assets must be protected with layered security controls.
- Continuous monitoring is essential to detect unauthorized access attempts.

----

## Final Thoughts

This lab demonstrated how attackers move from reconnaissance to exploitation.  
From a Blue Team perspective, understanding this process is essential to detect, prevent, and respond to real-world threats.
