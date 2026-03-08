# Defensive Security Intro – TryHackMe

## Objective

This lab introduces the principles of defensive security and the role of a Security Operations Center (SOC) in detecting, investigating, and responding to cyber attacks.

The objective is to monitor the FakeBank environment, identify suspicious activity, analyze attacker behavior, and apply mitigation measures to stop the attack.

---

# Task 1 – Think Like a Defender

## Key Concepts

Defensive security focuses on protecting systems, networks, and digital assets from cyber threats. Its primary objective is to detect, investigate, and respond to malicious activities before significant damage occurs.

Unlike offensive security, which attempts to discover vulnerabilities by simulating attacks, defensive security concentrates on monitoring systems, identifying suspicious behavior, and mitigating potential threats.

## Blue Team Perspective

From a Blue Team perspective, the defender’s role is to continuously monitor systems for signs of compromise. This involves analyzing alerts, logs, and abnormal system activity to quickly identify potential attacks.

Early detection and rapid response are critical in minimizing the impact of security incidents and maintaining the integrity, confidentiality, and availability of systems.

---

# Task 2 – Detect Suspicious Activity

## Environment

The investigation was conducted using the **Security Analyst Dashboard** within a virtual lab environment simulating the FakeBank infrastructure.

## Alert Detection

During the monitoring process, the Intrusion Detection System (IDS) generated multiple alerts indicating suspicious activity originating from an external source.

The monitoring dashboard identified a **Web Discovery Attack**, specifically an automated directory enumeration attempt targeting the FakeBank website.

### Alert Details

Attack Type: Web Discovery / Directory Enumeration  
Source IP Address: 32.122.195.63  
Target: FakeBank web application (admin endpoints)  
Detection Tool: Security Analyst Dashboard (IDS monitoring system)  
Alert Severity: High  

The alert indicated that the external IP address attempted to discover hidden directories within the website infrastructure. Directory enumeration is commonly used by attackers to identify sensitive endpoints such as administrative panels or hidden application resources.

The alert was assigned to **SOC Operator John Smith** for further investigation.

Screenshot of evidence:

<img width="1364" height="716" alt="detection-alerts-IDS png" src="https://github.com/user-attachments/assets/c60724d7-1daa-41b6-96b6-8f57317cc301" />

---

## Database Access Attempt

The monitoring system also detected unusual database query behavior associated with the same external IP address.

The system flagged an **Unusual Database Query Pattern**, suggesting a potential attempt to access the **customer database**, which stores sensitive user information.

This alert was assigned to **SOC Operator Sarah Johnson** for investigation.

### Potential Risks

- Unauthorized access to customer data  
- Data exfiltration  
- Manipulation or deletion of sensitive records  

Screenshot of evidence:



---

## SQL Injection Attempt

Further analysis revealed that the attacker attempted to exploit the web application using an **automated SQL Injection attack**.

SQL Injection attacks involve sending malicious database queries through application input fields, such as login forms or payment forms, with the goal of manipulating the underlying database.

In this scenario, the attacker targeted the **payment form**, attempting to inject malicious code in order to:

- Access sensitive database information  
- Extract user credentials  
- Modify stored data  
- Delete records  
- Manipulate financial transactions  

Due to the high risk associated with payment systems and sensitive financial data, this type of attack is considered **critical priority** and requires immediate investigation and containment by the technical security team.

Screenshot of evidence:

<img width="1365" height="716" alt="SQL-injection-attempt" src="https://github.com/user-attachments/assets/c3c3b788-ae55-408b-b09d-bba4e9e8ac33" />

---

## Event Tracking Analysis

The event tracking dashboard showed the following activity trends:

### Around 12:00

12 incidents detected  
18 alerts under investigation  
10 alerts resolved  

### Around 21:00

3 active incidents  
7 alerts under investigation  
22 alerts resolved  

This reduction in suspicious activity suggests that mitigation actions or investigation processes may have successfully reduced the attack activity.

Screenshot of evidence:

<img width="554" height="277" alt="Analysis-event-tracking24H" src="https://github.com/user-attachments/assets/1392ab16-832e-4ba5-bf57-b6f53196e6f7" />

---

# Task 3 – Identify the Attack

## Incident Overview

During the investigation process, the Intrusion Detection System (IDS) identified a security event classified under the **Event ID: SEC-000001**.

The alert indicated a **Web Discovery Attack**, suggesting that an external attacker was attempting to enumerate web directories in order to locate sensitive endpoints within the FakeBank web application.

The activity was detected within a short time window of approximately **2 minutes from the first alert generated by the monitoring system**.

---

## Attack Summary and Timeline

Initial Detection: 14/07/2025 – 10:21:39  
Total Duration of Suspicious Activity: 16 minutes and 32 seconds  
Total URL Access Attempts: 32  
Blocked Requests: 10  

Further analysis revealed that the attacker attempted to access the administrative endpoint:

GET Request – Response Code: **404**  
URL Targeted: `https://fakebank.com/admin`  
Time Observed: **10:39:07**

Although the response returned a 404 status code (page not found), the attempt indicates that the attacker was actively searching for administrative interfaces.

Screenshot of evidence:

<img width="570" height="510" alt="Attack-summary png" src="https://github.com/user-attachments/assets/fadb975e-59c3-446c-97a7-410ade60ec86" />

---

## Threat Intelligence Analysis

Threat intelligence data associated with the source IP address revealed the following information:

Source IP: 32.122.195.63  
Geolocation: Moscow, Russia  
ASN: AS12345  
Previous Malicious Activity: 47 recorded incidents  

