## Code Review Strategy

Before diving into the code analysis, the foremost important analysis we ensured is reviewing our assurance cases, misuse cases, and threat model report. From the review, we observed the most effective functionality concerned parts in the software and decided to approach the checklist review strategy which is the most effective method for analyzing the code of large-scale projects like Elasticsearch. To reduce the effort of going through all the code line by line we decided on adopting checklist strategy.

We analyzed our code in both automated and manual review process. The automated code review is performed using open source static code analysis tool called **PWD**. The selection of vulnerabilities in the automation tool to analyze is narrowed to **CWE(Common Weakness Enumeration)** that are related to our misuse case, assurance cases, and threat model. The resultant vulnerability from the tool is also examined manually. 

## Manual Code Review

The main functionality parts of the code that we focused mainly on the manual analysis are:

From our misuse case and threat report, we identified vulnerability related to the [CWE-798: Use of Hard-coded Credentials](https://cwe.mitre.org/data/definitions/798.html). There are maximum chances of attacker finding loop hole from this vulnerability that can lead to the disclosure of sensitive information and gaining unauthorized access to the sensitive files. The code issue is located in the file [KeyStoreWrapper at line 40]( https://github.com/elastic/elasticsearch/blob/master/x-pack/plugin/core/src/main/java/org/elasticsearch/license/CryptUtils.java). At the line 40 default pass phrase key value is **hard coded** which is used to decrypt the private key file. Attacker can easily decrypt the private key.

From the misuse case and threat report, we performed manual code review to verify the [CWE-284: Improper Access Control]( https://cwe.mitre.org/data/definitions/284.html). From the review, we see almost everything is very carefully managed the settings for **Access Control based on user role** and in handling the document-level privileges. There is medium severity issue related to the **Trusting all the incoming SSL certificates** from the server is observed under [CWE-300: Channel Accessible by Non-Endpoint](https://cwe.mitre.org/data/definitions/300.html). This could maximize the chances of affecting the integrity and confidentiality of the data. Attacker can read or modify the communication taking this advantage as the loop hole. The issue is located in the file [TrustAllConfig at line 46]( https://github.com/elastic/elasticsearch/blob/master/x-pack/plugin/core/src/main/java/org/elasticsearch/xpack/core/ssl/TrustAllConfig.java).



## Automated Tool Scan 
