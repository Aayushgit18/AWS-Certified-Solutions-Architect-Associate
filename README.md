# AWS-Certified-Solutions-Architect-Associate
Perfect 🔥
Let’s convert this into **SAA-C03 Exam Weapon Notes**.

This topic is foundational and AWS LOVES asking questions about Regions, AZs, and Global Services.

---

# 🎯 AWS Global Infrastructure – Exam-Focused Notes

---

## 🧠 1️⃣ What The Exam REALLY Tests Here

The exam does NOT test:

* Exact revenue numbers
* Market share %
* Gartner ranking

The exam DOES test:

* Region vs AZ difference
* Global vs Regional services
* How to choose a region
* High availability across AZ
* Edge locations use cases
* Disaster isolation logic

---

# 🌍 Regions

## 🔹 Definition (Exam-Ready)

A **Region** =

> A cluster of multiple Availability Zones (AZs) in a specific geographic area.

Examples:

* `us-east-1`
* `eu-west-3`
* `ap-southeast-2`

---

## 🧠 Exam Key Points

* Most AWS services are **region-scoped**
* Resources in one region are NOT automatically available in another
* You must deploy separately per region
* Data does NOT replicate automatically across regions

---

## ❓ How to Choose a Region (Exam Favorite Question)

When question says:

### 1️⃣ Compliance Requirement

> “Data must stay in Germany”

✅ Choose region inside that country.

---

### 2️⃣ Low Latency for Users

> “Users are in California”

✅ Choose closest region (us-west)

---

### 3️⃣ Service Availability

> “Application requires XYZ service”

✅ Verify region supports that service.

---

### 4️⃣ Cost Optimization

> “Minimize infrastructure cost”

✅ Compare pricing per region.

---

## 🧨 Common Trap

❌ Thinking AWS automatically moves your data globally.
It does NOT. Regions are isolated.

---

# 🏢 Availability Zones (AZ)

## 🔹 Definition

An **Availability Zone (AZ)** =

> One or more discrete data centers within a region, isolated from each other.

Each region usually has:

* Minimum: 3 AZs
* Maximum: 6 AZs

Example:
ap-southeast-2a
ap-southeast-2b
ap-southeast-2c

---

## 🧠 Exam Key Concepts

* AZs are physically separate
* Each AZ has independent:

  * Power
  * Networking
  * Cooling
* AZs are connected via **high-bandwidth, low-latency** network

---

## 🔥 Exam Scenario Pattern

> “Application must survive a data center failure.”

Correct answer:
✅ Deploy across multiple AZs (Multi-AZ)

NOT:
❌ Deploy in multiple regions (too much unless required)

---

## 🚨 Important Difference

| Feature          | Multi-AZ   | Multi-Region   |
| ---------------- | ---------- | -------------- |
| Protects against | AZ failure | Region failure |
| Cost             | Lower      | Higher         |
| Latency          | Low        | Higher         |

Exam LOVES this difference.

---

# 🌎 Edge Locations / Points of Presence (PoP)

* 400+ PoPs
* Used for:

  * CloudFront
  * Global Accelerator
  * Route 53
  * WAF

---

## 🎯 What Edge Locations Do

They:

* Cache content closer to users
* Reduce latency
* Improve global delivery

---

## 🧨 Exam Trap

Edge locations are NOT:

* Regions
* AZs
* Data centers for EC2

They are for content delivery.

---

# 🌐 Global vs Regional Services (VERY IMPORTANT)

## 🌍 Global Services

These are NOT region-specific:

* IAM
* Route 53
* CloudFront
* WAF

---

## 📍 Regional Services

Most services are regional:

* EC2
* RDS
* Lambda
* Rekognition
* EBS
* ECS
* EKS

---

## 🧨 Exam Trick Question

> “You created an EC2 in us-east-1 but cannot see it in us-west-2”

Why?

✅ EC2 is regional.

---

# 🧠 Architecture Insight (Exam Gold)

AWS design principle:

* Regions = Fault Isolation
* AZs = High Availability
* Edge = Low Latency

