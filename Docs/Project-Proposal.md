## Project Proposal - Elasticsearch 

### Description

### License
The core features in Elasticsearch are open source under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0.html), which is a permissive license from the Apache Software Foundation.  Elastic also provides paid features, through their X-Pack subscriptions.  The X-Pack features are also in the Elasticsearch GitHub repository, however these are published under the [Elastic License](https://github.com/elastic/elasticsearch/blob/0d8aa7527e242fbda9d84867ab8bc955758eebce/licenses/ELASTIC-LICENSE.txt).  So while the X-Pack code is open, it is not truly open source because of the license.

### Contributions

### Security History
Elastic has good resources and and published information about vulnerabilities in the Elasticsearch software.  They have a page summarizing [security issues](https://www.elastic.co/community/security) on their website and a [forum](https://discuss.elastic.co/c/security-announcements) where new security announcements are posted.  Reporting new vulnerabilities to Elastic is as easy as emailing security@elastic.co.  

There have been relatively few security issues in the Elasticsearch software itself.  In the last five years only seven vulnerabilities have been published.  Since the "X-Pack" software was, until recently, more of a separate code-base, those vulnerabilities were categorized separately with nine flaws found since 2017.  In fact all security bugs announced in 2017 were due to the X-Pack features.  The table below provides a quick summary of the number of vulnerabilities found i each of the past five years and the most significant severity according to CVSS v2.0. 

| Year | Elasticsearch | X-Pack | Highest Severity|
| ---- | ------------- | ------ | ----------------|
| 2014 | 2             | 0      | Medium          |
| 2015 | 5             | 0      | High            | 
| 2016 | 0             | 0      | N/A             |
| 2017 | 0             | 8      | Medium          |
| 2018 | 2             | 1      | High            |


### User Security Needs
   
   User authentication to protect data flow from unauthorized users and modifications.
    
   Data Integrity to prevent accidental data loss, corruption and unintentional modifications.

  **Identity Access Management** to Manage user activities on Elastic search cluster.
    
   Fine grained user privileges and attribute based access controls to prevent unauthorized access to Elastic search cluster.
      
   Access control's on stored data procedures. 
      
      For ex: If a client finds a bug in the application that gives access to elasticsearch 
      this gives them access to data in all indexes and grab data that belongs to other clients.
      (This can be eliminated with the use of a commercial plugin called SHIELD). 
      As a user I except this to be a part of elasticsearch.
       
   **Data Encryption** to protect user data (credit card information, email addresses, passwords) as it travels with in the clusters. 

   Secure (TLS/SSL) certificates to establish trust between cluster's. 

   Audit log for all unauthorized login attempts, nefarious network traffic trying to enter the cluster, detect false connections with no signatures.   

   Making sure that clusters are hidden with deep private networks and only accessible to required applications. 
   Manually disable features that are not used by the application(eg: default ports).

### Security Features
Since elastic search is made up of many moving parts, it has various layers of security. X-pack security is the security provider that works on elastic search on various levels. Following is a further description of the levels:

User Authentication: Authentication services called realms, provided built in by X-pack, handles the process. There are some built in realms like native, ldap, active_directory, pki, file, saml. Also, one can built their own realm, which can then be plugged into X-pack.

Authorization: This refers to the process of identifying whether the requesting user is allowed to execute the request. It involves 5 sub-parts:
•	Secured resources
•	Privilege
•	Permissions- set of privileges
•	Role- named set of permission
•	User 

Node/Client Authentication & Channel Encryption: Encryption of data transmitted over the wire and certificate-based node authentication. This is achieved by configuring IP filters.

Auditing: Logs almost all activities that take place in the system so as to assist analysis in case of anomalies.


### Motivations

### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects

