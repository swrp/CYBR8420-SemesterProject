

## Assurance Claim - 1: 

## Assurance Claim - 2: 

## Assurance Claim - 3: 

## Assurance Claim 4: 
**Top Claim 4: Elasticsearch minimizes the possibility of network eavesdropping attacks.**
* **Evidence E1:** When [generating certificates](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/configuring-tls.html#node-certificates), Elasticsearch allows private keys to be encrypted with a password, and the passwords to be stored in the Elasticsearch [keystore](https://www.elastic.co/guide/en/elasticsearch/reference/current/secure-settings.html).  The keystore provides an extra layer of protection beyond simple file system permissions.
* **Evidence E2:** To verify traffic is not being sent in plain text but rather an encrypted form, a packet capture could be conducted to verify API calls to Elasticsearch are indeed encrypted.  A simple packet capture could be done with Wireshark or another comparable tool. 
* **Evidence E3:** To verify that all Elasticsearch nodes are using appropriate encryption settings for the given environment, a configuration management tool could be used to enforce the proper configurations or generate a periodic report that could be reviewed by administrative staff.
* **Evidence E4:** Elasticsearch provides a number of [protocols and encryption algorithms](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/security-settings.html#ssl-tls-settings) that would be considered secure by industry standards.  It can seemingly also comply with [FIPS 140-2](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/fips-140-compliance.html#fips-140-compliance).
* **Evidence E5:** Part of enabling encryption for Elasticsearch involves [creating a certificate](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/configuring-tls.html#node-certificates) for each node.  The `xpack.ssl.verification_mode` setting can control the level of [verification](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/security-settings.html#ssl-tls-settings) when communicating over the network.
* **Evidence E6:** Another method that could provide further confidence around ensuring only authorized systems can connect to Elasticsearch, would be to conduct a penetration test on the connection process to verify certificates are verified appropriately in all cases.
* **Evidence E7:** The [IP Filtering](https://www.elastic.co/guide/en/elastic-stack-overview/6.4/ip-filtering.html#ip-filtering) options in Elasticsearch can limit which hosts are allowed to connect.  This further limits connections from unauthorized systems.
* **Evidence E8:**  Elasticsearch provides [segmentation features](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/separating-node-client-traffic.html#separating-node-client-traffic) that would allow cluster communication to be on a separate network than client communication.  An excellent method to test this would be a port scan to ensure logical separation exists as expected.
 
## Assurance Claim - 5: 
