# Azure-Honeynet
<h2>Introduction</h2>
<br>In this lab, I built a honeynet in Azure. All the logs will be sent to log analytics workspace where they will be utilized by Microsoft Sentinel. This will allow me to see all the different types of logs ingested to build the attack maps, create alerts, and manage incidents. </br>
The recording of this lab will be over two 48 hour periods where I will record an insecure environment apply security controls and then record the next 48 hours.
<br>In this lab I will be utilizing: </br> 

- Windows VM- Running Mssql server
- Linux VM
- Azure Key Vault
- Azure Storace Account
- Azure Active Directory
- Log Analytics Workspace
- Microsoft Sentinel
- Network Security Gateway
- KQL
- NIST 800-53 R5

<h1>Unsecure Environment</h1>
<h2>Metrics Unsecure</h2>
<b>Metrics recieved during the 48 hour unsecured period</b>
<br>Start Time: 2023-09-18 21:16:46</br>
Stop Time: 2023-09-20 21:16:46

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 72819
| Syslog                   | 1835
| SecurityAlert            | 89
| SecurityIncident         | 297
| NSG Inbound Malicious Flows Allowed | 7313

<br>SecurityEvent: Windows event log</br>
<br>Syslong: Linux event log</br>
<br>SecurityAlert: Log Analytics Alert</br>
<br>SecurityIncident: Incident created by Sentinel</br>
<br>*A significant number of the total alerts are brute force attempts against the windows and linux virtual machines</br>

<h1>Secured Environment</h1>

<h2>Metrics After Securing</h2>
<b>Metrics recieved during the 48 hour secured period</b>
<br>Start Time: 2023-09-23 21:46:38</br>
Stop Time: 2023-09-25 21:46:38

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 18956
| Syslog                   | 2
| SecurityAlert            | 0
| SecurityIncident         | 0
| NSG Inbound Malicious Flows Allowed | 0

<br>While I would still consider the alerts coming from SecurityEvent to be significant ranging at about 19,000. Upon closer inspection of the logs they are all from NT AUTHORITY\SYSTEM and WORKGROUP (as seen below) which will be disregarded as those are completley normal and not a cause for concern.</br>
<br>![image](https://github.com/ChrisHaugaard/Azure-Honeypot/assets/140214520/25e123a8-c5a5-48fa-8495-f04f5c59cca6)</br>


<h2>Metric Comparisson</h2>
<b>The percentages are reflecting the decrease in total number of logs created in that category.</b>
<br>Running a comparisson between the two metrics before and after adding security controls the result is fairly noteworthy.</br>
<br>SecurityEvents -73.97%</br>
<br>Syslog -99.89%</br>
<br>SecurityAlert -100%</br>
<br>SecurityIncident -100%</br>
<br>NSG Inbound Malicious Flows Allowed -100%</br>
<br>While SecurityEvents only increased by ~74% the alerts that were created were expected and not something that is required to get rid of. The security posture of the environment increased by about 100% in most categories and including what was seen with Security Event I believe it is ~100% across all metrics.</br>


<h2>Conclusion</h2>
I created an unsecure honeynet in azure recorded the results and incidents using log analytics workspace and microsoft sentinel. I then secured the environment and recorded again for the next two days. The security controls applied to the honeynet were able to successfully create a secure environment. The recording after the security controls were applied showed that by almost 100% across all metrics went down including stopping brute force attempts against the Linux vm, Windows vm, and mysql server.
<br>By using security controls available in Azure and best policies according to Nist 800-53 R5 I was able to secure the honeynet I created in Azure.</br>


