## Software Security Requirements - Elasticsearch


### Overview
To better define realistic security requirements for Elasticsearch the following environment, data flows, and threat actors were used as the foundation for requirements engineering.  Uses cases and misuse cases were then developed for each data flow to help define security requirements.  Finally, Elasticsearch documentation was reviewed for alignment of the identified security requirements, security configuration, and installation issues.

##### Environment 
* Fraud Monitoring Department at a bank or credit card company using Elasticsearch to store customer information, threat data, and transaction metadata
* The system is critical to the organization's ability to prevent credit card fraud and protect their cardholders

##### Data Flows
The following Elasticsearch data flows were used during the definition of use cases:
1. User storing data into elastic search - *Example: Fraud Analyst types information regarding fraudulent transactions from customer phone call which are then stored in Elasticsearch*
2. System pushes data into cluster - *Example: Credit Card transaction metadata pushed in Elasticsearch from other transaction processing systems*
3. Internal cluster communication - *Example: Elasticsearch nodes copy data between systems for redundancy*
4. User queries for data from cluster - *Example: Fraud Analyst views alerts or reports from Elasticsearch*
5. Alert to Fraud Analyst - *Example: Scheduled search in Elasticsearch sends fraud alert to Analyst when suspicious transactions occur*

##### Threat Actor Examples
There are many threat actors that might want to attack an Elasticsearch cluster when it contains customer information or other valuable data.  Threat actors might also want to disrupt the business functions that Elasticsearch provides to the Fraud Monitoring unit.  The following are some examples of threat actors identified for this scenario.
1. Ransomware Authors
2. Identity Thieves
3. Malicious Insider
4. Hacktivist Agents

### Use Cases / Misuse Cases

