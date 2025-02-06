#  IBM Hybrid Cloud Security Dashboard

## **📌 Overview**
This project develops a **Splunk-based security monitoring dashboard** that:
- **Ingests AWS CloudTrail logs** to track authentication events and API calls.
- **Monitors IAM role changes and privilege escalations.**
- **Detects publicly exposed S3 buckets for misconfigurations.**
- **Integrates IBM X-Force API** to identify known threat actors.
- **Provides real-time alerts and visualizations for security incidents.**

This project aligns with **IBM's Cyber Security Consultant** role, which requires expertise in **SIEM tools (Splunk), hybrid cloud security, compliance, and threat intelligence integration.**

# 📌 Lessons Learned
Throughout this project, key technical and security insights were gained, reinforcing IBM-relevant cybersecurity expertise.

## 1️⃣ Cloud Security & Compliance

✅ Understanding AWS Security Logs – Learned how to enable and analyze AWS CloudTrail logs for tracking user activity.

✅ IAM Security Best Practices – Identified privilege escalations and misconfigured IAM roles to enhance access control.

✅ S3 Bucket Security – Recognized risks of publicly exposed storage and how to mitigate misconfigurations.

## 2️⃣ SIEM & Threat Intelligence Integration
✅ Splunk Log Ingestion & Analysis – Learned how to process large-scale security logs from AWS into Splunk for real-time monitoring.

✅ Creating Custom Security Dashboards – Built Splunk dashboards to visualize security incidents and quickly detect threats.

✅ IBM X-Force Threat Intelligence – Integrated IBM’s own X-Force API to detect known cyber threats and malicious actors in security logs.

## 3️⃣ Incident Detection & Response
✅ Automated Alerts for Security Breaches – Designed real-time security alerts to detect failed logins, IAM changes, and cloud misconfigurations.

✅ Simulating Cybersecurity Attacks – Practiced real-world security incident simulations, including brute-force attacks, unauthorized IAM changes, and compliance failures.

✅ Response & Mitigation Strategies – Developed an actionable approach to responding to security threats, aligning with SOC (Security Operations Center) workflows.

# 📌 Benefits of This Project
This project brings substantial benefits both to cybersecurity professionals and to IBM as an industry leader in cybersecurity solutions.

## 1️⃣ Professional Growth & Industry Relevance

✔ Real-World Experience – This project mirrors enterprise security monitoring scenarios, making it directly applicable to cybersecurity careers.

✔ Hands-On SIEM & Cloud Security Skills – Security professionals must understand cloud security in AWS and manage security events with SIEM tools like Splunk.

✔ Compliance & Risk Management Knowledge – Many organizations face regulatory requirements (SOC 2, NIST, ISO 27001)—this project aligns with best security practices.

## 2️⃣ Enterprise-Level Security Implementation
✔ IBM’s Cybersecurity Focus – IBM develops security solutions for hybrid cloud environments, and this project aligns directly with their cloud security initiatives.

✔ Threat Intelligence & AI Security – IBM integrates AI into cybersecurity (IBM Watson, QRadar, X-Force). This project demonstrates understanding of threat detection & mitigation.

✔ Cost-Efficient Security Solutions – Implementing early threat detection reduces cybersecurity breaches, saving organizations millions in incident response costs.

## 3️⃣ Aligning with IBM's Core Security Solutions

✔ Hybrid Cloud Security (AWS, Azure, IBM Cloud) – IBM focuses on hybrid cloud security solutions, and this project provides a framework for monitoring hybrid cloud threats.

✔ SIEM Integration (Splunk, IBM QRadar) – IBM provides QRadar, a leading SIEM tool. By integrating Splunk, this project demonstrates SIEM knowledge transferable to IBM QRadar.

✔ Zero Trust Security Model – IBM emphasizes Zero Trust principles, ensuring continuous security monitoring—this project aligns with IBM’s security best practices.

# 📌 How This Positively Impacts IBM
By implementing this security monitoring system, IBM gains several business and operational advantages:

## 1️⃣ Strengthening IBM’s Cloud Security Solutions

💡 Enhanced Cybersecurity Expertise – This project proves that IBM can develop next-gen cloud security solutions for AWS, Azure, and IBM Cloud.

💡 Improved Security Analytics – Using Splunk & IBM X-Force, this project strengthens IBM’s AI-driven cybersecurity analytics offerings.

💡 Proactive Threat Hunting Capabilities – With real-time threat detection, IBM can offer businesses a proactive defense mechanism against cyber threats.

## 2️⃣ Increasing IBM’s Competitive Edge

💡 Demonstrating IBM’s Leadership in Security – This project showcases IBM’s ability to lead in hybrid cloud security monitoring.

💡 Expanding IBM’s Threat Intelligence Portfolio – By integrating IBM X-Force, IBM can expand its security threat intelligence offerings to enterprise clients.

💡 Enhancing IBM’s SIEM & SOC Solutions – This project’s use of Splunk (which is similar to IBM QRadar) provides a template for enhancing IBM’s security monitoring capabilities.

