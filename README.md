
# Git & GitHub Interview Notes (One Topic = One Point)

### 1. GitHub Enterprise Login (SSO + Okta)

* GitHub Enterprise URL उघडतो.
* **Sign in with SSO** किंवा **Continue with Okta** वर क्लिक करतो.
* Okta login page उघडते.
* Company email आणि password टाकतो.
* MFA (Authenticator App) approve करतो.
* परत GitHub मध्ये login होतो.

---

### 2. Git Workflow

1. main branch वरून नवीन feature branch तयार कर.
2. feature branch वर code लिही.
3. `git add .`
4. `git commit -m "Added login feature"`
5. `git push origin feature/login`
6. GitHub वर Pull Request तयार कर (feature/login → main)
7. Team Lead / Reviewer code review करतो आणि CI/CD pipeline (build, test, security checks) चालते.
8. सर्व checks ✅ Green आणि PR approve.
9. Merge into main.
10. Feature branch delete.

---

### 3. Branch Naming Convention

> "In our projects, we follow a standard branch naming convention.
>  We use prefixes like **feature/** for new features, **bugfix/** for bug fixes, and **hotfix/** for urgent production issues.
>  If we use Jira, we also include the ticket ID in the branch name,
> for example **feature/JIRA-123-user-login**. This helps the team easily
>  identify the purpose of the branch and link it to the corresponding task.
>  We also use lowercase letters and hyphens (-) to keep branch names consistent and easy to read."

---

### 4. Branch Naming Rules कुठे मिळतात?

* 📄 Rules → README / Confluence / Team Wiki
* 👨‍💼 Team Lead / Senior सांगतो
* 👀 आधीच्या branches बघून समजतं
* 🔗 काही teams मध्ये Jira branch नाव suggest करतं

---

### 5. Merge Command

> "Yes. First, I switch to the main branch because I want to bring the feature code into main.
> Then I run `git merge feature/login`.
> This command copies the changes from the feature/login branch into the main branch."

---

### 6. Fast-Forward Merge (Definition)

> "Fast-forward merge happens only when no new commits are added to the
>  main branch after the feature branch is created."

---

### 7. Merge Conflict

> "A merge conflict occurs when two developers modify the same code in different branches.
> When they try to merge those branches, Git cannot decide which change to keep,
> so it creates a merge conflict. We then resolve it manually."

---

### 8. Merge Conflict Options

* Accept Current
* Accept Incoming
* Accept Both

---

### 9. Fast-Forward Merge (Example)

> "Suppose I create a feature branch and start working. If no one changes
>  the main branch during that time, when I merge my feature branch,
> Git directly moves the main branch to my latest commits. This is called a fast-forward merge."

---

### 10. Fast-Forward vs Three-Way Merge

* ✅ Only feature changed → Fast-Forward
* ✅ Main + Feature both changed → Three-Way Merge

---

### 11. Squash

> "Squash combines multiple commits into one clean commit. It removes unnecessary commit history and keeps the main branch clean and easy to understand."

---

### 12. Rebase

> "Rebase is used to update my feature branch with the latest code from
>  the main branch. If other developers have added commits to the main
> branch, my feature branch becomes outdated. I use `git rebase main`.
>  Git first brings the latest code from the main branch into my feature branch,
> then it reapplies my commits on top of the latest code.
>  This keeps the commit history clean and up to date."

**Commands**

```bash
git switch feature/login
git rebase main
```

**Golden Line**

> "Merge joins branches. Rebase updates the feature branch with the latest code from the main branch."

---

### 13. Fast-Forward Merge (Interview Answer)

> "In a fast-forward merge, I am working on a feature branch. Before I merge my code,
>  no one has committed any new changes to the main branch. In this case,
> Git simply moves the main branch pointer forward. It does not create a merge commit."

---

### 14. Three-Way Merge (Interview Answer)

> "In a three-way merge, I am working on a feature branch, and meanwhile
>  another developer has already committed changes to the main branch.
> When I merge my feature branch into the main branch, Git detects that
>  both branches have new commits. So Git creates a merge commit to combine both histories."

---

### 15. Rebase (Interview Answer)

> "I use rebase when my feature branch becomes outdated because other
>  developers have committed changes to the main branch. Rebase first brings
>  the latest code from the main branch into my feature branch, then
> it reapplies my commits on top of the latest code."

---

### 16. Merge vs Rebase

> "Merge is used when I want to merge my feature branch into the main branch. It combines both branches and, if needed, Git creates a merge commit. It also preserves the complete history.

> Rebase is used when my feature branch becomes outdated because other
>  developers have committed changes to the main branch. I use `git rebase main`
>  to bring the latest code from the main branch into my feature branch. Then Git
>  reapplies my commits on top of the latest code. After that, I can merge my
> feature branch into the main branch."

**If interviewer asks: When do you use Merge and when do you use Rebase?**

> "I use rebase before merging to update my feature branch with the latest
> code from the main branch. Once my feature branch is up to date and tested,
> I use merge to bring my feature branch into the main branch."

---

### 17. Cherry-pick

> "Suppose I am working on a feature branch with multiple commits.
>  One of those commits is an urgent bug fix that needs to go to production immediately.
>  Instead of merging the entire feature branch, I use `git cherry-pick`
>  to move only that specific commit to the main branch."


खालील points पण **जसेच्या तसे (answers न बदलता)** फक्त व्यवस्थित organize केले आहेत.

---

# 18. Cherry-pick Workflow

1. Find Commit ID
2. Switch to Target Branch
3. `git cherry-pick <commit-id>`
4. Only that commit is copied

---

# 19. Cherry-pick (Interview Answer)

> "Suppose I'm working on the develop branch. It has many commits
> because multiple features are under development. One of those commits
> is a critical bug fix. The production team needs that bug fix immediately,
>  but the other features are not ready for release. In that situation,
>  I don't merge the entire develop branch. Instead, I switch to the main
>  branch and use `git cherry-pick <commit-id>` to copy only the bug-fix commit into the main branch."

---

# 20. Cherry-pick Example

```text
develop
A ── B ── C ── D (Bug Fix) ── E ── F ── G

main
A ── B ── X ── Y
```

---

# 21. Git Stash

> stash = save work

Command

```bash
git stash
```

---

# 22. Git Stash Pop

> pop = bring back work + remove stash

Command

```bash
git stash pop
```

---

# 23. Undoing Changes — Reset, Revert, Restore

Things go wrong. Git gives you multiple ways to undo changes — each for a different situation.

Think of it this way:

* `git restore` = Erasing pencil marks on the current page (undo uncommitted changes)
* `git revert` = Writing a correction on the next page: "Page 5 was wrong, here's the fix" (safe undo)
* `git reset` = Ripping out pages from the notebook (rewrites history — careful!)

---

# 24. Git Reset Commands

```bash
git reset --soft HEAD~1
```

Undo last commit, keep changes staged.

```bash
git reset --mixed HEAD~1
```

Undo last commit, keep changes unstaged (default).

```bash
git reset --hard HEAD~1
```

Undo last commit, DELETE all changes — gone forever!

---

# 25. Git Reset (Interview Answer)

> "Git reset has three modes: soft keeps changes in staging,
> mixed keeps changes in working directory, and hard completely removes commits and changes from history."

**Easy Trick**

* soft → keep staged
* mixed → unstage
* hard → delete everything

---

# 26. Reset vs Revert Rule

> Shared branch = Always revert, never reset --hard

---

# 27. Git Reflog

> "Even if you lose commits using reset, git reflog can help you recover them."

---

# 28. Push vs Pull vs Fetch

* push = send code
* pull = get code
* fetch = only see updates

---

# 29. Clone vs Fork

* Clone = GitHub ➜ Laptop
* 🍴 Fork = Someone's GitHub ➜ Your GitHub ➜ Laptop

---

# 30. Fetch vs Pull (Interview Answer)

> "git fetch downloads the latest changes from the remote
>  repository without modifying my local branch. git pull
> first performs a fetch and then automatically merges those changes into my current branch."

---

# 31. CI/CD Pipeline by Branch

* feature/* → Build + Unit Test
* develop → Deploy to DEV
* release/* → Deploy to STAGING + QA Testing
* main → Deploy to PRODUCTION

---

# 32. Release Flow

```text
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
पुन्हा Feature...
```

---

# 33. Microservices Deployment (Interview Answer)

> "In our microservices architecture, each service is deployed independently.
>  We don't wait for all services to be ready. Each microservice has
>  its own CI/CD pipeline and its own release cycle, so changes
> in one service do not require releasing all the others."

---

# 34. Hotfix Flow (Interview Answer)

> "If a critical issue happens in production, we create a hotfix branch from
>  the main branch because main contains the production code. We fix only that issue,
>  test it, create a Pull Request, and merge it into main. After deploying
> the fix to production, we also merge the hotfix into the develop branch.
> This is important because future releases are created from develop.
> If we don't merge the fix into develop, the same bug can appear again in the next release."

---

# 35. Why Merge Hotfix into Develop?

> "We merge the hotfix into develop so that the bug fix is included in future releases.
>  Otherwise, the next release from develop could bring the same production bug back."

---

# 36. AWS Request Flow

> "When a user accesses [www.myapp.com](http://www.myapp.com), Route 53 resolves
> the domain name to an IP address. CloudFront serves cached static content if available.
>  The request then goes to the Load Balancer, which distributes traffic to
>  healthy EC2 instances. The application running on EC2 processes the request,
> retrieves or stores data in RDS, and uploads static files to S3 if needed.
> CloudWatch monitors the infrastructure, and if any issue occurs, it sends alerts through SNS."

---

# 37. IAM Role vs Policy

* Role = Who are you? (Temporary identity)
* Policy = What can you do? (Permissions)

---

# 38. Types of IAM Policies

* AWS Managed → AWS created it
* Customer Managed → We created it
* Inline → Only for one user/group/role

---

# 39. Which IAM Policy Do You Mostly Use?

> "Mostly, I use Customer Managed Policies because they are customized for our project.
> AWS Managed Policies are used for standard access. Inline Policies are used very
>  rarely because they are meant for only one specific user, group, or role."

---

# 40. IAM Policy Types (Interview Answer)

* AWS Managed Policy → Created and managed by AWS. We use it for standard permissions.
* Customer Managed Policy → Created and managed by us based on project requirements.
* Inline Policy → Attached to only one user, group, or role for a specific purpose and cannot be reused.

---

# 41. IAM Permission Evaluation

> "AWS verifies whether the request is allowed. If it is not allowed, the request is denied. If it is allowed and there is no explicit deny, the request is allowed."

---

# 42. IAM Best Practices

> "I enable MFA on the root account, avoid using the root account for daily work,
>  use IAM Groups and Roles, follow the principle of least privilege,
> use OIDC for CI/CD instead of access keys, enable IAM Access Analyzer,
>  rotate access keys if required, implement SCPs and Permission Boundaries,
> and regularly audit IAM users and credentials."

**Top 5 IAM Best Practices**

* MFA on Root Account
* Never use Root for daily tasks
* Use IAM Roles instead of Access Keys
* Follow Least Privilege
* Use OIDC for CI/CD

---

# 43. Production VPC Design

```text
Production VPC:     10.0.0.0/16   (65,536 IPs)

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
```

हेही तुझ्या आधीच्या notes प्रमाणे **एकही answer न बदलता**, फक्त topic-wise organize केले आहेत.

---

# 44. Banking Microservices Architecture

```text
Customer (Web / Mobile App)
                                         |
                                         |
                               +------------------+
                               |  AWS ALB / Nginx |
                               +------------------+
                                         |
                                  API Gateway
                                         |
    ---------------------------------------------------------------------------------
    |          |           |          |          |          |         |              |
    |          |           |          |          |          |         |              |
 User MS   Auth MS   Account MS  Customer MS  Loan MS  Payment MS  Card MS  Notification MS
    |          |           |          |          |          |         |              |
    ---------------------------------------------------------------------------------
           |          |           |          |          |          |         |
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
```

---

# 45. Request Flow

```text
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
```

---

# 46. CI/CD Pipeline Flow

```text
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
```

---

# 47. Shell Script Debugging

> `set -x` is used to debug a shell script. It displays each command before execution.

---

# 48. Complete Project Architecture

## Application Architecture

```text
Users
                           │
                           ▼
                     Route 53 (DNS)
                           │
                           ▼
                Application Load Balancer
                           │
                           ▼
          NGINX Ingress Controller / Reverse Proxy
                           │
      ┌────────────────────┼────────────────────┐
      ▼                    ▼                    ▼
 Microservice-1      Microservice-2      Microservice-3
      │                    │                    │
      └────────────────────┼────────────────────┘
                           │
                           ▼
                    Amazon RDS Database
```

---

## CI/CD Architecture

```text
Developer
    │
    ▼
 GitHub
    │
    ▼
 Jenkins Pipeline
    │
    ├── Build
    ├── SonarQube
    ├── Trivy Scan
    ├── Docker Build
    ├── Push Docker Image to Amazon ECR
    └── Deploy to Amazon EKS
                           │
                           ▼
                     Kubernetes (EKS)
                           │
                           ▼
         (Microservices shown in the top diagram)
```

---

## Terraform Infrastructure

```text
Terraform
    │
    ├── VPC
    ├── Public Subnet
    ├── Private Subnet
    ├── Internet Gateway
    ├── NAT Gateway
    ├── Route Tables
    ├── Security Groups
    ├── IAM Roles
    ├── EKS Cluster
    ├── ALB
    ├── Route 53
    └── ACM Certificate
```

---

# 49. Tell Me About Your Project (Interview Answer)

> "Yes, sure. Our project was a banking application with around 10 to 15 microservices,
>  and I worked on the DevOps team. I'll explain the complete project step by step.
>
> First, based on the client requirements, the architecture was designed, and then
>  we started provisioning the AWS infrastructure. We used Terraform to automate the
creation of AWS resources such as VPC, public and private subnets, route tables,
> Internet Gateway, NAT Gateway, Security Groups, IAM roles, EKS cluster, S3 bucket
>  for the Terraform backend, and DynamoDB for state locking.
>
> Once the infrastructure was ready, the developers committed their code to GitHub.
>  Whenever the code was pushed, Jenkins automatically triggered the CI/CD pipeline.
> In the pipeline, we integrated SonarQube for code quality analysis, Trivy for security
> scanning, Nexus for artifact management, Docker for containerizing the application,
> and Amazon ECR for storing Docker images. Finally,
> Jenkins deployed the application to the Amazon EKS cluster.
>
> We had multiple environments, including lower environments for development and
>  testing, and a production environment. Before deploying to production, all changes
> were validated in the lower environments.
>
> For application access, we configured Route 53 for DNS, an Application Load Balancer
> to receive incoming traffic, and the NGINX Ingress Controller to route requests to the
>  appropriate microservice running inside the EKS cluster. We also used ACM to
>  configure SSL certificates, so the application was accessible securely over HTTPS.
>
> Apart from this, we also worked on automation tasks using AWS Lambda and Python.
>  For example, we automated the cleanup of stale EBS snapshots using Boto3,
>  IAM roles, and CloudWatch scheduling, which helped us optimize AWS costs.
>
> This was the overall architecture and deployment process of our project, a
> nd my primary responsibilities included infrastructure automation using
> Terraform, CI/CD pipeline management, Kubernetes deployments on EKS, and
> supporting application deployments and monitoring."

---

# 50. Project Flow (Quick Revision)

Client Requirement

↓

Architecture

↓

Terraform

↓

GitHub

↓

Jenkins

↓

SonarQube

↓

Trivy

↓

Nexus

↓

Docker

↓

ECR

↓

EKS

↓

Route 53

↓

ALB

↓

NGINX Ingress

↓

ACM (HTTPS)

↓

Lambda Automation

↓

Monitoring

---

# 51. Cross-Account Deployment (Assume Role)

```text
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
```

हेही **एकही answer न बदलता**, फक्त topic-wise organize केले आहेत.

---

# 52. Maven Build Lifecycle

* `mvn package` → JAR फक्त `target/` मध्ये तयार होतो.
* `mvn install` → JAR `target/` मध्ये तयार होतो आणि local Maven repository
* (`~/.m2/repository`) मध्येही कॉपी होतो.
* `mvn deploy` → JAR तयार होतो आणि Nexus/JFrog सारख्या remote repository मध्ये upload होतो.

---

# 53. Maven to Nexus to Docker Flow (Interview Answer)

> "Whenever a developer pushes the code to Git, it is in source code format,
>  not in a deployable format. So, as a DevOps engineer, I use Maven to build
> the application. First, I verify Maven using `mvn -version`, and then I run
> `mvn clean package` to generate the JAR file.
>
> We don't keep the JAR only on the local build server because it is not
>  a central and reliable storage. So, we upload it to Nexus by using
> `mvn deploy`. In the pom.xml, we configure the Nexus repository details
> using `distributionManagement`, and Jenkins uses those details to upload the artifact automatically.
>
> After that, during the Docker build stage, the JAR is available in the
> Jenkins workspace, and the Dockerfile uses the `COPY` instruction to copy
>  the JAR into the Docker image. Then we build the Docker image and continue with deployment."

---

# 54. Common Jenkins Plugins

* Git Plugin
* GitHub Plugin (or GitLab Plugin)
* Maven Integration Plugin
* Pipeline Plugin
* Pipeline: Stage View Plugin
* Blue Ocean Plugin (Optional)
* JDK Tool Plugin
* SonarQube Scanner Plugin
* OWASP Dependency-Check Plugin
* Nexus Artifact Uploader Plugin
* Docker Pipeline Plugin
* Docker Plugin
* Kubernetes Plugin
* Kubernetes CLI Plugin
* AWS Credentials Plugin
* Pipeline: AWS Steps Plugin
* Credentials Binding Plugin
* SSH Agent Plugin
* Publish Over SSH Plugin
* Email Extension Plugin (Email-ext)
* Slack Notification Plugin (Optional)
* Prometheus Metrics Plugin (Optional)

---

# 55. pom.xml (Interview Answer)

> "pom.xml is the configuration file of a Maven project. It tells Maven what dependencies to download, which plugins to use, how to build the application, and whether to create a JAR or WAR file. Whenever Jenkins runs the Maven build, Maven reads the pom.xml file and generates the artifact accordingly."

---

# 56. Jenkins Controller and Agent (Interview Answer)

> "In our project, we used a Jenkins Controller and multiple Agents.
> The Controller was responsible for managing Jenkins, triggering pipelines,
>  and assigning jobs to the appropriate Agent. The Agent executed the actual
>  tasks such as Git checkout, Maven build, SonarQube scan, Docker image creation,
>  pushing the image to ECR, and deploying the application to EKS.
>  This setup reduced the load on the Controller and allowed multiple builds to run in parallel."

---

# 57. Passwordless sudo for Jenkins (Interview Answer)

> "In our project, Jenkins was running on a Linux server. During the CI/CD pipeline,
> Jenkins had to execute commands like Docker build, Docker push, Kubernetes deployment,
>  and other administrative tasks. These commands required sudo access. Since Jenkins
> is a non-interactive service, it cannot enter a password during pipeline execution.
>  So, we used `sudo visudo` to grant the Jenkins user passwordless sudo access by adding:
>
> `jenkins ALL=(ALL) NOPASSWD: ALL`
>
> This allowed Jenkins to execute all the required commands automatically without any manual intervention, ensuring the CI/CD pipeline ran successfully."

---

# 58. AWS Systems Manager (SSM) Session Manager (Interview Answer)

> "In production environments, we typically use AWS Systems Manager
> (SSM) Session Manager instead of SSH keys and Bastion Hosts. Each EC2 instance
>  is attached to an IAM role with the AmazonSSMManagedInstanceCore policy,
> and the SSM Agent runs on the instance. Users are granted IAM permissions,
> allowing them to securely connect to private EC2 instances directly from the
>  AWS Console or AWS CLI. This eliminates the need to manage .pem keys,
> improves security, provides centralized access control, and enables session logging and auditing."

---

# 59. Route 53 Records (Interview Answer)

> "In my project, I primarily used Alias Records and TXT Records in Route 53.
>  We used Alias Records to map our application domain to the Application
> Load Balancer because our application was deployed behind an ALB. Since
> Alias Records support the root domain and integrate directly with AWS resources,
>  they were the preferred choice. We also used TXT Records for domain ownership
>  verification whenever required. I have worked with A Records
> as well for environments where a domain needed to point directly to an EC2 instance's public IP address."

---

# 60. Route 53 (Short Interview Answer)

> "In my project, I mainly used Alias Record because our application
> was deployed behind an Application Load Balancer (ALB). I also used
>  TXT Record for domain verification. If an application is
> hosted directly on an EC2 instance with a public IP, then we use an A Record."

---

# 61. Easy Route 53 Trick

* EC2 (Public IP) → A Record
* ALB / NLB / CloudFront / S3 → Alias Record
* Domain Verification → TXT Record
* One Domain → Another Domain → CNAME

---

# 62. Domain Structure

> "In our project, we had one root domain, and each application
> or microservice was accessed through a separate subdomain."

---

# 63. DNS Validation

> "We used a CNAME record for DNS validation."

---

# 64. API Gateway

> "API Gateway request घेतो, authenticate करतो, योग्य backend service
>  कडे पाठवतो आणि response परत client ला देतो."

---

# 65. Cross-Account Access

> "Implemented AWS IAM Cross-Account Access using IAM Roles and AWS STS
> AssumeRole between Master, Staging, and QA accounts."

---

# 66. Cross-Account Access Setup

### Step 1: Staging Account

* IAM → Roles → Create Role
* Trusted Entity → AWS Account
* Another AWS Account → Master Account ID
* Attach AdministratorAccess
* Role Name → `Staging-Role`

---

### Step 2: QA Account

* IAM → Roles → Create Role
* Trusted Entity → AWS Account
* Another AWS Account → Master Account ID
* Attach AdministratorAccess
* Role Name → `QA-Role`

---

### Step 3: Master Account

* Create User `admin1`
* Create User `admin2`
* Create User Group `Admins`
* Add `admin1` आणि `admin2` त्या Group मध्ये

---

### Step 4: Create Policy in Master

* User Group ला AssumeRole policy attach करा.

---

# 67. EC2 IAM Role

> "Implemented IAM Roles for EC2 to securely access Amazon S3 using
> temporary credentials without storing access keys."

---

# 68. IAM Role vs STS AssumeRole

* EC2 + IAM Role = Access Keys लागत नाहीत (Automatic Temporary Credentials).
* IAM User + `sts:AssumeRole` = Temporary Credentials
* मिळतात आणि Role च्या permissions ने access मिळतो.

---

# 69. AWS STS AssumeRole

> "Configured AWS STS AssumeRole for secure, temporary, role-based access to AWS resources."

---

# 70. GitHub Webhook

> "Configured GitHub Webhooks to automatically trigger Jenkins pipelines on every code push, enabling Continuous Integration (CI)."

---

# 71. GitHub Webhook with Jenkins (Interview Answer)

> "In my project, we integrated GitHub with Jenkins using a webhook.
>  I configured the GitHub repository in Jenkins, enabled the
> 'GitHub hook trigger for GITScm polling' option, and added the
> Jenkins webhook URL in GitHub. Whenever a developer pushed
> code to GitHub, Jenkins automatically triggered the pipeline, pulled
> the latest code, built the application, and started the deployment process. T
> his eliminated the need to trigger builds manually."

---

# 72. Cross-Account Deployment

> "Implemented cross-account deployment using AWS IAM Roles and
>  AWS STS AssumeRole from Jenkins to Production AWS accounts."

आता तुझे notes **1 ते 72 topics** मध्ये व्यवस्थित organize झाले आहेत.
हे interview revision आणि mock interview दोन्हीसाठी उपयोगी sequence आहे.

खालील notes **एकही answer न बदलता**, फक्त topic-wise organize केले आहेत.

---

# 73. AWS KMS Usage

> In my project, we mainly used AWS KMS in five places:

* Terraform remote state (S3 backend)
* EBS volume encryption
* RDS encryption
* Secrets Manager

---

# 74. Auditing as a DevOps Engineer (Interview Answer)

> "As a DevOps Engineer, I was responsible for monitoring
>  AWS CloudTrail logs for security and infrastructure-related activities.
> I verified who accessed KMS keys, who made changes to IAM roles a
> nd policies, and who created, modified, or deleted AWS resources such
> as EC2, S3, and RDS. I also ensured CloudTrail was enabled, logs were stored
>  securely in an encrypted S3 bucket, and I supported troubleshooting and security investigations whenever required."

---

# 75. CloudTrail Monitoring (Short Interview Answer)

> "I checked CloudTrail logs to see who accessed AWS resources, who used KMS keys,
>  and who made changes to IAM, EC2, or S3. If I found any unusual or unauthorized activity,
>  I informed my Team Lead or the Security Team and shared the CloudTrail logs for investigation."

---

# 76. Centrally Managing Encryption Keys (Interview Answer)

> "In our project, we created one customer-managed KMS key and used
> it for multiple AWS services such as S3, EBS, RDS, and Secrets Manager
> . Instead of creating separate encryption keys for each service,
> we managed everything from AWS KMS. If we needed to update the key policy,
>  enable key rotation, or change permissions, we did it in one place,
> and the changes applied to all the services using that key."

---

# 77. KMS Auditing

> "I regularly reviewed CloudTrail logs to monitor KMS key usage and
> identify any unauthorized access or unusual activities.
> If I found any issues, I informed my Team Lead."

---

# 78. KMS Key Review

> "I periodically reviewed KMS key policies and IAM permissions
>  to ensure that only authorized users and applications had access to the encryption keys."

---

# 79. KMS Key Rotation

> "In our project, we enabled automatic key rotation for our
>  customer-managed KMS key. This improved security because AWS
> automatically rotated the key at regular intervals. We did not
> need to make any changes to our applications or AWS services,
> and all services continued using the same KMS key without interruption."

---

# 80. Why Key Rotation?

> "We used key rotation to improve security, reduce the risk of long-term key exposure, and meet compliance requirements."

---

# 81. Compliance

> "In our project, I had to follow compliance requirements to ensure that sensitive data was secure."

---

# 82. Dev VPC Setup

### Step 1: Create Dev VPC (North Virginia)

1. AWS Console → VPC
2. Region → North Virginia (us-east-1)
3. Create VPC
4. Name → Dev-VPC
5. CIDR → 10.0.0.0/16
6. Create

**Create Subnets**

* Public Subnet → 10.0.1.0/24
* Private Subnet → 10.0.2.0/24

**Internet Gateway**

* Create Internet Gateway
* Attach to Dev VPC

**Route Table**

Public Route Table

* Destination → 0.0.0.0/0
* Target → Internet Gateway

Private Route Table

* Local route only

**Launch EC2**

* Public subnet मध्ये Bastion/EC2
* Private subnet मध्ये Application EC2

---

# 83. Testing VPC Setup

### Step 2: Create Testing VPC (North Virginia)

1. Create VPC
2. Name → Testing-VPC
3. CIDR → 192.168.0.0/16

**Create Subnets**

* Public → 192.168.1.0/24
* Private → 192.168.2.0/24

---

# 84. Environment VPCs

North Virginia मध्ये 2 VPCs आहेत:

* Dev → 10.0.0.0/16
* Testing → 192.168.0.0/16

Ohio मध्ये 1 VPC आहे:

* Pre-Prod → 172.16.0.0/16

---

# 85. IAM Cross-Account Roles

> "Managed multiple AWS environments (Development, Testing, and Production)
> by using IAM Cross-Account Roles (Switch Role), enabling secure access
> and administration across AWS accounts."

---

# 86. Transit Gateway

> "Configured and managed AWS Transit Gateway and Transit Gateway Peering
> to establish secure network connectivity between multiple VPCs across
> environments and regions by updating VPC and TGW route tables."

---

# 87. Route 53 Routing Policies

> "Configured AWS Route 53 Failover and Latency routing policies
> with Health Checks to improve application availability and user experience."

---

# 88. S3 Bucket Security

> "Managed secure access to Amazon S3 buckets using IAM and Bucket
> Policies while maintaining Block Public Access."

---

# 89. Private S3 Access

**Requirement**

> "We need access to application logs stored in S3, but the bucket should not be public."

**Solution**

> "Configured Amazon S3 bucket policies to provide secure access to
> developers while keeping the bucket private."

---

# 90. S3 Access Points

**Requirement**

> "I don't have AWS access, but I need today's report."

**Solution**

> "Configured S3 Access Points to provide folder-level access for different teams."

---

# 91. S3 Cross-Region Replication (CRR)

**Requirement**

> "Our application stores files in the Mumbai region. We need a
> backup in another AWS region so that if the Mumbai region becomes unavailable, our data is still safe."

**Solution**

> "We use S3 Cross-Region Replication (CRR)."

---

# 92. AWS WAF & Shield

> "Configured AWS WAF and AWS Shield to protect internet-facing
>  applications by blocking unwanted IP addresses and mitigating DDoS attacks."

---

# 93. WAF Example

> "Our application was receiving unwanted traffic from a specific public IP. So, I created an IP Set in AWS WAF, added that IP, created a Web ACL, and attached it to the ALB. After that, requests from that IP were blocked. AWS Shield protected the application from DDoS attacks."

---

# 94. OpenSearch Logging

> "To connect logs to OpenSearch Dashboards, we first deploy
> OpenSearch and OpenSearch Dashboards in the Kubernetes cluster.
>  Then we deploy Fluent Bit as a DaemonSet so that one Fluent
> Bit pod runs on every worker node. Fluent Bit reads container
> logs from /var/log/containers/*.log and forwards them to OpenSearch.
>  OpenSearch indexes and stores the logs, and OpenSearch Dashboards
>  provides a UI where we can search, filter, and analyze logs for troubleshooting."

---

# 95. Static Website Hosting (Interview Answer)

> "In my project, the frontend team shared the static website files like i
> ndex.html, CSS, JavaScript, and images. My responsibility was to make the
>  website live on AWS. First, I created an S3 bucket and uploaded all the
> website files. Then I configured CloudFront in front of the S3 bucket to
>  improve performance and enable HTTPS. After that, I requested an SSL
>  certificate from ACM and validated it through Route 53. Finally,
> I mapped the domain name to the CloudFront distribution using an
>  Alias A record in Route 53. After testing, the website was accessible securely over HTTPS."

---

# 96. Why CloudFront?

> "We used CloudFront because users can access the website from
> different locations. CloudFront keeps a cached copy of the
> website at edge locations, which reduces latency, improves performance,
>  and also enables secure HTTPS access."

---

# 97. Gateway VPC Endpoint

> "In our project, we had private EC2 instances that needed to
>  access an S3 bucket. Instead of routing traffic through a NAT Gateway,
>  we created a Gateway VPC Endpoint for S3 and associated it with the
> private route table. This enabled secure, private communication over
> the AWS network, improved security, and reduced NAT Gateway costs.
> For services like Systems Manager, we used Interface Endpoints to
>  manage private EC2 instances without SSH."

---

# 98. Interface Endpoints for SSM

> "Our EC2 instance was in a private subnet with no internet access.
>  To manage it without SSH, we used AWS Systems Manager. Since there
>  was no internet, we created Interface Endpoints for SSM, SSM Messages,
>  and EC2 Messages. We also attached the AmazonSSMManagedInstanceCore
>  IAM role to the EC2 instance. This allowed us to connect to the instance using Session Manager."

---

# 99. Gateway Endpoint Practical Flow

> "First, I created a VPC with public and private subnets. Initially,
>  the private EC2 instance was accessing S3 through a NAT Gateway.
> To avoid internet traffic and reduce NAT costs, I created a Gateway
> VPC Endpoint for S3, associated it with the private route table,
> and updated the S3 bucket policy if required. After that, the private
>  EC2 instance accessed the S3 bucket directly through the AWS network without using the internet."

---

# 100. Security, Logging & Monitoring

**Security**

* SG
* NACL
* IAM
* Private Subnet
* WAF
* RBAC
* VPC Flow Logs

**Logs**

* Terminal
* VPC Flow Logs
* OpenSearch

**Monitoring**

* Prometheus + Grafana

---

