## Software Security Requirements - Elasticsearch


### Overview
To better define realistic security requirements for Elasticsearch the following environment, data flows, and threat actors were used as the foundation for requirements engineering.  Uses cases and misuse cases were then developed for each data flow to help define security requirements.  Finally, Elasticsearch documentation was reviewed for alignment of the identified security requirements, security configuration, and installation issues.

##### Environment 
* Fraud Monitoring Department at a bank or credit card company using Elasticsearch to store customer information, threat data, and transaction metadata
* The system is critical to the organization's ability to prevent credit card fraud and protect their cardholders

##### Data Flows
The following Elasticsearch data flows were used during the definition of use cases:
1. User updating data into elastic search based on role based access - *Example: Fraud Analyst performs create/read/write/update/delete operations based on the fraudulent transactions from customer phone call and which are then stored in Elasticsearch*
2. System pushes data into cluster - *Example: Credit Card transaction metadata pushed in Elasticsearch from other transaction processing systems*
3. Internal cluster communication - *Example: Elasticsearch nodes copy data between systems for redundancy*
4. Analyst queries for data from cluster - *Example: Data Analyst of the organization pulls reports of fraud activity from elastic cluster*
5. Alert to Fraud Analyst - *Example: Scheduled search in Elasticsearch sends fraud alert to Analyst when suspicious transactions occur*

##### Threat Actor Examples
There are many threat actors that might want to attack an Elasticsearch cluster when it contains customer information or other valuable data.  Threat actors might also want to disrupt the business functions that Elasticsearch provides to the Fraud Monitoring unit.  The following are some examples of threat actors identified for this scenario.
1. Ransomware Authors
2. Identity Thieves
3. Malicious Insider
4. Hacktivist Agents

### Use Cases / Misuse Cases