If question says:

* Disaster recovery across continents → Multi-Region
* High availability → Multi-AZ
* Faster content delivery → Edge Location / CloudFront

---

# 🧨 Practice Exam-Style Questions

---

### Question 1

A company requires its application to remain available if a single data center fails.

What should they do?

A) Deploy to multiple regions
B) Deploy to multiple AZs
C) Use CloudFront
D) Use IAM

✅ Answer: B

---

### Question 2

A company wants lowest latency delivery for static content worldwide.

What should they use?

A) EC2 Auto Scaling
B) Multi-AZ
C) CloudFront
D) S3 Versioning

✅ Answer: C

---

### Question 3

An organization must ensure data remains inside France.

What should they do?

A) Deploy in eu-west-3
B) Deploy in us-east-1
C) Use CloudFront
D) Use Multi-AZ

✅ Answer: A

---

# 📌 Memorize This (High Yield)

* Regions = Geographic area
* AZs = Data center isolation
* Edge Locations = Content delivery
* IAM = Global
* EC2 = Regional
* Multi-AZ ≠ Multi-Region
* Most services are regional

---

# 🔥 Real-World vs Exam

Real world:

* You might use multi-region less often due to cost.

Exam world:

* If question emphasizes disaster recovery across continents → Multi-Region.

Exam prefers:

> Fully managed, highly available, fault tolerant, least operational overhead.

---

# 🏁 Final Takeaway

This topic looks simple, but:

AWS SAA uses it in:

* 5–8 questions indirectly
* Especially in HA/DR questions

Mastering this = easier elimination of wrong answers.

---

__________________________________________________________________________________________

Excellent 👏🔥
This is a **very high-weight topic** for SAA-C03. IAM questions are everywhere.

From now, I’ll follow your requested structure exactly.

---

# 🏷 Topic Name: IAM Users, Groups & IAM Policies (Deep Dive)

---

# 🧠 1️⃣ Explanation in Details (Concept Clarity Mode)

---

## 🔐 Why IAM Exists

IAM (Identity and Access Management) controls:

> Who can access AWS
> What they can do
> Which resources they can access

Without IAM, anyone could:

* Launch thousands of EC2 instances 💸
* Delete production databases ❌
* Exfiltrate sensitive data 🔓

So AWS enforces strict permission control.

---

# 👤 IAM Users

An IAM User represents:

> One person or application needing access to AWS.

Example:

* Alice → Developer
* Bob → Developer
* David → Operations

Each user:

* Has credentials
* Can log into AWS Console
* Can use CLI/API

---

# 👥 IAM Groups

A Group is:

> A collection of users with shared permissions.

Important Rules:

* Groups can only contain USERS.
* Groups CANNOT contain other groups.
* A user can belong to multiple groups.
* A user can belong to no group (not best practice).

Example:

Developers Group:

* Alice
* Bob
* Charles

Operations Group:

* David
* Edward

Audit Group:

* Charles
* David

So Charles inherits permissions from:

* Developers
* Audit

David inherits permissions from:

* Operations
* Audit

This is cumulative permission inheritance.

---

# 📜 IAM Policies

Policies define permissions.

They are JSON documents.

They answer:

> Allow or Deny which Actions on which Resources?

Example:
Allow:

* EC2:DescribeInstances
* ElasticLoadBalancing:Describe
* CloudWatch:Describe

---

# 🏗 IAM Policy Structure (CRITICAL)

IAM policy components:

---

### 1️⃣ Version

Usually:

```
"Version": "2012-10-17"
```

This is NOT a date you need to memorize.
It is the policy language version.

---

### 2️⃣ Statement (Core of Policy)

Each statement includes:

---

### 🔹 Effect

* Allow
* Deny

If Deny exists → Deny overrides Allow.

---

### 🔹 Principal

Who this policy applies to.

* User
* Role
* Account
* Service

Important:
Principal is mostly seen in resource-based policies.

---

### 🔹 Action

List of API operations.

Examples:

* s3:GetObject
* ec2:StartInstances
* dynamodb:PutItem

