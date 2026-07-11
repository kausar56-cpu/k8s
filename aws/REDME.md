Q: How do you log in to GitHub Enterprise using Okta SSO?

Answer: First, I open the GitHub Enterprise URL. Then I click on "Sign in with SSO" or "Continue with Okta". It redirects me to the Okta login page. I enter my company email and password, then complete the MFA verification using the Authenticator app. After successful authentication, I am automatically logged in to GitHub Enterprise.

Q: Can you explain the complete Git workflow you follow in your project?

        │
        ▼
1. Create a new feature branch from the main branch
        │
        ▼
2. Write the code in the feature branch
        │
        ▼
3. git add .
        │
        ▼
4. git commit -m "Added login feature"
        │
        ▼
5. git push origin feature/login
        │
        ▼
6. Create a Pull Request (PR)
   (feature/login → main)
        │
        ▼
7. Team Lead / Reviewer reviews the code
   CI/CD pipeline runs
   (Build, Test, Security Checks)
        │
        ▼
8. All checks pass ✅
   PR is approved
        │
        ▼
9. Merge into the main branch
        │
        ▼
10. Delete the feature branch

Q: What branch naming convention do you follow in your project?

Answer:

In our project, we follow a standard branch naming convention. We use feature/ for new features, bugfix/ for bug fixes, and hotfix/ for urgent production issues. If we use Jira, we also include the ticket ID in the branch name, for example feature/JIRA-123-user-login. This helps the team easily identify the purpose of the branch and link it to the related task. We also use lowercase letters and hyphens (-) to keep branch names consistent and easy to read.

Sure. I won't change your answers. I'll only add the interview question above each answer.


---

Q: Where do you find the branch naming rules in your project?

📄 Rules कुठे? → README / Confluence / Team Wiki
👨‍💼 कोण सांगतं? → Team Lead / Senior
👀 कसं समजतं? → आधीच्या branches बघून
🔗 काही teams मध्ये? → Jira branch नाव suggest करतं


---

Q: How do you merge a feature branch into the main branch?

Yes. First, I switch to the main branch because I want to bring the feature code into main. Then I run git merge feature/login. This command copies the changes from the feature/login branch into the main branch.


---

Q: What is a Fast-Forward Merge?

Fast-forward merge happens only when no new commits are added to the main branch after the feature branch is created.


---

Q: Can you explain Fast-Forward Merge with an example?

Suppose I create a feature branch and start working. If no one changes the main branch during that time, when I merge my feature branch, Git directly moves the main branch to my latest commits. This is called a fast-forward merge.


---

Q: What is a Merge Conflict?

A merge conflict occurs when two developers modify the same code in different branches. When they try to merge those branches, Git cannot decide which change to keep, so it creates a merge conflict. We then resolve it manually.


---

Q: How do you resolve a Merge Conflict?

👉 Accept Current / Incoming / Both


---

Q: What is the difference between Fast-Forward Merge and Three-Way Merge?

Only feature changed → Fast-Forward
✅ Main + Feature both changed → Three-Way Merge


---

Q: What is Squash Merge?

"Squash combines multiple commits into one clean commit. It removes unnecessary commit history and keeps the main branch clean and easy to understand."


---

Q: What is Rebase?

"Rebase is used to update my feature branch with the latest code from the main branch. If other developers have added commits to the main branch, my feature branch becomes outdated. I use git rebase main. Git first brings the latest code from the main branch into my feature branch, then it reapplies my commits on top of the latest code. This keeps the commit history clean and up to date."

Command:

git switch feature/login
git rebase main

🎯 Golden Line: Merge joins branches. Rebase updates the feature branch with the latest code from the main branch.

तुझे answers मी बदलत नाही. खाली फक्त interview questions add केले आहेत.


---

Q: Can you explain Fast-Forward Merge?

Answer:

> "In a fast-forward merge, I am working on a feature branch. Before I merge my code, no one has committed any new changes to the main branch. In this case, Git simply moves the main branch pointer forward. It does not create a merge commit."




