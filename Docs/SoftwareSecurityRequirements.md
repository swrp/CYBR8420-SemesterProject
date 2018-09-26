## Software Security Requirements - Elasticsearch


### Overview
To better define realistic security requirements for Elasticsearch the following environment, data flows, and threat actors were used as the foundation for requirements engineering.  Uses cases and misuse cases were then developed for each data flow to help define security requirements.  Finally, Elasticsearch documentation was reviewed for alignment of the identified security requirements, security configuration, and installation issues.

##### Environment 
* Fraud Monitoring Department at a bank or credit card company using Elasticsearch to store customer information, threat data, and transaction information
* The system is critical to the organization's ability to prevent credit card fraud and protect their cardholders

##### Data Flows
The following Elasticsearch data flows were used during the definition of use cases:
1. User storing data into elastic search - *Example: Fraud Analyst types notes from customer interaction which are then stored in Elasticsearch*
2. System pushes data into cluster - *Example: Credit Card transaction data pushed in Elasticsearch from other systems*
3. Internal cluster communication - *Example: Elasticsearch nodes copy data between systems for redundancy*
4. User queries for data from cluster - *Example: Fraud Analyst views alerts or reports from Elasticsearch*
5. Alert to Fraud Analyst - *Example: Scheduled search in Elasticsearch sends fraud alert to Analyst when suspicious transactions occur*

##### Threat Actor Examples
There are many threat actors that might want to attack an Elasticsearch cluster when it contains customer information or other valuable data.  Threat actors might also want to disrupt the business functions that Elasticsearch provides to the Fraud Monitoring unit.  The following are some examples of threat actors identified for this scenario.
1. Ransomware Authors
2. Identity Thieves
3. Malicious Insider

### Use Cases / Misuse Cases

##### User Stores Data 
Task 1 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### System Uploads Data
Task 2 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### Internal Cluster Communication
Elasticsearch is often deployed as a multi-node cluster in larger environments to provide data redundancy and increased performance.  There are a variety of protocols that make up the data flow between systems to accomplish smooth, scalable operations of the software.  The [misuse case](https://github.com/swrp/CYBR8420-SemesterProject/blob/mabaumgartner/Misuse%20Cases/Misuse%20Case_Elasticsearch_Cluster%20Communication_medium.png) for this data flow highlights attacks that might target cluster use cases such as data replication, fault detection, and joining a node to the cluster.  

Security Requirements
* Authenticate all new nodes that request to join the cluster to verify authorization
* Data being transmitted between nodes should be encrypted to ensure confidentiality
* Cluster communication should have the ability to operate on a separate network socket or interface so that it can be segmented from data collection and user traffic

Elasticsearch does seem to include features in this area, although these security features are in the X-Pack paid modules.  Encrypting cluster communication and authenticating nodes systems can be done by [configuring TLS and deploying certificates](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/configuring-tls.html#tls-transport) to each node.  Elasticsearch also implements a feature called TCP Transport Profiles that allow cluster traffic between nodes to be[ segmented from other data flows](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/separating-node-client-traffic.html) by designating specific ports or even interfaces for cluster communication.


##### User Searches for Data
Task 4 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### Alert to Fraud Analyst
Task 5 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

In many environments, Elasticsearch might be used to monitor incoming data for specific conditions, and when that condition is met, some type of alert or notification might be raised to a stakeholder.  In the case on a fraud monitoring department, Elasticsearch might be used to run scheduled searches every few minutes looking for outliers in recent credit card transactions.  The [misuse case](ADD) for this data flow shows how attackers might be able to target email alerts and clarifies that other delivery options are needed for  important alerts that need analyst attention.

Security Requirements
* Retain an audit log of all generated alerts

Add Reflection 

### Documentation Review
Task 6

### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects/2