This intelligence suggests that the IP address has been previously linked to malicious activities and may be associated with automated attack infrastructure.

Screenshot of evidence:

<img width="577" height="243" alt="Threat-intelligence-analysis png" src="https://github.com/user-attachments/assets/a8c9a9aa-633e-4909-b02c-42b8da6f4858" />

---

## Attack Behaviour Analysis

The attacker appeared to be conducting a **systematic reconnaissance attempt**, and could likely using automated tools to scan multiple web endpoints in search of vulnerable resources.

This behaviour is consistent with the early stages of a web application attack lifecycle:

1. Reconnaissance (directory enumeration)  
2. Discovery of sensitive endpoints  
3. Attempted exploitation of vulnerable services  

The consistent scanning activity suggests the use of automated attack tools rather than manual probing.

---

## Blue Team Perspective

From a defensive security perspective, this type of attack highlights the importance of continuous monitoring and rapid response.

Attackers often attempt multiple techniques in a short period of time in order to identify exploitable weaknesses. Even unsuccessful attempts, such as requests returning 404 responses, can provide valuable intelligence about attacker behaviour.

SOC analysts must therefore remain vigilant when monitoring alerts and treat reconnaissance activity as a potential precursor to more severe attacks.

---

# Task 4 – Stop the Attack

## Incident Response Actions

Following the analysis and identification of the attack, initial containment and mitigation measures were implemented.

---

## IP Address Blocking

The malicious source IP address was blocked:

Blocked IP: **32.122.195.63**  
Block Duration: **24 hours**

This action prevents further traffic from the identified attacker.

However, it is important to note that attackers may attempt to bypass IP blocking by using VPN services, proxy networks, or other infrastructure to change their source IP address.

Screenshot of evidence:

<img width="563" height="505" alt="action-block-source-IPaddress png" src="https://github.com/user-attachments/assets/67fcf87d-cdc1-4074-8e95-d432e6582249" />

---

## Rate Limiting Implementation

Traffic control mechanisms were implemented to limit the number of requests that a single IP address can send to the server.

### Initial Configuration

Time Window: 60 seconds  
Maximum Requests: 50  

This configuration was considered too permissive for sensitive endpoints such as payment or transfer forms.

Screenshot of evidence:

<img width="551" height="273" alt="action-implement-rate-limiting png" src="https://github.com/user-attachments/assets/fc8f0de1-698c-4e7c-b7cd-3f865e979300" />

---

### Updated Configuration

Time Window: 60 seconds  
Maximum Requests: 10  

This adjustment helps mitigate automated attacks such as:

- Brute force attempts  
- SQL Injection automation  
- Carding attacks  
- Bot-based scraping  

---

## Security Incident Record

Event ID: **SEC-000001**  
Priority: **Critical**  
Status: **Under Investigation / Mitigation in Progress**  
Incident Category: **Web Application Attack**

### Incident Overview

Detection Method: IDS / WAF Automated Alert  
Attack Type: Automated SQL Injection  
Target Asset: Payment Processing Endpoint  
Source IP: 32.122.195.63  

The monitoring system detected multiple automated requests containing malicious SQL payloads targeting the payment processing endpoint.

The high frequency of requests indicates a scripted attack attempting to exploit database vulnerabilities within the payment form.

---

## Analyst Recommendations

Recommended security improvements include:

Rate Limiting Adjustment  
Reduce request thresholds on sensitive endpoints.

Input Sanitization  
Implement strict server-side validation and parameterized SQL queries to prevent SQL injection vulnerabilities.

PCI-DSS Compliance  
Ensure sensitive financial data is not logged in plaintext during security events.

Honeypot Implementation  
Deploy hidden fields designed to detect automated bot interactions.

Screenshots of evidence:

<img width="301" height="319" alt="Recommended-actions-alerts-of-IDS" src="https://github.com/user-attachments/assets/b9bc549f-eb7d-4b59-ab60-4d6570584a63" />

<img width="528" height="221" alt="Additional-notes-actions-recomendentions-png" src="https://github.com/user-attachments/assets/d3f732f1-ec01-4f0b-b4d7-c94ca7188060" />

---

## Next Steps

Verify whether the WAF successfully blocked all malicious requests.

Conduct a detailed log review to confirm that no unauthorized data access occurred before mitigation actions were applied.

Ensure the malicious IP address remains blocked at the firewall level.

Coordinate with the backend development team to confirm secure database query implementation using parameterized queries.

Screenshot of evidence:

<img width="1365" height="720" alt="action-bloked-IPaddress-sucess png" src="https://github.com/user-attachments/assets/ee33f516-c789-444f-a5a0-03db83a5317d" />

---

# About the report - My SOC analysis insights perspectives through evidences screenchosts

The analysis documented in this report is supported by visual evidence collected during the investigation process.

Screenshots from the security monitoring dashboard and IDS alert panels were captured to document:

- Detected alerts  
- Attack source information  
- Event tracking statistics  
- Monitoring dashboard activity  
- Security mitigation actions  

These screenshots are included in this repository as supporting evidence for the incident investigation.

---

# Conclusion

This lab demonstrated the full defensive security workflow:

Detection → Investigation → Identification → Response.

Through monitoring IDS alerts, analyzing attacker behavior, and implementing mitigation strategies, it was possible to contain the simulated attack against the FakeBank web application.

This exercise highlights the importance of continuous monitoring, rapid incident response, and proactive security measures in protecting web applications from automated cyber attacks.