---

### 🔹 Resource

Which resource the action applies to.

Example:

* Specific S3 bucket
* Specific EC2 instance
* All resources (*)

---

### 🔹 Condition (Optional)

When policy applies.

Example:

* Only from specific IP
* Only if MFA enabled

---

# 🔒 Principle of Least Privilege

AWS best practice:

> Give only permissions required, nothing more.

Not:
AdministratorAccess for everyone.

Because:

* Security risk
* Cost risk
* Compliance issue

---

# 🎯 2️⃣ Exam Perspective Notes (SAA-C03 Mode – Detailed)

---

## 🧠 What The Exam REALLY Tests

The exam tests:

* Permission inheritance logic
* Least privilege design
* Policy structure understanding
* Effect (Allow vs Deny)
* Multi-group permission logic
* Inline vs Attached policies
* Resource-based vs Identity-based policies

---

# ⚠️ High Probability Exam Areas

---

## 🔥 1️⃣ Policy Evaluation Logic

If:
Allow + Deny both exist

👉 Explicit Deny ALWAYS wins.

Very common exam trap.

---

## 🔥 2️⃣ Multiple Group Membership

If a user belongs to 2 groups:

Permissions = Union of all allowed actions.

Unless:
Explicit Deny appears.

---

## 🔥 3️⃣ Inline vs Managed Policy

Inline Policy:

* Attached directly to user/group/role
* One-to-one relationship

Managed Policy:

* Reusable
* Best practice

Exam prefers:
Managed policies over inline (scalability).

---

## 🔥 4️⃣ Least Privilege Design Question

If question says:

> “Developers should only start and stop EC2”

Correct:
Allow ec2:StartInstances + ec2:StopInstances

NOT:
Allow ec2:* (too broad)

---

# 🧪 3️⃣ Practice Exam-Style Questions

---

### Question 1

Alice belongs to Developers group (Allow EC2 FullAccess).
She also has an inline policy that Denies ec2:TerminateInstances.

Can she terminate EC2?

A) Yes
B) No

✅ Answer: B

Because:
Explicit Deny overrides Allow.

---

### Question 2

A company wants to give developers access to S3 but restrict access to only one specific bucket.

What should they do?

A) Allow s3:* on *
B) Allow s3:* on specific bucket ARN
C) Attach AdministratorAccess
D) Create another region

✅ Answer: B

Because:
Least privilege principle.

---

### Question 3

Charles belongs to:

* Developers group (Allow EC2)
* Audit group (Allow CloudTrail)

What permissions does Charles have?

A) Only EC2
B) Only CloudTrail
C) EC2 + CloudTrail
D) None

✅ Answer: C

Permissions accumulate.

---

# 🏗 4️⃣ Architecture Insight (Exam Gold)

---

### Real-World Thinking

In real architecture:

You NEVER:

* Assign policies to individuals manually
* Give broad admin access to everyone

You:

* Create groups per role
* Attach managed policies
* Use roles for services
* Enforce MFA

---

### Exam Mindset

If question mentions:

> “Many users require same permissions”

Answer:
Use Group + Managed Policy

NOT:
Create inline policy per user

---

# 🚨 5️⃣ Exam Scenario Patterns

---

If question says:

> “Developers require same access”

→ Use IAM Group.

---

If question says:

> “Single user needs special permission”

→ Use inline policy (acceptable).

---

If question says:

> “Access should be revoked easily”

→ Use managed policies.

---

If question says:

> “User cannot access resource despite allow”

→ Check for explicit Deny.

---

# 📌 6️⃣ Exam-Ready Memory Sheet

* IAM = Global service
* Groups contain only users
* Users can belong to multiple groups
* Permissions accumulate
* Explicit Deny overrides Allow
* Policy structure:

  * Effect
  * Action
  * Resource
  * Principal
  * Condition
* Least privilege always preferred
* Managed policies scalable
* Inline policies one-to-one

---

# 🔥 DevOps Mapping For You

Think:

IAM User = Developer account
IAM Group = Kubernetes RBAC group
Policy = Role binding

