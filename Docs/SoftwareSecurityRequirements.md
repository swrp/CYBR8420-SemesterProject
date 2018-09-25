## Software Security Requirements - Elasticsearch


### Overview
To better define realistic security requirements for Elasticsearch the following environment, data flows, and threat actors were used as the foundation for requirements engineering.  Uses cases and misuse cases were the developed for each data flow.

##### Environment 
* Fraud Monitoring Department at a bank or credit card company using Elasticsearch to store customer information, threat data, and transaction information
##### Data Flows
The following Elasticsearch data flows....
1. User storing data into elastic search - *Example: Fraud Analyst types notes from customer interaction*
2. System pushes data into cluster - *Example: Credit Card transaction data pushed in Elasticsearch from other systems*
3. Internal cluster communication - *Example: Elasticsearch nodes copy data between systems for redundancy*
4. User queries for data from cluster - *Example: Fraud Analyst views alerts or reports from Elasticsearch*
5. Monitoring Network Traffic

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
Elasticsearch is often deployed as a multi-node cluster in larger environments to provide data redundancy and increased performance.  There are a variety of protocols that make up the data flow between systems to accomplish smooth, scalable operations of the software.

##### User Searches for Data
Task 4 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### Monitoring Network Traffic
Task 5 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

### Documentation Review
Task 6

### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects/2