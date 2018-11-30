## Code Review Strategy

## Manual Code Review
As observed from our misuse case where [Analyst queries for data from cluster](https://github.com/swrp/CYBR8420-SemesterProject/blob/master/submissions/SoftwareSecurityRequirements.md#analyst-queries-for-data-from-cluster) we have identified that use of token service would minimize attacks like CSRF, session hijacking, CORS, etc on elasticsearch. Elasticsearch is implementing tokens which are validated on a time basis and creates a new token once they are expired. This can be found at [line 487](https://github.com/swrp/elasticsearch/blob/76095c7fee7b9982d4ca243c42eacb29f4f9b3a5/x-pack/plugin/security/src/main/java/org/elasticsearch/xpack/security/authc/TokenService.java#L487) in the invalidateAccessToken Function. 

Link: [CVE-2015-8131](https://nvd.nist.gov/vuln/detail/CVE-2015-8131)

Severity: 6.8 Medium

Identified Versions: Elasticsearch Kibana before 4.1.3 and 4.2.x 



## Automated Tool Scan 
