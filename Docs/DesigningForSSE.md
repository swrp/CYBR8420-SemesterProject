## Designing for Software Security Engineering
#### Data Flow: User Uploads Data
Level 0 DFD

![Level 0 for User Uploads Data](https://github.com/swrp/CYBR8420-SemesterProject/blob/BhawiniTripathi-TMT/Level0_DataFlow1.PNG)

#### Data Flow: System Uploads Data
Level 0 DFD

![Level 0 for System Uploads Data](https://github.com/swrp/CYBR8420-SemesterProject/blob/BhawiniTripathi-TMT/Level0_DataFlow2.PNG)

#### Data Flow: Internal Cluster Communication
Level 0 DFD  
![Level 0 for Internal Cluster Communication](https://github.com/swrp/CYBR8420-SemesterProject/blob/mark/Threat%20Models/InternalClusterCommunication_Level_0.PNG)  

Threat Model/Level 1 DFD  
A full threat model and Level 1 data flow diagram has been completed <a href = "https://swrp.github.io/CYBR8420-SemesterProject/InternalClusterCommunication_ThreatReport.htm">here </a>

Threat Model Analysis  
As indicated in several sections of the threat model, Elasticsearch has a fairly robust security solution provided by the X-Pack features.  When doing the analysis, these security features directly addressed the STRIDE threats in many cases.  When thinking specifically about the Internal Cluster Communication data flow, the security features included seem to be all encompassing from the documentation available.

Elasticsearch has methods to authenticate all cluster nodes, making spoofing very difficult unless a member of the cluster is compromised.  Some security features, like strong encryption of all traffic, certainly minimize Information Disclosure threats, but also could reduce tampering,  Whitelisting and dedicated networks specifically for cluster communication drastically reduce the risk of denial of service attacks. 

Audit log generation options are available to ensure integrity of the log files and repudiation threats.  There is event an event type in the Elasticsearch system called "tampered_request" that specifically is logged if a tampered search request is discovered.  Role based access control and the default behavior of not running the software as root, but rather with standard user access reduces the risk of elevation of privilege.

The threat model and analysis did not reveal any significant design issues.

#### Data Flow:


#### Data Flow:
**Use Case: Analyst queries for data from cluster**

Level 0 DFD

![Level 0 Analyst Querying for Data](https://github.com/swrp/CYBR8420-SemesterProject/blob/swrp-TMT/Threat%20Models/AnalystQueriesForFraudReports.png)

<a href = "https://swrp.github.io/CYBR8420-SemesterProject/AnalystQueriesForFraudReprts.htm"> Click here for a complete Level-1 threat report</a>

**Observations**
The threat report generated 14 threats of which 

#### Data Flow:

#### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects/5
