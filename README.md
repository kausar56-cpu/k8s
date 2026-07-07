How to login GitHub 

GitHub Enterprise URL उघडतो.
"Sign in with SSO" किंवा "Continue with Okta" वर क्लिक करतो.
Okta login page उघडते.
Company email + password टाकतो.
MFA (Authenticator App) approve करतो.
परत GitHub मध्ये login होतो.
-------------------------------------------

Diagram flow

1. main branch वरून नवीन feature branch तयार कर
        │
        ▼
2. feature branch वर code लिही
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
6. GitHub वर Pull Request तयार कर
   (feature/login → main)
        │
        ▼
7. Team Lead / Reviewer code review करतो
   + CI/CD pipeline (build, test, security checks) चालते
        │
        ▼
8. सर्व checks ✅ Green आणि PR approve
        │
        ▼
9. Merge into main
        │
        ▼
10. Feature branch delete

11. ---------------------------------------



हा Lambda project DevOps interviews मध्ये खूप common आहे. मी तुझ्या notes व्यवस्थित आणि zero level पासून समजावतो.


---

Use Case

Goal: Automatically delete old (stale) EBS snapshots to reduce AWS cost.


---

Step 1: Create Lambda Function

Go to AWS Lambda.

Create Function.

Runtime: Python 3.x


Why? Lambda lets us run code without managing servers.


---

Step 2: Write Python Code

Inside Lambda, write Python code.

Python uses boto3.

What is boto3?

Interview Answer:

> Boto3 is the AWS SDK for Python. It allows Python code to communicate with AWS services using AWS APIs.



Example:

import boto3

This means your Python code can now talk to AWS services like EC2, S3, IAM, EBS, etc.


---

Step 3: Talk to AWS API

Suppose we want EBS snapshots.

Lambda calls

AWS API

↓

EC2 Service

↓

DescribeSnapshots API

AWS returns

Snapshot 1

Snapshot 2

Snapshot 3


---

Step 4: Filter Stale Snapshots

Python checks

Is snapshot old?

Is it unused?

If Yes

↓

Delete it.

This reduces storage cost.


---

Step 5: IAM Role

Lambda needs permission.

Create IAM Role

Attach

AWSLambdaBasicExecutionRole

and custom policy

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeSnapshots",
        "ec2:DeleteSnapshot"
      ],
      "Resource": "*"
    }
  ]
}

Why?

Without IAM permissions,

Lambda cannot

Describe Snapshots

Delete Snapshots



---

Step 6: Trigger Lambda

Instead of manually clicking Run,

CloudWatch (Amazon EventBridge Scheduler) triggers Lambda automatically.

Example

Every day at 12 AM

CloudWatch

↓

Lambda

↓

Python Code

↓

boto3

↓

AWS API

↓

Describe Snapshots

↓

Delete Old Snapshots


---

Complete Flow

CloudWatch Schedule

        ↓

Lambda Function

        ↓

Python Code

        ↓

boto3

        ↓

AWS API

        ↓

Describe EBS Snapshots

        ↓

Find Old Snapshots

        ↓

Delete Old Snapshots

        ↓

AWS Cost Reduced


---

Default Execution Time

By default,

3 Seconds

If needed,

we can increase it up to 15 minutes in the Lambda configuration.


---

Interview Answer

> "I created a Lambda function using Python. Inside the function, I used the boto3 library to communicate with AWS APIs. The Lambda function fetches all EBS snapshots using the DescribeSnapshots API, filters stale or unused snapshots, and deletes them using the DeleteSnapshot API. I attached an IAM role with the required permissions and configured an EventBridge (CloudWatch) schedule to trigger the Lambda function automatically every day. This helps optimize AWS storage costs by removing unused snapshots."



Easy way to remember

CloudWatch → Lambda → Python → boto3 → AWS API → EBS Snapshots → Delete Old Snapshots → Save Cost