Explicit Deny = NetworkPolicy block

This mapping makes IAM intuitive for you.

---

This topic alone can give 4–6 questions in SAA.

Master this = strong scoring boost.

---

_________________________________________________________________________

Excellent 🔥
This is a **core foundational block** of SAA-C03. EC2 + Security Groups easily appear in 8–12 questions.

As promised, full structured format below.

---

# 🏷 Topic Name: Amazon EC2, Instance Types & Security Groups

---

# 🧠 1️⃣ Explanation in Details (Concept Clarity Mode)

---

# ☁️ What is Amazon EC2?

EC2 = **Elastic Compute Cloud**

It is AWS’s Infrastructure as a Service (IaaS).

Meaning:

> You rent virtual machines (servers) on demand.

Instead of buying physical servers, you:

* Launch
* Configure
* Scale
* Terminate

All within minutes.

---

# 🖥 EC2 Is Not Just “A VM”

EC2 ecosystem includes:

* EC2 Instances (Virtual Machines)
* EBS (Elastic Block Store – network storage)
* Instance Store (hardware-attached storage)
* Elastic Load Balancer (distribute traffic)
* Auto Scaling Groups (automatic scaling)

Understanding EC2 = Understanding how cloud compute works.

---

# ⚙️ What You Choose When Launching EC2

When creating an EC2 instance, you choose:

### 1️⃣ Operating System

* Linux (most common)
* Windows
* macOS

---

### 2️⃣ Compute Power

* vCPU count
* RAM

---

### 3️⃣ Storage Type

#### Network Attached

* EBS
* EFS

#### Hardware Attached

* Instance Store

---

### 4️⃣ Network Settings

* VPC
* Subnet
* Public IP
* Network speed

---

### 5️⃣ Security Group (Firewall)

Controls:

* Inbound traffic
* Outbound traffic

---

### 6️⃣ EC2 User Data (Bootstrapping)

User Data:

* Runs at first launch only
* Executes as root
* Automates setup

Example:

* Install Nginx
* Install Docker
* Pull code from GitHub

The more complex your script → longer boot time.

---

# 🧱 EC2 Instance Types

AWS categorizes instance types by workload optimization.

Naming Convention Example:
m5.2xlarge

Breakdown:

* m = instance class
* 5 = generation
* 2xlarge = size

---

## 🔹 General Purpose (M, T)

Balanced:

* CPU
* Memory
* Network

Example:
t2.micro (free tier)

Used for:

* Web servers
* Small applications
* Code repos

---

## 🔹 Compute Optimized (C series)

High CPU power.

Used for:

* HPC
* Gaming servers
* ML inference
* Batch processing

Example:
c5, c6

---

## 🔹 Memory Optimized (R, X, Z)

High RAM.

Used for:

* In-memory DB
* Redis
* BI systems

R = RAM (easy memory trick)

---

## 🔹 Storage Optimized (I, D, H1)

High disk throughput.

Used for:

* OLTP
* NoSQL DB
* Data warehousing

---

# 🔥 Security Groups (Very Important)

Security Group = Firewall attached to EC2.

They:

* Control traffic at instance level
* Are stateful
* Only contain ALLOW rules
* Are attached to VPC

---

## 🔹 Key Characteristics

* Inbound rules → Incoming traffic
* Outbound rules → Outgoing traffic
* Default:

  * All inbound blocked
  * All outbound allowed
* Can reference:

  * IP ranges
  * Other Security Groups

---

## 🔹 Security Group Referencing

Instead of IP:
You can allow traffic from another Security Group.

This is very common in:

* Load balancer → EC2
* App tier → DB tier

It avoids hardcoding IP addresses.

---

## 🔹 Important Ports

| Port | Purpose       |
| ---- | ------------- |
| 22   | SSH (Linux)   |
| 3389 | RDP (Windows) |
| 80   | HTTP          |
| 443  | HTTPS         |
| 21   | FTP           |

Memorize these.

---

# 🎯 2️⃣ Exam Perspective Notes (SAA-C03 Mode – Detailed)

