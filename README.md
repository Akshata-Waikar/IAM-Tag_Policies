# EC2 Instance Launch with Enforced Tagging Policy Using IAM (Without AWS Organizations)

## 📌 Project Description

This project demonstrates how to enforce mandatory tagging when launching EC2 instances using only AWS IAM policies — without relying on AWS Organizations or Service Control Policies (SCPs). It ensures that instances cannot be launched unless the following tags are provided:

- `Name`
- `emailID`
- `phoneNo`
- `Place`

This approach supports better cost tracking, resource management, and operational governance.

---

## 🎯 Objective

The objective of this project is to enforce mandatory tagging during EC2 instance creation without using AWS Organizations. By applying a custom IAM policy, EC2 launches are denied unless the required tags are provided. The project demonstrates both successful and failed launch scenarios, using only identity-based policies within a single AWS account.

---

## 🧰 Technology Stack

| Component          | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| AWS EC2            | Launch and manage virtual servers.                                          |
| AWS IAM            | Manage users and enforce tagging with custom policies.                      |
| IAM Policy         | JSON-based policy to deny EC2 launches if tags are missing.                 |
| AWS Console        | Used to configure IAM and launch EC2 instances.                             |
| AWS CLI (Optional) | Used to test EC2 launches programmatically.                                 |


---

## ⚙️ Implementation Steps

### Step 1: Create IAM Policy

Create a custom IAM policy with the following JSON to deny EC2 launches if required tags are missing:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyRunInstanceWithoutTags",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "*",
      "Condition": {
        "Null": {
          "aws:RequestTag/Name": "true",
          "aws:RequestTag/emailID": "true",
          "aws:RequestTag/phoneNo": "true",
          "aws:RequestTag/Place": "true"
        }
      }
    }
  ]
}

Step 2: Attach Policies to IAM User
Attach:

✅ AmazonEC2FullAccess

✅ The above custom policy

Step 3: Launch EC2 Instance With Tags (Success Case)
During instance creation, add all required tags

Step 4: Launch EC2 Without Tags (Failure Case)
Skip the tagging step or remove one tag.


✅ Conclusion
This project implemented tag enforcement for EC2 instances using IAM policies, ensuring no instances are launched without required metadata. It provides a lightweight alternative to AWS Organizations for individual users or small teams and promotes disciplined cloud resource management.


Project Completed By : Akshata Waikar