## 3️⃣ Reducing Security Incidents for IBM & Its Clients

💡 Faster Threat Detection for IBM Clients – This project’s security alerts help organizations reduce cyberattack response time, saving millions in incident mitigation costs.

💡 Compliance Assurance for IBM Services – Companies working with IBM must meet compliance standards (SOC 2, NIST, ISO 27001)—this project ensures clients meet these standards.

💡 Cyber Risk Reduction – IBM customers will benefit from automated cloud security monitoring, preventing costly data breaches and compliance violations.

+--------------------------------------+
|         AWS CloudTrail               |
|   (Security Logs from AWS)           |
+--------------------------------------+
             │  
             ▼  
+--------------------------------------+
|         Splunk SIEM                   |
|  (Ingesting & Analyzing AWS Logs)     |
+--------------------------------------+
             │  
             ▼  
+--------------------------------------+
|      Security Dashboard (Splunk)      |
|  - Failed Logins                      |
|  - IAM Role Changes                   |
|  - Public S3 Buckets                  |
+--------------------------------------+
             │  
             ▼  
+--------------------------------------+
|     IBM X-Force Threat Intelligence   |
|  - Checks for Malicious IPs           |
|  - Generates Risk Scores              |
+--------------------------------------+

---
# 📌 Phase 1: AWS Setup
## 1️⃣ Enable AWS CloudTrail

Run the command to enable CloudTrail logging **(BASH)**: 

aws cloudtrail create-trail --name SecurityTrail --s3-bucket-name my-cloudtrail-logs

## 2️⃣ Verify Logs Are Being Stored

Run the command to check if logs are being saved **(BASH)**:

aws s3 ls s3://my-cloudtrail-logs/

# 📌 Phase 2: Install Splunk & Ingest Logs
## 1️⃣ Install Splunk & Enable HTTP Event Collector (HEC)

Start Splunk **(BASH)**:

splunk start

Open Splunk Web Interface:

http://localhost:8000

Enable HEC Token in Splunk: Settings → Data Inputs → HTTP Event Collector → New Token

## 2️⃣ Send AWS CloudTrail Logs to Splunk

Configure Splunk to monitor CloudTrail logs **(BASH)**:

splunk add monitor /data/aws_logs/ -index aws_security -sourcetype aws:cloudtrail

# 📌 Phase 3: Create Security Dashboard & Alerts
## 1️⃣ Create a New Splunk Dashboard

Run the Splunk query to display indexed AWS security logs **(SPLUNK)**:

index=aws_security | stats count by source

## 2️⃣ Key Security Alerts

## 🚨 Failed Login Attempts 
**(SPLUNK)**
index=aws_security eventName=ConsoleLogin errorCode=Failure
| stats count by userIdentity.arn, sourceIPAddress

## 🛑 Suspicious IAM Role Changes 
**(SPLUNK)**
index=aws_security eventType=AttachRolePolicy policy=AdministratorAccess
| stats count by userIdentity.name

## ⚠️ Publicly Exposed S3 Buckets 
**(SPLUNK)**
index=aws_security eventName=PutBucketAcl
| search requestParameters.x_amz_acl=public-read

# 📌 Phase 4: Integrate IBM X-Force Threat Intelligence
## 1️⃣ Get an IBM X-Force API Key

Sign up for an API key: 👉 IBM X-Force Exchange
## 2️⃣ Python Script to Check Malicious IPs

Use the following Python script to check if an IP is blacklisted **(PYTHON)**:

import requests

API_KEY = "your_ibm_xforce_api_key"
IP = "8.8.8.8"

response = requests.get(f"https://api.xforce.ibmcloud.com/api/ipr/{IP}",
                        headers={"Accept": "application/json", "Authorization": f"Bearer {API_KEY}"})
print(response.json())

## 3️⃣ Cross-Check AWS Traffic with IBM Threat Data

Run the Splunk query to flag AWS traffic from malicious IPs **(SPLUNK)**:

index=aws_security src_ip=*
| lookup threat_feed.csv ip AS src_ip OUTPUT risk_score
| where risk_score > 80

# 📌 Phase 5: Testing & Deployment
## 1️⃣ Test AWS Log Ingestion

Run this command to confirm AWS security logs are being ingested **(SPLUNK)**:

index=aws_security | stats count by index

## 2️⃣ Simulate a Security Event

To test alerts, simulate an IAM privilege escalation **(BASH)**:

aws iam create-user --user-name TestUser
aws iam attach-user-policy --user-name TestUser --policy-arn arn:aws:iam::aws:policy/AdministratorAccess



# 📌 Conclusion
This project directly aligns with IBM’s cybersecurity consulting goals, helping IBM: 

✔ Improve hybrid cloud security (AWS, Azure, IBM Cloud)

✔ Enhance SIEM & threat detection using Splunk & IBM X-Force

✔ Strengthen compliance monitoring for enterprise clients

✔ Reduce cyber risks, security incidents, and compliance costs

🚀 With this project, IBM can continue to lead in cybersecurity, providing enterprises with cutting-edge cloud security solutions! 🔥



