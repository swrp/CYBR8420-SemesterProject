

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
## Assurance Claim - 4: 

## Assurance Claim - 5: 
