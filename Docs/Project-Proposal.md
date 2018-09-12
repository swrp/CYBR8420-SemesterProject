## Project Proposal - Elasticsearch 

### Description

### License

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

### Motivations

### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects

