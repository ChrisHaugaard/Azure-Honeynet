# Azure-Honeypot
<h2>Introduction</h2>
<br>In this lab, I built a honeynet in Azure. All the logs will be sent to log analytics workspace where they will be utilized by Microsoft Sentinel. This will allow me to see all the different types of logs ingested to build the attack maps, create alerts, and manage incidents. </br>
The recording of this lab will be over two 48 hour periods where I will record an insecure environment apply security controls and then record the next 48 hours.
<br>In this lab I will be utilizing: </br> 

- Windows VM- Running Mysql server
- Linux VM
- Azure Key Vault
- Azure Storace Account
- Azure Active Directory
- Log Analytics Workspace
- Microsoft Sentinel
- Network Security Gateway
- KQL

<h1>Unsecure Environment</h1>
<h2>Maps Unsecured</h2>
<br><img width="926" alt="Windows-rdp" src="https://github.com/ChrisHaugaard/Azure-Honeypot/assets/140214520/8f280738-69e0-4c92-9523-f257660e6e7c"></br>
<br><img width="883" alt="linux-auth-fail" src="https://github.com/ChrisHaugaard/Azure-Honeypot/assets/140214520/8e65aa63-bcf6-4965-9260-21f934bf7953"></br>
<br><img width="817" alt="mssql-auth" src="https://github.com/ChrisHaugaard/Azure-Honeypot/assets/140214520/e5360a2b-e6a8-400f-967b-4281a82f9017"></br>
<br><img width="820" alt="nsg-allowed" src="https://github.com/ChrisHaugaard/Azure-Honeypot/assets/140214520/588b4829-ed22-462d-8e59-c7c62a3743bd"></br>

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

<h2>Architecture Unsecured</h2>

![UNSECURE_Azure](https://github.com/ChrisHaugaard/Azure-Honeypot/assets/140214520/62dfa11f-d0c5-4aeb-826d-325276659d4a)

<h1>Secured Environment</h1>
<h2>Architecture After Securing</h2>

![AzureHoneypot_Secured](https://github.com/ChrisHaugaard/Azure-Honeypot/assets/140214520/ee13270f-78c9-43be-abb3-27234d43efa0)

<h2>Maps After Securing</h2>
There are no maps to provide as after securing there was nothing recorded

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
<br></br>
<br></br>