##### 1. User updating data into elastic search based on role based access
![Privileges for accessing data](https://github.com/swrp/CYBR8420-SemesterProject/blob/maddagadanew/Misuse%20Cases/Misuse%20Case_Controlling%20Data%20Access%20and%20Actions%20on%20data_ORIGINAL.png)

Elasticsearch is used for many purposes, it is used by many organizations to store and retrieve intricate data structures which are serialized as JSON documents. Technically, JSON documents (Data objects) that are stored in the elastic search, every field in the data is indexed by default. The stored documents can be retrieved, accessed and update data from any node in the cluster based on the authorized access of the user. Also, user can perform certain CRUD operations based on role-based access control on the data.

The misuse case mainly focused on performing CRUD operations on the data documents in the Elastic cluster by unauthorized internal Malicious employee. Different operations are performed on the data to manipulate or to steal customer information. Seems like Elastic search has implemented the protection mechanism for the role-based user access. Ways to control what data users can have access to and what tasks they can perform based on the security privileges are clearly documented in the [Elasticsearch privileges page](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/security-privileges.html)

**Security Requirements**:
* Role-based access control should be enabled to prevent users from performing unauthorized CURD actions on the data.
* Enable the IP filtering feature to prevent blacklisted IP’s from joining the cluster or accessing the data documents. For example, the malicious user attempting to join the cluster without permissions.

Elasticsearch seems to have these security features that are packaged in X-Pack module. These features must be enabled by the user based on the organization usage. Role based access controls and security privileges are very clearly documented in their documentation [Role based access controls page](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/authorization.html) and [Cluster Security Privileges page](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/security-privileges.html). 

From my observation, Elasticsearch failed in securing the customer data which is stored in the elastic cluster from the Ransomware attack. [Ransomware Attack on Elastic Cluster](https://www.zdnet.com/article/elasticsearch-ransomware-attacks-now-number-in-the-thousands/). But, they have a feature of IP filtering through which only whitelisted ones only can access and perform certain operations on data documents and entering into main master elastic cluster. The way this feature works is documented in the [Ip filtering page](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/ip-filtering.html).


##### System Uploads Data
Task 2 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### Internal Cluster Communication
Elasticsearch is often deployed as a multi-node cluster in larger environments to provide data redundancy and increased performance.  There are a variety of protocols that make up the data flow between systems to accomplish smooth, scalable operations of the software.  The misuse case for this data flow highlights attacks that might target cluster nodes when a new node joins the cluster or  nodes perform data replication.  

![cluster misuse case diagram](https://github.com/swrp/CYBR8420-SemesterProject/blob/master/Misuse%20Cases/Misuse%20Case_Elasticsearch_Cluster%20Communication%20-%20.jpeg)

Security Requirements
* Authenticate all new nodes that request to join the cluster to verify authorization
* Data being transmitted between nodes should be encrypted to ensure confidentiality
* Cluster communication should have the ability to operate on a separate network interface so that it can be segmented from data collection and user traffic

Elasticsearch does seem to include features in this area, although these security features are in the X-Pack paid modules.  Encrypting cluster communication and authenticating nodes can be done by [configuring TLS and deploying certificates](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/configuring-tls.html#tls-transport) to each node.  Elasticsearch also implements a feature called TCP Transport Profiles that allow cluster traffic between nodes to be[ segmented from other data flows](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/separating-node-client-traffic.html) by designating specific ports or even interfaces for cluster communication.


#####  Analyst queries for data from cluster
In the process of improving the performance outcomes, individual organizations try to examine all the fraud activities by performing a data analysis. The analyst trying to investigate the data needs to query all the transactional information and search for fraud activities to view them on the dashboard and export them to reports. 
![Mis-use case](https://github.com/swrp/CYBR8420-SemesterProject/blob/swrp/Misuse%20Cases/AnalystQueryData.jpeg) 

Security Requirements
* Use Encrypted token patterns
* Account lockout policies after certain failed login attempts
* Grant access to authorized users 

Integrating elastic cluster with ArcSight SIEM helps to get alerts if any attacker tries to brute force through any account. 
This [link](https://www.elastic.co/blog/integrating-elasticsearch-with-arcsight-siem-part-4) describes how to configure accounts to get notified if there are any brute force attempts.  

Attempting to modify the data (using CSRF, XSS, session hijacking)on kibana can be prevented by using encrypted token patterns. Elasticsearch fixed these issues from
[Version 4.2.1](https://www.elastic.co/blog/kibana-4-2-1-and-4-1-3) of kibana.

Configurations can be made to restrict access limited to authorized users using
[X-Pack Security](https://www.elastic.co/guide/en/elastic-stack-overview/current/setting-up-authentication.html). 
##### Alert to Fraud Analyst
In many environments, Elasticsearch might be used to monitor incoming data for specific conditions, and when that condition is met, some type of alert or notification might be raised to a stakeholder.  In the case of a fraud monitoring department, Elasticsearch might be used to run scheduled searches every few minutes looking for outliers in recent credit card transactions.  The misuse case for this data flow shows how attackers might be able to target email alerts and clarifies that other delivery options are needed for important alerts that need analyst attention.

![alerting misuse case diagram](https://github.com/swrp/CYBR8420-SemesterProject/blob/master/Misuse%20Cases/Misuse%20Case_Elasticsearch_Alerting.jpeg)

Security Requirements
* Retain an audit log of all generated alerts
* Allow alerts to be delivered by a protocol other than email, possibly to a ticketing system or customer relationship management system
* Alert emails should be encrypted or at least transported over an encrypted channel

Elasticsearch (with the X-Pack features) does include the ability for [alerting](https://www.elastic.co/guide/en/elastic-stack-overview/current/xpack-alerting.html), and alerts can be sent in [many forms](https://www.elastic.co/guide/en/elastic-stack-overview/current/actions.html).  The ability to send alerts as an email or webhook action would likely allow an IT service management system to issue a service ticket when an alert is generated.  The documentation also indicates that the software does indeed have the ability to use the STARTTLS protocol when [configuring email settings](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/actions-email.html#configuring-email)

### Documentation Review
Task 6

### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects/2