---

# 🧠 What The Exam REALLY Tests

* Instance type selection logic
* Security Group behavior
* Bootstrapping behavior
* Stateful firewall concept
* Troubleshooting patterns
* SG referencing logic
* Timeout vs connection refused

---

# 🚨 HIGH-YIELD EXAM FACTS

---

## 🔥 1️⃣ Security Groups Are Stateful

If inbound is allowed:
Response is automatically allowed.

No need to configure outbound rule separately.

---

## 🔥 2️⃣ Timeout vs Connection Refused

Timeout:
→ Security Group issue.

Connection refused:
→ App not running.

VERY common exam trap.

---

## 🔥 3️⃣ Security Groups Only Allow

No Deny rule.

If not explicitly allowed → implicitly denied.

---

## 🔥 4️⃣ Security Groups Are Regional

Cannot reuse across regions.

---

## 🔥 5️⃣ EC2 User Data Runs Once

Exam trap:
User Data runs only at first launch.

Not at every reboot.

---

## 🔥 6️⃣ Instance Type Selection Pattern

If question says:

* CPU heavy → Compute optimized
* Memory heavy → Memory optimized
* Balanced → General purpose
* High disk throughput → Storage optimized

---

# 🧪 3️⃣ Practice Exam-Style Questions

---

### Question 1

Users cannot access EC2 website. Browser times out.

Most likely cause?

A) EC2 instance crashed
B) Security Group blocking port 80
C) Wrong instance type
D) No EBS attached

✅ Answer: B

Timeout = SG issue.

---

### Question 2

An application requires high CPU usage for video encoding.

Best instance type?

A) R5
B) C5
C) T2
D) M5

✅ Answer: B

Compute optimized.

---

### Question 3

You want EC2 to install Apache automatically at launch.

What should you use?

A) Security Group
B) Auto Scaling
C) User Data
D) IAM Role

✅ Answer: C

---

### Question 4

Load Balancer should send traffic to EC2 only.

What should Security Group rule reference?

A) IP address
B) VPC ID
C) Load Balancer Security Group
D) Instance ID

✅ Answer: C

---

# 🏗 4️⃣ Architecture Insight (Exam Gold)

---

## Real-World Architecture

You never:

* Allow 0.0.0.0/0 for SSH in production
* Use general purpose for ML workloads
* Hardcode IPs between services

You:

* Use SG referencing
* Use correct instance type
* Separate SSH into its own SG

---

## Exam Mindset

Exam prefers:

* Least privilege
* Managed service
* Security-first design

If question mentions:
“Internal communication between tiers”

→ Use Security Group referencing.

---

# 🚨 5️⃣ Exam Scenario Patterns

---

If question says:

> “Application server cannot talk to DB server”

Check:
DB Security Group inbound rule.

---

If question says:

> “Website not reachable, browser timeout”

Check:
Security Group inbound port 80/443.

---

If question says:

> “High memory usage database”

Choose:
Memory optimized.

---

If question says:

> “High CPU ML training”

Choose:
Compute optimized.

---

If question says:

> “Need automated setup at boot”

Use:
User Data.

---

# 📌 6️⃣ Exam-Ready Memory Sheet

* EC2 = IaaS
* User Data runs once
* SG = Stateful
* SG only allow rules
* Default:

  * Inbound blocked
  * Outbound allowed
* Ports:

  * 22 SSH
  * 3389 RDP
  * 80 HTTP
  * 443 HTTPS
* Compute optimized = C
* Memory optimized = R
* General purpose = M, T

---

# 🧠 DevOps Mapping For You

Security Group = Kubernetes NetworkPolicy (but stateful)

Instance Type = Pod resource requests (CPU/memory sizing)

User Data = Cloud-init script

Load Balancer SG referencing = Service-to-service allowlist

---

This topic alone = ~10% of exam weight indirectly.

Master this = huge confidence boost.

---
_____________________________________________________________________

Excellent 🔥
This is a **very high-weight SAA topic**.
EC2 purchasing questions are common and often tricky.

