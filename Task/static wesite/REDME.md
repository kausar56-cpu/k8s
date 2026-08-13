हो, समजलं. तुम्हाला **interview theory नाही**, तर **AWS Console मध्ये खरंच काय-काय click करून setup करायचा** तो practical task हवा आहे.

तुमच्या **Java/Spring Boot banking application** साठी एक छोटा practical task:

## Practical: Java App + ALB + CloudFront

### Step 1 — Java application EKS वर चालू करा

तुमच्याकडे already:

```text
Spring Boot
   ↓
Docker
   ↓
ECR
   ↓
EKS
```

असणे अपेक्षित आहे.

EKS मध्ये application expose करा:

```text
Internet
   ↓
ALB
   ↓
EKS Service
   ↓
Java Pod
```

Browser मधून ALB URL उघडून application चालतेय हे first verify करा.

---

### Step 2 — CloudFront Create करा

AWS Console मध्ये:

**CloudFront → Distributions → Create distribution**

**Origin domain** मध्ये तुमचा **ALB DNS name** select करा.

Example:

```text
my-banking-alb-123456.ap-south-1.elb.amazonaws.com
```

Origin protocol:

```text
HTTPS only
```

---

### Step 3 — Default Cache Behavior

CloudFront मध्ये:

```text
Viewer protocol policy:
Redirect HTTP to HTTPS
```

Allowed methods:

```text
GET
HEAD
OPTIONS
PUT
POST
PATCH
DELETE
```

Banking application असल्यामुळे API methods लागतील.

**Cache policy:** Dynamic APIs साठी caching avoid करा.

---

### Step 4 — API caching बंद करा

उदा. तुमच्या application मध्ये:

```text
/api/login
/api/account
/api/payment
/api/transaction
```

या requests CloudFront ने cache करू नयेत.

CloudFront मध्ये cache policy अशी configure करा की dynamic API responses cache होणार नाहीत.

---

### Step 5 — ACM Certificate

**AWS Certificate Manager → Request certificate**

Domain:

```text
banking.example.com
```

Certificate issue झाल्यावर CloudFront distribution मध्ये certificate attach करा.

> CloudFront साठी ACM certificate **us-east-1 (N. Virginia)** मध्ये असणे आवश्यक आहे.

---

### Step 6 — Route 53

Route 53 → Hosted Zone:

```text
example.com
```

Record create:

```text
Name: banking
Type: A
Alias: Yes
Target: CloudFront Distribution
```

मग:

```text
https://banking.example.com
```

CloudFront कडे जाईल.

---

### Step 7 — Final testing

Browser:

```text
https://banking.example.com
```

Request flow:

```text
User
 ↓
Route 53
 ↓
CloudFront
 ↓
ALB
 ↓
EKS
 ↓
Spring Boot
```

Login test करा:

```text
POST /api/login
```

Account test:

```text
GET /api/account
```

Payment:

```text
POST /api/payment
```

हे requests **CloudFront → ALB → EKS → Java** पर्यंत जातील.

---

### Interview मध्ये practical action सांगायचा असेल तर

> **“First I deployed my Spring Boot Docker image on EKS and exposed it through an ALB. Then I created a CloudFront distribution and configured the ALB as the origin. I configured HTTPS and disabled caching for dynamic banking APIs. Then I created an ACM certificate and configured Route 53 to point my banking domain to CloudFront. Finally, I tested login, account and payment APIs through the CloudFront URL.”**

**हा actual hands-on task आहे — S3/React वाला static website नाही.**
