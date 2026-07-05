---
title: "Secure Database Credentials for AWS Lambda with AWS Secrets Manager"
date: 2026-06-15
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# How to Securely Provide Database Credentials to Lambda Functions by Using AWS Secrets Manager

During the development of Serverless applications, one of the biggest challenges is how to store and pass database credentials to AWS Lambda functions securely. Hardcoding passwords in source code or passing them through environment variables always poses a high risk of leaking sensitive information.

Using **AWS Secrets Manager** eliminates these risks by centrally storing database credentials and allowing Lambda functions to query them dynamically when connecting to Amazon RDS (MySQL).

---

## 1. Solution Operation Model

The process of securely handling connection requests from a client to a backend database includes the following steps:

1. The **Client** sends a Request to the RESTful API hosted on **AWS API Gateway**.
2. **API Gateway** executes the corresponding **AWS Lambda** function.
3. The **Lambda** function calls the **AWS Secrets Manager** API to retrieve database credentials (username/password).
4. The **Lambda** function uses that information to connect, query the **Amazon RDS (MySQL)** database, and return results.

![AWS Secrets Manager Database Rotation](/images/week9_secretsmanager.png)

---

## 2. Deployment Process via CloudFormation

To automate and manage infrastructure as code (IaC), the post provides an AWS CloudFormation template to quickly initialize:

* An **Amazon RDS MySQL** database (instance type `db.t3.micro`).
* Two **Lambda** functions:
  * `LambdaRDSCFNInit`: Used to initialize the `Employees` table and insert sample data immediately after stack initialization.
  * `LambdaRDSTest`: Used to query the employee count for testing.
* A **RESTful API Gateway** with a `GET` method.
* A **Secret** resource in Secrets Manager containing a randomly generated password.

---

## 3. Key Technical Takeaways

* **Dynamic References:** CloudFormation uses dynamic references to retrieve the password directly from Secrets Manager when creating the RDS instance. This ensures that the password is never logged or stored in plain text in config files.
* **Automatic Rotation:** Configuring the `AWS::SecretsManager::RotationSchedule` resource in coordination with a rotation Lambda function to automatically change the RDS database password every **30 days**, minimizing risks if credentials are leaked.

Combining Lambda with AWS Secrets Manager helps enterprises automate the lifecycle of sensitive credentials, reduce overhead costs of maintaining separate security infrastructure, and significantly enhance the security level of Serverless applications.

---

* **Original Blog Link:** [How to securely provide database credentials to Lambda functions by using AWS Secrets Manager](https://aws.amazon.com/blogs/security/how-to-securely-provide-database-credentials-to-lambda-functions-by-using-aws-secrets-manager/)