As requested, full structured breakdown 👇

---

# 🏷 Topic Name: EC2 Instance Purchasing Options (Complete Comparison)

---

# 🧠 1️⃣ Explanation in Details (Concept Clarity Mode)

AWS offers multiple pricing models because:

> Different workloads require different cost optimization strategies.

Let’s break each one clearly and deeply.

---

# 1️⃣ On-Demand Instances

### 🔹 What It Is

* Pay per second (Linux/Windows)
* No commitment
* No upfront payment

### 🔹 When To Use

* Short-term workloads
* Unpredictable traffic
* Testing environments
* New applications

### 🔹 Characteristics

* Highest cost
* Maximum flexibility
* No risk

Think:

> “Hotel booking for one night.”

---

# 2️⃣ Reserved Instances (RI)

### 🔹 What It Is

Commit to:

* 1 year OR 3 years
* Specific instance attributes:

  * Instance type
  * Region
  * OS
  * Tenancy

### 🔹 Discount

Up to ~72%

### 🔹 Best For

* Steady workloads
* Databases
* Long-running backend services

### 🔹 Scope Options

* Regional
* Zonal (reserves capacity in AZ)

### 🔹 Payment Options

* No upfront
* Partial upfront
* All upfront (max discount)

---

## Convertible Reserved Instances

More flexible:

* Can change instance family
* Can change OS
* Can change tenancy

But:

* Slightly less discount (~66%)

---

# 3️⃣ Savings Plans (Modern Replacement for RIs)

### 🔹 What It Is

Commit to:

> “I will spend $X per hour for 1 or 3 years.”

Not tied strictly to instance type.

### 🔹 Flexibility

Can change:

* Instance size
* OS
* Tenancy

Locked to:

* Instance family
* Region

### 🔹 Discount

Up to ~70%

### 🔹 Best For

* Long-term workloads
* Growing applications
* Flexible architecture

Think:

> “I commit to spend $300/month at hotel, but I can change room type.”

---

# 4️⃣ Spot Instances

### 🔹 What It Is

Unused AWS capacity sold at huge discount.

### 🔹 Discount

Up to 90%

### 🔹 Risk

Can be terminated ANY TIME.

2-minute warning before termination.

### 🔹 Best For

* Batch jobs
* Big data processing
* Image rendering
* Machine learning training
* Non-critical workloads

### 🔹 NOT For

* Databases
* Critical production apps
* Stateful applications

Think:

> “Last-minute hotel discount — but you may get kicked out.”

---

# 5️⃣ Dedicated Hosts

### 🔹 What It Is

You get entire physical server.

### 🔹 Why

* Compliance
* Bring Your Own License (BYOL)
* Per-core licensing model

### 🔹 Most Expensive Option

You control:

* Physical server visibility

---

# 6️⃣ Dedicated Instances

Runs on hardware dedicated to you.

Difference from Host:

* You don’t control physical server.
* No hardware-level visibility.

Less common in exam.

---

# 7️⃣ Capacity Reservations

### 🔹 What It Is

Reserve capacity in a specific AZ.

### 🔹 Key Point

NO DISCOUNT.

You pay on-demand price.

Purpose:
Guarantee capacity availability.

Useful:

* High-demand events
* Critical workloads needing AZ capacity

---

# 🎯 2️⃣ Exam Perspective Notes (SAA-C03 Mode – Detailed)

---

## 🧠 What The Exam REALLY Tests

Not:

* Exact discount percentages

Tests:

* Choosing correct pricing model
* Understanding workload type
* Flexibility vs commitment trade-offs
* Spot suitability
* Capacity reservation purpose

---

# 🔥 Most Common Exam Patterns

---

## 🟢 If Question Says:

> “Long-running steady database for 3 years”

Answer:
Reserved Instance OR Savings Plan.

---

## 🟢 If Question Says:

> “Flexible instance type over time”

Answer:
Convertible RI OR Savings Plan.

---

## 🟢 If Question Says:

> “Batch processing job that can fail”

Answer:
Spot Instances.

