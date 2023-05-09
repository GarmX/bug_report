# CodeFever by PGYER has arbitrary code execution (RCE)

BUG_Author: GarminXee

vendors: https://github.com/PGYER/codefever

This project star has 2.4k.

Vulnerability verification:

Ordinary command execution


![image](https://github-production-user-asset-6210df.s3.amazonaws.com/54017627/237123690-128b1ccb-12fa-428b-93d6-42c34ecf6e10.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230509%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230509T142436Z&X-Amz-Expires=300&X-Amz-Signature=942bd8d2c16254463660fac62d6004ecefaf1c1d41f1d5e98c87a2e06513f6c5&X-Amz-SignedHeaders=host&actor_id=54017627&key_id=0&repo_id=436107857)

![image](https://github-production-user-asset-6210df.s3.amazonaws.com/54017627/237123828-12aa801f-3713-4972-a145-16ceeab55791.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230509%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230509T142502Z&X-Amz-Expires=300&X-Amz-Signature=fc62a5d1cdf1213e0ed39e6454b0c2d4a1e64a8b58fecbad190dee81bb398e3f&X-Amz-SignedHeaders=host&actor_id=54017627&key_id=0&repo_id=436107857)


Rebound shell

![image](https://github.com/GarmX/bug_report/assets/77141248/1a7ebffa-1383-49af-bc1a-b0bda6510416)

Loophole analysis:

1. Follow the interface to find / api/repository/createMergeRequest and find the corresponding controller
![image](https://github.com/GarmX/bug_report/assets/77141248/abc13819-aca6-4d77-8a72-d59e6fda7fd9)


2. After the merge branch is created, it enters the processing logic and triggers the call to getLastCommit
![image](https://github.com/GarmX/bug_report/assets/77141248/d9b15cb1-37b5-4534-bf0d-019a64ee0c94)


3. Follow up the getLastCommit method, without filtering, directly encapsulate the command execution function
![image](https://github.com/GarmX/bug_report/assets/77141248/8872ad2f-0de7-4103-9c77-815c4f44e67d)


4. Call the execCommand method in repository_model
![image](https://github.com/GarmX/bug_report/assets/77141248/fff93f86-7d0d-4ee2-ba91-7cbce8eae0ef)


5. Finally, call batch, and then execute the command.

![image](https://github.com/GarmX/bug_report/assets/77141248/784f4aca-dd53-4c10-90d3-1ee5035a7e70)
