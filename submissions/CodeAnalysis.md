## Code Review Strategy

## Manual Code Review
As onserved from our misuse case where [Analyst queries for data from cluster](https://github.com/swrp/CYBR8420-SemesterProject/blob/master/submissions/SoftwareSecurityRequirements.md#analyst-queries-for-data-from-cluster) we have identified use of token service to minimize the CSRF attacks on elasticsearch. Elasticsearch uses tokens which are validated on a time basis and creates a new token once the tokens are expired. This can be found at [line 487](https://github.com/swrp/elasticsearch/blob/76095c7fee7b9982d4ca243c42eacb29f4f9b3a5/x-pack/plugin/security/src/main/java/org/elasticsearch/xpack/security/authc/TokenService.java#L487) in the invalidateAccessTokenFunction. 

## Automated Tool Scan 
