

## Assurance Claim - 1: 

**Top Claim 1: Elasticsearch prevents unauthorized access to the elastic cluster.**

![Preventions of unauthorized access](https://github.com/swrp/CYBR8420-SemesterProject/blob/maddagada/Assurance-Cases/Assurance%20Case-Preventing%20unauthorized%20access.png)

* **Evidence E1:** To gain unauthorized access to the elastic cluster, user must prove his/her identity via username and password credentials. [User authentication methods](https://www.elastic.co/guide/en/shield/current/setting-up-authentication.html) such as LDAP and active directory for managing and authentication are used in the Elasticsearch.
* **Evidence E2:** To prevent anonymous access Elasticsearch added extra security shield in the authentication process of user. By [enabling the anonymous access](https://www.elastic.co/guide/en/shield/current/anonymous-access.html) security the authentication process is done is two phases – token extraction and user credential authentication. In the case when no authentication token was resolved, by default access requests are rejected and an authentication error is returned with status code HTTP 401. If the user does not have access permissions for the requested action, access requests are rejected with an authentication error HTTP 403. 
* **Evidence E3:** In Elasticsearch, Only a user with the [superuser](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/built-in-roles.html) role can grants full access to the cluster, including all the data documents which is clearly stated in the documentation.
* **Evidence E4:** To defend the illegitimate operation such as create/modify/update/delete on data documents administrator can able to assigns the access privilege permissions at field level to the user based on the role in the organization. [Role based access controls page](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/authorization.html) and [Privileges permissions](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/security-privileges.html) are clearly documented in their documentation page.


## Assurance Claim - 2: 

## Assurance Claim - 3: 
**Top Claim 3: Elasticsearch defends against suspicious login activity.**
![Suspicious login attempts](https://github.com/swrp/CYBR8420-SemesterProject/blob/swrp/Assurance-Cases/Assurance-Claim.png)
* **Evidence E1:** Elasticsearch has the flexibility to add filters that can detect successful [brute-force](https://www.elastic.co/blog/integrating-elasticsearch-with-arcsight-siem-part-4) login attempts within a window size of X-minutes. Once the conditions are met [alerts](https://www.elastic.co/guide/en/watcher/current/actions.html#actions-email) actions can be configured to send emails to notify admin.
* **Evidence E2:** To prevent unauthorized login attempts to user accounts [multi-factor authentication](https://www.elastic.co/guide/en/cloud/current/ec-account-security.html) can be enabled. This adds an additional level of security which prompts for login credential's followed by a one-time password sent to the registered mobile.  

## Assurance Claim 4:
![Network Eavesdropping Claim](https://github.com/swrp/CYBR8420-SemesterProject/blob/mabaumgartner/Assurance-Cases/Assurance%20Claim%204.png)

* **Evidence E1:** When [generating certificates](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/configuring-tls.html#node-certificates), Elasticsearch allows private keys to be encrypted with a password, and the passwords to be stored in the Elasticsearch [keystore](https://www.elastic.co/guide/en/elasticsearch/reference/current/secure-settings.html).  The keystore provides an extra layer of protection beyond simple file system permissions.
* **Evidence E2:** To verify traffic is not being sent in plain text but rather an encrypted form, a packet capture could be conducted to verify API calls to Elasticsearch are indeed encrypted.  A simple packet capture could be done with Wireshark or another comparable tool. 
* **Evidence E3:** To verify that all Elasticsearch nodes are using appropriate encryption settings for the given environment, a configuration management tool could be used to enforce the proper configurations or generate a periodic report that could be reviewed by administrative staff.
* **Evidence E4:** Elasticsearch provides a number of [protocols and encryption algorithms](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/security-settings.html#ssl-tls-settings) that would be considered secure by industry standards.  It can seemingly also comply with [FIPS 140-2](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/fips-140-compliance.html#fips-140-compliance).
* **Evidence E5:** Part of enabling encryption for Elasticsearch involves [creating a certificate](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/configuring-tls.html#node-certificates) for each node.  The `xpack.ssl.verification_mode` setting can control the level of [verification](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/security-settings.html#ssl-tls-settings) when communicating over the network.
* **Evidence E6:** Another method that could provide further confidence around ensuring only authorized systems can connect to Elasticsearch, would be to conduct a penetration test on the connection process to verify certificates are verified appropriately in all cases.
* **Evidence E7:** The [IP Filtering](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/ip-filtering.html#ip-filtering) options in Elasticsearch can limit which hosts are allowed to connect.  This further limits connections from unauthorized systems.
* **Evidence E8:**  Elasticsearch provides [segmentation features](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/separating-node-client-traffic.html#separating-node-client-traffic) that would allow cluster communication to be on a separate network than client communication.  An excellent method to test this would be a port scan to ensure logical separation exists as expected.
 
## Assurance Claim 5: 
**Top Claim 5:  Elasticsearch's audit logging functions prevents tampering.**

![Audit Logging Claim](https://github.com/swrp/CYBR8420-SemesterProject/blob/mabaumgartner/Assurance-Cases/Assurance%20Claim%205.png)

* **Evidence E1:** A application penetration test would be the best way to verify that the logging process cannot be forced into a denial of service condition by denying the release or closure of the log file.  This testing could provide assurance that the file would not grow too large or could not be closed for log rotation.
* **Evidence E2:** The Elasticsearch logging process should only append to the log file and will never overwrite data in the open file.  To verify this expected operation, a code review of the audit logging module should be conducted.
* **Evidence E3:** Elasticsearch can be configured to add [multiple outputs](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/auditing.html#auditing) for audit logs including the host file system and an Elasticsearch index.
* **Evidence E4:** To verify that only users with the [superuser role](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/built-in-roles.html) can configure the audit log settings some testing on the application could be performed.
* **Evidence E5:** Elasticsearch needs to capture relevant data elements and sufficient [audit log types](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/audit-event-types.html) to ensure that security issues can be properly investigated.


### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects/4