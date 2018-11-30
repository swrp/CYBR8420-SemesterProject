## Code Review Strategy

Before diving into the code analysis, the foremost important analysis we ensured is reviewing our assurance cases, misuse cases, and threat model report. From the review, we observed the most effective functionality concerned parts in the software and decided to approach the checklist review strategy which is the most effective method for analyzing the code of large-scale projects like Elasticsearch. To reduce the effort of going through all the code line by line we decided on adopting checklist strategy.

We analyzed our code in both automated and manual review process. The automated code review is performed using open source static code analysis tool called **PWD**. The selection of vulnerabilities in the automation tool to analyze is narrowed to **CWE(Common Weakness Enumeration)** that are related to our misuse case, assurance cases, and threat model. The resultant vulnerability from the tool is also examined manually. The main functionality parts of the code that we focused mainly on the manual analysis are:

* **Authorization**
* **Input Sanitization**
* **Session Token Validation**

## Manual Code Review



## Automated Tool Scan 
