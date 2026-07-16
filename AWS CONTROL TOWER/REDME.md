AWS Control Tower
        │
        ▼
AWS Landing Zone
        │
        ▼
AWS Organizations
        │
        ▼
Organizational Units (OUs)
        │
        ├── Security OU
        │      ├── Audit Account
        │      └── Log Archive Account
        │
        ├── Infrastructure OU
        │      ├── Shared Services Account
        │      └── Networking Account
        │
        └── Workloads OU
               ├── Dev Account
               ├── UAT Account
               └── Prod Account
               ----------------------------------------------------------------

               In our company, we don't use the root user to log in to AWS accounts.
               We use AWS SSO (IAM Identity Center). If I need access to a particular account, 
               like the UAT account, I raise a request to the Cloud Admin. The admin gives me
               access to that account. Then I log in using the company's SSO portal with my
               office email and password. After login, I can see the accounts assigned to me.
               I simply click on the required account, and the AWS Console opens."



               AWS Landing Zone is a ready-to-use AWS environment.
               Before deploying applications, we set up security, networking, IAM, logging, 
               and multiple AWS accounts. This gives all teams a secure and standardized 
               environment to work in. That's what we call an AWS Landing Zone."

    

