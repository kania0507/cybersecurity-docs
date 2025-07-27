---
description: https://tryhackme.com/room/introtosiem
---

# TryHackMe Walkthrough: Intro to SIEM

SIEM stands for **Security Information and Event Management system**. It is a tool that collects data from various endpoints/network devices across the network, stores them at a centralized place, and performs correlation on them. This room will cover the basic concepts required to understand SIEM and how it works.

**Question 1**: What does SIEM stand for?

**Answer**: Security Information and Event Management system.

## Task 2 — Network Visibility through SIEM <a href="#id-2c30" id="id-2c30"></a>

Network log sources can be divdied into two logical parts:

**Host-Centric Log Sources**

> These are log sources that capture events that occurred within or related to the host. Some log sources that generate host-centric logs are Windows Event logs, Sysmon, Osquery, etc. Some examples of host-centric logs are:
>
> A user accessing a file
>
> A user attempting to authenticate.
>
> A process Execution Activity
>
> A process adding/editing/deleting a registry key or value.
>
> Powershell execution

and

**Network Centric Log Sources**

> Network-related logs are generated when the hosts communicate with each other or access the internet to visit a website. Some network-based protocols are SSH, VPN, HTTP/s, FTP, etc. Examples of such events are:
>
> SSH connection
>
> A file being accessed via FTP
>
> Web traffic
>
> A user accessing company’s resources through VPN.
>
> Network file sharing Activity

**Key Features of SIEM:**

> Real-time log Ingestion
>
> Alerting against abnormal activities
>
> 24/7 Monitoring and visibility
>
> Protection against the latest threats through early detection
>
> Data Insights and visualization
>
> Ability to investigate past incidents.

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

**Question 1:** Is Registry-related activity host-centric or network-centric?

**Answer:** host-centric

**Question 2:** Is VPN related activity host-centric or network-centric?

**Answer:** network-centric

## Task 3 — Log Sources and Log Ingestion <a href="#c381" id="c381"></a>

> Every device in the network generates some kind of log whenever an activity is performed on it, like a user visiting a website, connecting to SSH, logging into his workstation, etc.

**Log Ingestion Methods**

> **1) Agent / Forwarder:** These SIEM solutions provide a lightweight tool called an agent (forwarder by Splunk) that gets installed in the Endpoint. It is configured to capture all the important logs and send them to the SIEM server.
>
> **2) Syslog:** Syslog is a widely used protocol to collect data from various systems like web servers, databases, etc., are sent real-time data to the centralized destination.
>
> **3) Manual Upload:** Some SIEM solutions, like Splunk, ELK, etc., allow users to ingest offline data for quick analysis. Once the data is ingested, it is normalized and made available for analysis.
>
> **4) Port-Forwarding:** SIEM solutions can also be configured to listen on a certain port, and then the endpoints forward the data to the SIEM instance on the listening port.

**Question 1**: In which location within a Linux environment are HTTP logs stored?

**Answer**: /var/log/httpd

## Task 4 — Why SIEM <a href="#id-9e2d" id="id-9e2d"></a>

> SIEM is used to provide correlation on the collected data to detect threats. Once a threat is detected, or a certain threshold is crossed, an alert is raised. This alert enables the analysts to take suitable actions based on the investigation. SIEM plays an important role in the Cyber Security domain and helps detect and protect against the latest threats in a timely manner. It provides good visibility of what’s happening within the network infrastructure.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

### **SOC Analyst Responsibilities** <a href="#id-75da" id="id-75da"></a>

> SOC Analysts utilize SIEM solutions in order to have better visibility of what is happening within the network. Some of their responsibilities include:
>
> Monitoring and Investigating.
>
> Identifying False positives.
>
> Tuning Rules which are causing the noise or False positives.
>
> Reporting and Compliance.
>
> Identifying blind spots in the network visibility and covering them.

**Question 1**: Read the task above.

**Answer**: No answer needed.

## Task 5 — Analysing Logs and Alerts <a href="#id-5798" id="id-5798"></a>

### **Dashboards** <a href="#id-6e6a" id="id-6e6a"></a>

> Dashboards are the most important components of any SIEM. SIEM presents the data for analysis after being normalized and ingested. The summary of these analyses is presented in the form of actionable insights with the help of multiple dashboards. Each SIEM solution comes with some default dashboards and provides an option for custom Dashboard creation. Some of the information that can be found in a dashboard are:

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>



### Correlation Rules <a href="#id-8bf5" id="id-8bf5"></a>

> Correlation rules play an important role in the timely detection of threats allowing analysts to take action on time. Correlation rules are pretty much logical expressions set to be triggered.

Some examples include:

> If a User gets 5 failed Login Attempts in 10 seconds — Raise an alert for `Multiple Failed Login Attempts`
>
> If login is successful after multiple failed login attempts — Raise an alert for `Successful Login After multiple Login Attempts`
>
> A rule is set to alert every time a user plugs in a USB (Useful if USB is restricted as per the company policy)
>
> If outbound traffic is > 25 MB — Raise an alert to potential Data exfiltration Attempt (Usually, it depends on the company policy)

### Alert Investigation <a href="#id-3874" id="id-3874"></a>

> When monitoring SIEM, analysts spend most of their time on dashboards as it displays various key details about the network in a very summarized way. Once an alert is triggered, the events/flows associated with the alert are examined, and the rule is checked to see which conditions are met. Based on the investigation, the analyst determines if it’s a True or False positive. Some of the actions that are performed after the analysis are:
>
> Alert is False Alarm. It may require tuning the rule to avoid similar False positives from occurring again.
>
> Alert is True Positive. Perform further investigation.
>
> Contact the asset owner to inquire about the activity.
>
> Suspicious activity is confirmed. Isolate the infected host.
>
> Block the suspicious IP.

**Question 1:** Which Event ID is generated when event logs are removed?

**Answer:** 104

**Question 2:** What type of alert may require tuning?

**Answer:** False alarm

## Task 6 — Lab Work <a href="#id-4184" id="id-4184"></a>

**Question 1:** Click on Start Suspicious Activity, which process caused the alert?

**Answer:** cudominer.exe

**Question 2:** Which Event ID is generated when event logs are removed?

**Answer:** chris.fort

**Question 3:** What is the hostname of the suspect user?

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

**Answer:** HR\_02

**Question 4:** Examine the rule and the suspicious process; which term matched the rule that caused the alert?



<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

**Answer:** miner (the process is called cudoMINER)

**Question 5**: What is the best option that represents the event? Chose either False-Positive or True-Positive.

**Answer**: **True-Positive**

**Question** **6**: Selection the right ACTION will display the FLAG. What is the FLAG?

**Answer: THM{000\_SIEM\_INTRO}**

## Task 7 — Conclusion <a href="#id-578f" id="id-578f"></a>

**Question 1**: Complete this room

**Answer**: No answer needed.