---

Q: Can you explain Three-Way Merge?

Answer:

> "In a three-way merge, I am working on a feature branch, and meanwhile another developer has already committed changes to the main branch. When I merge my feature branch into the main branch, Git detects that both branches have new commits. So Git creates a merge commit to combine both histories."




---

Q: What is Rebase?

Answer:

> "I use rebase when my feature branch becomes outdated because other developers have committed changes to the main branch. Rebase first brings the latest code from the main branch into my feature branch. Then Git reapplies my commits on top of the latest code. After that, I can merge my feature branch into the main branch."




---

Q: What is the difference between Merge and Rebase?

Answer:

> "Merge is used when I want to merge my feature branch into the main branch. It combines both branches and, if needed, Git creates a merge commit. It also preserves the complete history.



> Rebase is used when my feature branch becomes outdated because other developers have committed changes to the main branch. I use git rebase main to bring the latest code from the main branch into my feature branch. Then Git reapplies my commits on top of the latest code. After that, I can merge my feature branch into the main branch."




---

Q: When do you use Merge and when do you use Rebase?

Answer:

> "I use rebase before merging to update my feature branch with the latest code from the main branch. Once my feature branch is up to date and tested, I use merge to bring my feature branch into the main branch."



One-line trick:

Merge = Feature → Main

Rebase = Main → Feature (Update Feature)



---

Q: What is Git Cherry-pick?

Answer:

> "Suppose I am working on a feature branch with multiple commits. One of those commits is an urgent bug fix that needs to go to production immediately. Instead of merging the entire feature branch, I use git cherry-pick to move only that specific commit to the main branch."




---

Q: What are the steps to use Git Cherry-pick?

1. Find Commit ID
        ↓
2. Switch to Target Branch
        ↓
3. git cherry-pick <commit-id>
        ↓
4. Only that commit is copied


---

Q: Can you explain Git Cherry-pick with an example?

Answer:

> "Suppose I'm working on the develop branch. It has many commits because multiple features are under development. One of those commits is a critical bug fix. The production team needs that bug fix immediately, but the other features are not ready for release. In that situation, I don't merge the entire develop branch. Instead, I switch to the main branch and use git cherry-pick <commit-id> to copy only the bug-fix commit into the main branch."




---

Q: What is Git Stash?

Answer:

> stash = save work




---

Q: What is Git Stash Pop?

Answer:

> pop = bring back work + remove stash




---

Q: What is the difference between Reset, Revert, and Restore?

Answer:

> Think of it this way:

git restore = Erasing pencil marks on the current page (undo uncommitted changes)

git revert = Writing a correction on the next page: "Page 5 was wrong, here's the fix" (safe undo)

git reset = Ripping out pages from the notebook (rewrites history — careful!)




---

Q: What are the different modes of Git Reset?

Answer:

> "Git reset has three modes: soft keeps changes in staging, mixed keeps changes in working directory, and hard completely removes commits and changes from history."



Easy Trick:

soft → keep staged

mixed → unstage

hard → delete everything



---

Q: Can we use git reset --hard on a shared branch?

Answer:

> Shared branch = Always revert, never reset --hard




---

Q: How can you recover lost commits after Git Reset?

Answer:

> "Even if you lose commits using reset, git reflog can help you recover them."




---

Q: What is the difference between Git Push, Pull, and Fetch?

Answer:

> push = send code
pull = get code
fetch = only see updates




---

Q: What is the difference between Clone and Fork?

Answer:

> Clone = GitHub ➜ Laptop
🍴 Fork = Someone's GitHub ➜ Your GitHub ➜ Laptop




---

Q: What is the difference between Git Fetch and Git Pull?

Answer:

> "git fetch downloads the latest changes from the remote repository without modifying my local branch. git pull first performs a fetch and then automatically merges those changes into my current branch."




---

Q: How does your CI/CD pipeline work for different branches?

Answer:

feature/*  → Build + Unit Test

develop    → Deploy to DEV

release/*  → Deploy to STAGING + QA Testing

main       → Deploy to PRODUCTION


---

Q: Can you explain your Git branching flow?

Feature
   ↓
Develop
   ↓
Release
   ↓
QA
   ↓
Main (Production)
   ↓
Feature...


---

Q: How do you handle releases in a microservices architecture?

Answer:

> "In our microservices architecture, each service is deployed independently. We don't wait for all services to be ready. Each microservice has its own CI/CD pipeline and its own release cycle, so changes in one service do not require releasing all the others."




---

Q: How do you handle a production hotfix?

Answer:

> "If a critical issue happens in production, we create a hotfix branch from the main branch because main contains the production code. We fix only that issue, test it, create a Pull Request, and merge it into main. After deploying the fix to production, we also merge the hotfix into the develop branch. This is important because future releases are created from develop. If we don't merge the fix into develop, the same bug can appear again in the next release."




---

Q: Why do you merge the hotfix into the develop branch?

Answer:

> "We merge the hotfix into develop so that the bug fix is included in future releases. Otherwise, the next release from develop could bring the same production bug back."
>
तुझे answers न बदलता, फक्त interview questions add केले आहेत.


---

Q: Can you explain your Production VPC design?

Production VPC:     10.0.0.0/16   (65,536 IPs)
│
├── Public Subnets (Load Balancers, Bastion)
│   ├── 10.0.1.0/24   (251 usable IPs) — AZ-a
│   ├── 10.0.2.0/24   (251 usable IPs) — AZ-b
│   └── 10.0.3.0/24   (251 usable IPs) — AZ-c
│
├── Private Subnets (Application Servers, ECS/EKS)
│   ├── 10.0.10.0/24  (251 usable IPs) — AZ-a
│   ├── 10.0.20.0/24  (251 usable IPs) — AZ-b
│   └── 10.0.30.0/24  (251 usable IPs) — AZ-c
│
├── Database Subnets (RDS, ElastiCache)
│   ├── 10.0.100.0/24 (251 usable IPs) — AZ-a
│   ├── 10.0.200.0/24 (251 usable IPs) — AZ-b
│   └── 10.0.201.0/24 (251 usable IPs) — AZ-c
│
└── Reserved for future (10.0.40.0/24 – 10.0.99.0/24)

Note: AWS reserves 5 IPs per subnet (first 4 + last 1)
      /24 = 256 total - 5 reserved = 251 usable


---

Q: Can you explain your banking microservices architecture?

Customer (Web / Mobile App)
                                         |
                               +------------------+
                               |  AWS ALB / Nginx |
                               +------------------+
                                         |
                                  API Gateway
                                         |
    ---------------------------------------------------------------------------------
    |          |           |          |          |          |         |              |
 User MS   Auth MS   Account MS  Customer MS  Loan MS  Payment MS  Card MS  Notification MS
    |          |           |          |          |          |         |              |
    ---------------------------------------------------------------------------------
           |          |           |          |          |          |         |
 Transaction MS  Beneficiary MS  Statement MS  KYC MS  Fraud MS  Audit MS  Report MS
           |          |           |          |          |          |         |
    ---------------------------------------------------------------------------------
                                         |
                                  Message Queue
                              (Kafka / RabbitMQ)
                                         |
                     -------------------------------------
                     |                |                  |
                 Email Service    SMS Service     Push Notification
                                         |
                           --------------------------
                           |                        |
                    Redis Cache              Elasticsearch
                           |                        |
                           --------------------------
                                         |
                                 MySQL / PostgreSQL
                                         |
                                   Amazon RDS


---

Q: Can you explain the request flow in your application?

Customer
   │
   ▼
Mobile App / Website
   │
   ▼
Load Balancer (ALB)
   │
   ▼
API Gateway
   │
   ├── Login Service
   ├── Customer Service
   ├── Account Service
   ├── Balance Service
   ├── Transaction Service
   ├── Payment Service
   ├── UPI Service
   ├── Beneficiary Service
   ├── Card Service
   ├── Loan Service
   ├── KYC Service
   ├── Notification Service
   ├── Fraud Detection Service
   ├── Statement Service
   └── Audit Service


---

Q: Can you explain your CI/CD pipeline?

Developer
    │
GitHub
    │
Jenkins
    │
Maven Build
    │
SonarQube
    │
Docker Build
    │
Trivy Scan
    │
Push to ECR
    │
Helm/Kubectl
    │
Amazon EKS
    │
ALB
    │
Customer


---

Q: What is set -x in Shell Scripting?

Answer:

> set -x is used to debug a shell script. It displays each command before execution.

तुझे answers बदललेले नाहीत. फक्त interview questions वर add केले आहेत.


---

Q: Can you explain your project and your role in it?

Answer:

> "Yes, sure. Our project was a banking application with around 10 to 15 microservices, and I worked on the DevOps team. I'll explain the complete project step by step.

First, based on the client requirements, the architecture was designed, and then we started provisioning the AWS infrastructure. We used Terraform to automate the creation of AWS resources such as VPC, public and private subnets, route tables, Internet Gateway, NAT Gateway, Security Groups, IAM roles, EKS cluster, S3 bucket for the Terraform backend, and DynamoDB for state locking.

Once the infrastructure was ready, the developers committed their code to GitHub. Whenever the code was pushed, Jenkins automatically triggered the CI/CD pipeline. In the pipeline, we integrated SonarQube for code quality analysis, Trivy for security scanning, Nexus for artifact management, Docker for containerizing the application, and Amazon ECR for storing Docker images. Finally, Jenkins deployed the application to the Amazon EKS cluster.

We had multiple environments, including lower environments for development and testing, and a production environment. Before deploying to production, all changes were validated in the lower environments.

For application access, we configured Route 53 for DNS, an Application Load Balancer to receive incoming traffic, and the NGINX Ingress Controller to route requests to the appropriate microservice running inside the EKS cluster. We also used ACM to configure SSL certificates, so the application was accessible securely over HTTPS.

Apart from this, we also worked on automation tasks using AWS Lambda and Python. For example, we automated the cleanup of stale EBS snapshots using Boto3, IAM roles, and CloudWatch scheduling, which helped us optimize AWS costs.

This was the overall architecture and deployment process of our project, and my primary responsibilities included infrastructure automation using Terraform, CI/CD pipeline management, Kubernetes deployments on EKS, and supporting application deployments and monitoring."




---

Q: Can you explain Cross-Account IAM Role access in CI/CD?

Developer
     │
     ▼
GitHub
     │
     ▼
Jenkins (Dev Account)
     │
     │ 1. Pipeline starts
     ▼
Assume IAM Role
(Production Account)
     │
     │ 2. Temporary credentials from AWS STS
     ▼
Production Account
     │
     ├── Deploy to EKS
     ├── Access S3
     └── Update other AWS resources


---

Q: How did you manage multiple environments in your project?

Answer:

> "All environments were managed through Git branches and ArgoCD. Each environment had its own branch, and ArgoCD automatically synchronized and deployed the application to the respective Kubernetes environment. We did not use Cross-Account access in our deployment process."




---

Q: When do you use IRSA in Amazon EKS?

Answer:

> "If an application is running inside an EKS cluster and it needs to access AWS services such as S3, Secrets Manager, DynamoDB, SQS, or other AWS services, then we configure an OIDC provider and use IAM Roles for Service Accounts (IRSA). This allows the pod to securely access AWS services without storing AWS access keys."




---

Q: What is VPC Peering?

Answer:

> "VPC Peering is used to securely connect two VPCs over AWS's private network. It allows resources in one VPC to communicate with resources in another VPC using private IP addresses, without using the public internet."




---

Q: What is the difference between mvn package, mvn install, and mvn deploy?

Answer:

> mvn package → JAR फक्त target/ मध्ये तयार होतो.
mvn install → JAR target/ मध्ये तयार होतो आणि local Maven repository (~/.m2/repository) मध्येही कॉपी होतो.
mvn deploy → JAR तयार होतो आणि Nexus/JFrog सारख्या remote repository मध्ये upload होतो.




---

Q: How do you build and store Maven artifacts in your project?

Answer:

> "Whenever a developer pushes the code to Git, it is in source code format, not in a deployable format. So, as a DevOps engineer, I use Maven to build the application. First, I verify Maven using mvn -version, and then I run mvn clean package to generate the JAR file.

We don't keep the JAR only on the local build server because it is not a central and reliable storage. So, we upload it to Nexus by using mvn deploy. In the pom.xml, we configure the Nexus repository details using distributionManagement, and Jenkins uses those details to upload the artifact automatically.

After that, during the Docker build stage, the JAR is available in the Jenkins workspace, and the Dockerfile uses the COPY instruction to copy the JAR into the Docker image. Then we build the Docker image and continue with deployment."




---

Q: Which Jenkins plugins have you used in your project?

Answer:

Git Plugin

GitHub Plugin (or GitLab Plugin)

Maven Integration Plugin

Pipeline Plugin

Pipeline: Stage View Plugin

Blue Ocean Plugin (Optional)

JDK Tool Plugin

SonarQube Scanner Plugin

OWASP Dependency-Check Plugin

Nexus Artifact Uploader Plugin

Docker Pipeline Plugin

Docker Plugin

Kubernetes Plugin

Kubernetes CLI Plugin

AWS Credentials Plugin

Pipeline: AWS Steps Plugin

Credentials Binding Plugin

SSH Agent Plugin

Publish Over SSH Plugin

Email Extension Plugin (Email-ext)

Slack Notification Plugin (Optional)

Prometheus Metrics Plugin (Optional)



---

Q: What is pom.xml?

Answer:

> "pom.xml is the configuration file of a Maven project. It tells Maven what dependencies to download, which plugins to use, how to build the application, and whether to create a JAR or WAR file. Whenever Jenkins runs the Maven build, Maven reads the pom.xml file and generates the artifact accordingly."




---

Q: Can you explain the Jenkins Controller and Agent architecture?

Answer:

> "In our project, we used a Jenkins Controller and multiple Agents. The Controller was responsible for managing Jenkins, triggering pipelines, and assigning jobs to the appropriate Agent. The Agent executed the actual tasks such as Git checkout, Maven build, SonarQube scan, Docker image creation, pushing the image to ECR, and deploying the application to EKS. This setup reduced the load on the Controller and allowed multiple builds to run in parallel."




---

Q: Why did you configure passwordless sudo for the Jenkins user?

Answer:

> "In our project, Jenkins was running on a Linux server. During the CI/CD pipeline, Jenkins had to execute commands like Docker build, Docker push, Kubernetes deployment, and other administrative tasks. These commands required sudo access. Since Jenkins is a non-interactive service, it cannot enter a password during pipeline execution. So, we used sudo visudo to grant the Jenkins user passwordless sudo access by adding:

jenkins ALL=(ALL) NOPASSWD: ALL

This allowed Jenkins to execute all the required commands automatically without any manual intervention, ensuring the CI/CD pipeline ran successfully."

तुझे answers जसेच्या तसे ठेवले आहेत. फक्त प्रत्येकाच्या वर interview question add केला आहे.


---

Q: How do you securely access private EC2 instances in production?

Answer:

> "In production environments, we typically use AWS Systems Manager (SSM) Session Manager instead of SSH keys and Bastion Hosts. Each EC2 instance is attached to an IAM role with the AmazonSSMManagedInstanceCore policy, and the SSM Agent runs on the instance. Users are granted IAM permissions, allowing them to securely connect to private EC2 instances directly from the AWS Console or AWS CLI. This eliminates the need to manage .pem keys, improves security, provides centralized access control, and enables session logging and auditing."




---

Q: Which Route 53 records did you use in your project?

Answer:

> "In my project, I primarily used Alias Records and TXT Records in Route 53. We used Alias Records to map our application domain to the Application Load Balancer because our application was deployed behind an ALB. Since Alias Records support the root domain and integrate directly with AWS resources, they were the preferred choice. We also used TXT Records for domain ownership verification whenever required. I have worked with A Records as well for environments where a domain needed to point directly to an EC2 instance's public IP address."




---

Q: Which DNS record do you use in different scenarios?

Answer:

> "In my project, I mainly used Alias Record because our application was deployed behind an Application Load Balancer (ALB). I also used TXT Record for domain verification. If an application is hosted directly on an EC2 instance with a public IP, then we use an A Record."



Easy Trick:

EC2 (Public IP) → A Record

ALB / NLB / CloudFront / S3 → Alias Record

Domain Verification → TXT Record

One Domain → Another Domain → CNAME



---

Q: How did you manage domains for your applications?

Answer:

> "In our project, we had one root domain, and each application or microservice was accessed through a separate subdomain."




---

Q: Which record did you use for DNS validation?

Answer:

> "We used a CNAME record for DNS validation."




---

Q: What is the role of API Gateway?

Answer:

> "API Gateway request घेतो, authenticate करतो, योग्य backend service कडे पाठवतो आणि response परत client ला देतो."




---

Q: Have you implemented AWS Cross-Account Access?

Answer:

> "Implemented AWS IAM Cross-Account Access using IAM Roles and AWS STS AssumeRole between Master, Staging, and QA accounts."




---

Q: Can you explain AWS Cross-Account Access with three AWS accounts?

Master Account
      admin1 / admin2
             │
      sts:AssumeRole
        /            \
       ▼              ▼
Staging Account    QA Account
  Staging-Role       QA-Role
       │                │
AdministratorAccess  AdministratorAccess


---

Q: How do EC2 IAM Roles and STS AssumeRole differ?

Answer:

> EC2 + IAM Role = Access Keys लागत नाहीत (Automatic Temporary Credentials).



> IAM User + sts:AssumeRole = Temporary Credentials मिळतात आणि Role च्या permissions ने access मिळतो.




---

Q: How did you provide EC2 access to Amazon S3 securely?

Answer:

> "Implemented IAM Roles for EC2 to securely access Amazon S3 using temporary credentials without storing access keys."




---

Q: What is AWS STS AssumeRole?

Answer:

> "Configured AWS STS AssumeRole for secure, temporary, role-based access to AWS resources."




---

Q: How did you trigger Jenkins automatically after code was pushed to GitHub?

Answer:

> "Configured GitHub Webhooks to automatically trigger Jenkins pipelines on every code push, enabling Continuous Integration (CI)."




---

Q: How did you integrate GitHub with Jenkins?

Answer:

> "In my project, we integrated GitHub with Jenkins using a webhook. I configured the GitHub repository in Jenkins, enabled the 'GitHub hook trigger for GITScm polling' option, and added the Jenkins webhook URL in GitHub. Whenever a developer pushed code to GitHub, Jenkins automatically triggered the pipeline, pulled the latest code, built the application, and started the deployment process. This eliminated the need to trigger builds manually."




---

Q: How did you implement cross-account deployment in your CI/CD pipeline?

Answer:

> "Implemented cross-account deployment using AWS IAM Roles and AWS STS AssumeRole from Jenkins to Production AWS accounts."
>
मी तुझे दिलेले answers जसे आहेत तसे ठेवतो. फक्त प्रत्येकाच्या वर Interview Question add करून format करतो.


---

Q: Where did you use AWS KMS in your project?

Answer:

"In my project, we mainly used AWS KMS in five places:

Terraform remote state (S3 backend)

EBS volume encryption

RDS encryption

Secrets Manager"



---

Q: What was your role in auditing as a DevOps Engineer?

Answer:

"As a DevOps Engineer, I was responsible for monitoring AWS CloudTrail logs for security and infrastructure-related activities. I verified who accessed KMS keys, who made changes to IAM roles and policies, and who created, modified, or deleted AWS resources such as EC2, S3, and RDS. I also ensured CloudTrail was enabled, logs were stored securely in an encrypted S3 bucket, and I supported troubleshooting and security investigations whenever required."


---

Q: How did you check unauthorized activity in AWS?

Answer:

"I checked CloudTrail logs to see who accessed AWS resources, who used KMS keys, and who made changes to IAM, EC2, or S3. If I found any unusual or unauthorized activity, I informed my Team Lead or the Security Team and shared the CloudTrail logs for investigation."


---

Q: What do you mean by centrally managing encryption keys?

Answer:

"In our project, we created one customer-managed KMS key and used it for multiple AWS services such as S3, EBS, RDS, and Secrets Manager. Instead of creating separate encryption keys for each service, we managed everything from AWS KMS. If we needed to update the key policy, enable key rotation, or change permissions, we did it in one place, and the changes applied to all the services using that key."


---

Q: How did you perform KMS auditing?

Answer:

"I regularly reviewed CloudTrail logs to monitor KMS key usage and identify any unauthorized access or unusual activities. If I found any issues, I informed my Team Lead."


---

Q: How did you perform KMS Key Review / Access Review?

Answer:

"I periodically reviewed KMS key policies and IAM permissions to ensure that only authorized users and applications had access to the encryption keys."


---

Q: Did you implement KMS Key Rotation? Why did you use it?

Answer:

"In our project, we enabled automatic key rotation for our customer-managed KMS key. This improved security because AWS automatically rotated the key at regular intervals. We did not need to make any changes to our applications or AWS services, and all services continued using the same KMS key without interruption."

Why did we use key rotation?

"We used key rotation to improve security, reduce the risk of long-term key exposure, and meet compliance requirements."


---

Q: How did you handle compliance requirements in your project?

Answer:

"In our project, I had to follow compliance requirements to ensure that sensitive data was secure."


---

Q: How did you configure Transit Gateway connectivity between multiple VPCs and regions?

Answer:

(Transit Gateway steps as provided by you)


---

Q: How many VPCs were configured in your Transit Gateway setup?

Answer:

"North Virginia region had two VPCs:

Dev → 10.0.0.0/16

Testing → 192.168.0.0/16


Ohio region had one VPC:

Pre-Prod → 172.16.0.0/16"



---

Q: How did you manage multiple AWS environments securely?

Answer:

"Managed multiple AWS environments (Development, Testing, and Production) by using IAM Cross-Account Roles (Switch Role), enabling secure access and administration across AWS accounts.

Configured and managed AWS Transit Gateway and Transit Gateway Peering to establish secure network connectivity between multiple VPCs across environments and regions by updating VPC and TGW route tables."


---

Q: Which Route 53 routing policies did you use in your project?

Answer:

"Configured AWS Route 53 Failover and Latency routing policies with Health Checks to improve application availability and user experience."


---

Q: How did you secure Amazon S3 bucket access?

Answer:

"Managed secure access to Amazon S3 buckets using IAM and Bucket Policies while maintaining Block Public Access."


---

Q: How did you provide application log access from S3 without making the bucket public?

Answer:

"Configured Amazon S3 bucket policies to provide secure access to developers while keeping the bucket private."


---

Q: Client does not have AWS access but needs a report from S3. How will you provide it?

Answer:

"We can generate a pre-signed URL with limited permissions and expiry time, allowing the client to securely download the report without providing AWS access."


---

Q: How did you provide folder-level access in S3?

Answer:

"Configured S3 Access Points to provide folder-level access for different teams."


---

Q: How did you implement S3 Cross-Region Replication?

Answer:

"Manager says:

Our application stores files in the Mumbai region. We need a backup in another AWS region so that if the Mumbai region becomes unavailable, our data is still safe.

Solution:

We use S3 Cross-Region Replication (CRR)."


---

Q: How did you protect internet-facing applications in AWS?

Answer:

"Configured AWS WAF and AWS Shield to protect internet-facing applications by blocking unwanted IP addresses and mitigating DDoS attacks."


---

Q: How did you block unwanted traffic from a specific IP using AWS WAF?

Answer:

"Our application was receiving unwanted traffic from a specific public IP. So, I created an IP Set in AWS WAF, added that IP, created a Web ACL, and attached it to the ALB. After that, requests from that IP were blocked. AWS Shield protected the application from DDoS attacks."


Q: How did you connect Kubernetes logs to OpenSearch Dashboards?

Answer:

"To connect logs to OpenSearch Dashboards, we first deploy OpenSearch and OpenSearch Dashboards in the Kubernetes cluster. Then we deploy Fluent Bit as a DaemonSet so that one Fluent Bit pod runs on every worker node. Fluent Bit reads container logs from /var/log/containers/*.log and forwards them to OpenSearch. OpenSearch indexes and stores the logs, and OpenSearch Dashboards provides a UI where we can search, filter, and analyze logs for troubleshooting."


---

Q: How did you deploy a static website on AWS?

Answer:

"In my project, the frontend team shared the static website files like index.html, CSS, JavaScript, and images. My responsibility was to make the website live on AWS. First, I created an S3 bucket and uploaded all the website files. Then I configured CloudFront in front of the S3 bucket to improve performance and enable HTTPS. After that, I requested an SSL certificate from ACM and validated it through Route 53. Finally, I mapped the domain name to the CloudFront distribution using an Alias A record in Route 53. After testing, the website was accessible securely over HTTPS."


---

Q: Why did you use CloudFront?

Answer:

"We used CloudFront because users can access the website from different locations. CloudFront keeps a cached copy of the website at AWS Edge Locations, so users get faster responses instead of every request going to the S3 bucket. It also provides HTTPS support using ACM, integrates with AWS WAF for security, and reduces the load on the S3 bucket."


---

Q: Why did you use S3 for website hosting?

Answer:

"Because it was a static website. S3 is a cost-effective and highly available service for hosting static content like HTML, CSS, JavaScript, and images."


---

Q: How did private EC2 instances access S3 securely?

Answer:

"In our project, we had private EC2 instances that needed to access an S3 bucket. Instead of routing traffic through a NAT Gateway, we created a Gateway VPC Endpoint for S3 and associated it with the private route table. This enabled secure, private communication over the AWS network, improved security, and reduced NAT Gateway costs. For services like Systems Manager, we used Interface Endpoints to manage private EC2 instances without SSH."


---

Q: How did you access private EC2 instances without internet access?

Answer:

"Our EC2 instance was in a private subnet with no internet access. To manage it without SSH, we used AWS Systems Manager. Since there was no internet, we created Interface Endpoints for SSM, SSM Messages, and EC2 Messages. We also attached the AmazonSSMManagedInstanceCore IAM role to the EC2 instance. This allowed us to connect to the instance using Session Manager."


---

Q: How did you configure S3 VPC Endpoint in your project?

Answer:

"First, I created a VPC with public and private subnets. Initially, the private EC2 instance was accessing S3 through a NAT Gateway. To avoid internet traffic and reduce NAT costs, I created a Gateway VPC Endpoint for S3, associated it with the private route table, and updated the S3 bucket policy if required. After that, the private EC2 instance accessed the S3 bucket directly through the AWS network without using the internet."


---

Q: What security services and mechanisms did you use in your project?

Answer:

"Security: SG, NACL, IAM, Private Subnet, WAF, RBAC, VPC Flow Logs."


---

Q: Where did you check application and network logs?

Answer:

"Logs: Terminal, VPC Flow Logs, OpenSearch."


---

Q: Which monitoring tools did you use in your project?

Answer:

"Monitoring: Prometheus + Grafana."