##### User Stores Data 
Task 1 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### System Uploads Data
Task 2 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### Internal Cluster Communication
Elasticsearch is often deployed as a multi-node cluster in larger environments to provide data redundancy and increased performance.  There are a variety of protocols that make up the data flow between systems to accomplish smooth, scalable operations of the software.  The [misuse case](https://github.com/swrp/CYBR8420-SemesterProject/blob/master/Misuse%20Cases/Misuse%20Case_Elasticsearch_Cluster%20Communication.jpg) for this data flow highlights attacks that might target cluster nodes when a new node joins the cluster or  nodes perform data replication.  

Security Requirements
* Authenticate all new nodes that request to join the cluster to verify authorization
* Data being transmitted between nodes should be encrypted to ensure confidentiality
* Cluster communication should have the ability to operate on a separate network interface so that it can be segmented from data collection and user traffic

Elasticsearch does seem to include features in this area, although these security features are in the X-Pack paid modules.  Encrypting cluster communication and authenticating nodes can be done by [configuring TLS and deploying certificates](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/configuring-tls.html#tls-transport) to each node.  Elasticsearch also implements a feature called TCP Transport Profiles that allow cluster traffic between nodes to be[ segmented from other data flows](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/separating-node-client-traffic.html) by designating specific ports or even interfaces for cluster communication.


##### User Searches for Data
Task 4 - Description, link to misuse case, list security requirements, reflection (including links to documentation)  

##### Alert to Fraud Analyst
In many environments, Elasticsearch might be used to monitor incoming data for specific conditions, and when that condition is met, some type of alert or notification might be raised to a stakeholder.  In the case of a fraud monitoring department, Elasticsearch might be used to run scheduled searches every few minutes looking for outliers in recent credit card transactions.  The [misuse case](https://github.com/swrp/CYBR8420-SemesterProject/blob/master/Misuse%20Cases/Misuse%20Case_Elasticsearch_Alerting.jpg) for this data flow shows how attackers might be able to target email alerts and clarifies that other delivery options are needed for important alerts that need analyst attention.

Security Requirements
* Retain an audit log of all generated alerts
* Allow alerts to be delivered by a protocol other than email, possibly to a ticketing system or customer relationship management system
* Alert emails should be encrypted or at least transported over an encrypted channel

Elasticsearch (with the X-Pack features) does include the ability for [alerting](https://www.elastic.co/guide/en/elastic-stack-overview/current/xpack-alerting.html), and alerts can be sent in [many forms](https://www.elastic.co/guide/en/elastic-stack-overview/current/actions.html).  The ability to send alerts as an email or webhook action would likely allow an IT service management system to issue a service ticket when an alert is generated.  The documentation also indicates that the software does indeed have the ability to use the STARTTLS protocol when [configuring email settings](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/actions-email.html#configuring-email)

### Documentation Review
##### Installation Settings
* Security has to be enabled explicitly using X-pack settings while installing Elasticsearch, Kibana, Logstash, Beats and Elasticsearch Hardoop as it disabled by default.
* Elastic cloud hosted on elastic search has X-pack always installed so any cluster can be easily monitored and secured.
* Security disabled at the node means it is also disabled for all Kibana instances connected to this Elasticsearch.
##### General Settings
* Elastic search has “changeme” as the default password and elastic search accepts the continuous usage of this password.
* The passwords are hashed and then stored. There are a bunch of hashing algorithms to select from.
* Elastic search defaults the username of the anonymous user but requires specification of roles associated with the user. There is a functionality of the user providing credential to request action based on the given permissions. An HTTP 403 is returned if the user does not have appropriate permissions.
* Built in token service is disabled to prevent sniffing of a token from a plain http connection. Cluster generates a cryptographic key by default which is used to encrypt and authenticate the tokens.
#### Realm Settings
Realm settings have to be configured depending on the realm type. Also, the priority of the realm within the realm chain has to be configured.
* In a native realm, the time to live for cached user entries, maximum number of user entries and the hashing algorithm can be set. If not set, each of them is set to their default.
* In a LDAP realm, URL, load balancing and failover types, DN of the user that is used to bind the LDAP and perform searches and the password for the user along with DN templates and group attribute and a variety of others can be defined. Pooling for user search can be enabled and health checks can be performed on them.
* In Active Directory realm, X-pack security attempts to authenticate against the specified URL and load balancing is brought into effect in case of multiple URLs defined. Much of the attributes that can be defined are similar to the LDAP realm. Metadata of all additional attributes to be loaded into the LDAP server along with TCP & SSL attributes can be defined.
* In PKI realm a pattern is specified which is then used to extract username from certificate DN. Trustore and its passwords are specified same as in LDAP and AD realms. Trustore stores the path to the Java keystore file that contains the certificates to trust.
* In SAML realm, the Entity ID (URL with maximum length of 1024 characters) of the SAML Identity provider is specified. The path to a metadata file is also specified along with other metadata attributes. Also, X-pack security has the functionality of signing outgoing SAML messages by configuring a signing key. Encryption key is configured, using which X-pack security publishes an encryption certificate while the generation of metadata. This is used to decrypt the incoming SAML content.
* In Kerberos realm, keytab path is specified. This would contain the service principal used by that particular Elasticsearch node.
#### TLS/SSL settings
* TLS/SSL settings are configured to include supported protocols, control the server’s behavior with respect to requesting a certificate from client connections. Also, the verification that the certificates have been signed by a trusted authority. Configurations can be made so that PKCS #12 container files can be used by X-pack security to contain the private key and certificates to be trusted.
* Settings are available similarly for both default transport and each transport profile. IP filtering can be enabled by allowing or denting specific IP addresses. Traffic can also be allowed or denied for specific ports or profiles.
* Elasticsearch mitigates the issue of credential theft by storing a hashed version of user credentials in memory. The default algorithm used for this purpose is SHA-256, but other algorithms can also be selected.


### Project Links
* Team Repository: https://github.com/swrp/CYBR8420-SemesterProject
* Project Board: https://github.com/swrp/CYBR8420-SemesterProject/projects/2