---

## 🟢 If Question Says:

> “Guarantee EC2 capacity in specific AZ”

Answer:
Capacity Reservation.

---

## 🟢 If Question Says:

> “BYOL software license per socket”

Answer:
Dedicated Host.

---

# 🚨 Important Exam Trap

Spot Instances are NOT suitable for:

* Databases
* Critical production systems
* Stateful applications

The exam LOVES this trap.

---

# 📊 MASTER COMPARISON TABLE (Long-Term Memory)

| Option               | Commitment      | Discount         | Can Terminate? | Best For                  |
| -------------------- | --------------- | ---------------- | -------------- | ------------------------- |
| On-Demand            | None            | None             | No             | Short-term, unpredictable |
| Reserved             | 1–3 years       | High (~72%)      | No             | Steady workloads          |
| Convertible RI       | 1–3 years       | Medium (~66%)    | No             | Long-term but flexible    |
| Savings Plan         | 1–3 years spend | High (~70%)      | No             | Flexible long-term        |
| Spot                 | None            | Very High (~90%) | YES            | Batch, ML, analytics      |
| Dedicated Host       | Optional        | Moderate         | No             | BYOL, compliance          |
| Dedicated Instance   | Optional        | Low              | No             | Hardware isolation        |
| Capacity Reservation | None            | None             | No             | Guarantee AZ capacity     |

---

# 🧪 3️⃣ Practice Exam-Style Questions

---

### Question 1

A company runs a MySQL database 24/7 for 3 years.

What is MOST cost-effective?

A) Spot
B) On-demand
C) Reserved Instance
D) Dedicated Host

✅ Answer: C

---

### Question 2

A company runs nightly batch image processing jobs that can restart if interrupted.

Best option?

A) On-demand
B) Spot
C) Reserved
D) Dedicated

✅ Answer: B

---

### Question 3

A company must use an existing per-core licensed Oracle software.

Best choice?

A) Spot
B) Dedicated Host
C) Savings Plan
D) Capacity Reservation

✅ Answer: B

---

### Question 4

A company needs guaranteed EC2 capacity in us-east-1a during Black Friday.

Best option?

A) Reserved
B) Spot
C) Capacity Reservation
D) Savings Plan

✅ Answer: C

---

# 🏗 4️⃣ Architecture Insight (Exam Gold)

---

## Real-World Thinking

Most production systems:

* Mix On-Demand + Savings Plan
* Use Spot for non-critical workloads
* Rarely use Dedicated Host unless compliance required

---

## Architect Decision Tree

Ask:

1. Is workload interruptible?
   → Yes → Spot

2. Is workload long-term predictable?
   → Yes → Reserved or Savings Plan

3. Need flexibility?
   → Savings Plan

4. Need physical server control?
   → Dedicated Host

5. Need guaranteed AZ capacity?
   → Capacity Reservation

---

# 🚨 5️⃣ Exam Scenario Pattern Recognition

If question says:

* “Steady-state” → Reserved
* “Flexible” → Savings Plan
* “Interruption tolerant” → Spot
* “Compliance” → Dedicated Host
* “Capacity guarantee” → Capacity Reservation
* “Short-term testing” → On-demand

---

# 📌 6️⃣ Exam-Ready Memory Sheet

* Spot = Cheapest + Risky
* Reserved = Commitment + Discount
* Savings Plan = Spend-based commitment
* Dedicated Host = Physical server
* Capacity Reservation = No discount, only capacity
* Convertible RI = More flexible, less discount
* Spot NEVER for databases
* Savings Plan preferred over RI (modern AWS direction)

---

# 🔥 DevOps Mapping For You

Think:

Spot = Kubernetes spot nodes
Reserved = Reserved worker node capacity
Savings Plan = Cluster-level cost commitment
Dedicated Host = Bare metal control
Capacity Reservation = Pre-booking node capacity

---

This topic alone can appear in 3–5 exam questions.

Master this = easy scoring boost.

---

Send next transcript 👇
We continue building architect-level exam readiness. 🚀

