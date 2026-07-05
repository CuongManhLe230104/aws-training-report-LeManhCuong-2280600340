---
title: "Understanding VPC Links in Amazon API Gateway Private Integrations"
date: 2026-06-25
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Understanding VPC Links in Amazon API Gateway Private Integrations

When designing and building highly secure API systems, hiding backend services within a private VPC network and not exposing them to the public Internet is a mandatory requirement. A **VPC Link** is a resource in Amazon API Gateway that allows connecting API routes to these private, internal resources securely.

This post dives into the core technologies behind VPC Link (such as AWS Hyperplane and AWS PrivateLink) and compares the fundamental architectural differences between VPC Links for REST APIs and HTTP APIs.

---

## 1. Underlying Technologies

* **AWS Hyperplane:** AWS's high-performance internal network virtualization platform, supporting connection and routing between different VPCs. Hyperplane uses a **VPC-to-VPC NAT** network address translation mechanism instead of PrivateLink.
* **AWS PrivateLink:** Technology that allows accessing AWS services privately within the AWS internal network without going through the public Internet. Traffic is routed via Interface VPC Endpoints (user side) and VPC Endpoint Services (provider side).

---

## 2. Distinguishing Private API and Private Integration

* **Private API:** Means the API Gateway endpoint itself can only be accessed from within the VPC (or via Direct Connect/VPN). Currently, only REST APIs support configuring Private APIs.
* **Private Integration:** Means the backend system (behind the API Gateway) is located within the VPC and completely hidden from the public Internet. API Gateway uses a VPC Link to securely connect to this backend.

---

## 3. Comparing VPC Links for REST APIs vs. HTTP APIs

The first difference lies in the underlying technology. REST API's VPC Link is based on **AWS PrivateLink**, while HTTP API uses the VPC-to-VPC NAT network address translation system of **AWS Hyperplane**. This difference leads to major changes in the underlying architecture:

* **Resources and Integration Capabilities:** HTTP APIs are much more flexible as they do not require a VPC Endpoint Service but can connect directly to ALBs, NLBs, or services registered via AWS Cloud Map; a single VPC Link can also link to multiple different backends. Conversely, REST APIs require a VPC Endpoint Service, connect through a single NLB, and configuring multiple backends is much more complex.
* **Features and IP Addressing:** HTTP APIs leverage the Layer 7 capabilities of ALBs (such as advanced routing, authentication) and operate by tunneling through ENIs. Meanwhile, REST APIs are more limited at Layer 7 since they route through an NLB (Layer 4), and the backend system will identify the source IP as the private IP of that NLB.

![VPC Link HTTP API Architecture](/images/week9_vpclink_http_alb.png)

---

## 4. Conclusion

Understanding the differences between the two types of VPC Links helps solutions architects make accurate decisions when designing systems:
* If you need a cost-effective, high-speed API solution that integrates flexibly with ALBs or containers, **VPC Link for HTTP APIs** is the optimal choice.
* If you require specialized features of REST APIs, you will need to configure **VPC Link via the PrivateLink mechanism with an NLB**.

---

* **Original Blog Link:** [Understanding VPC Links in Amazon API Gateway Private Integrations](https://aws.amazon.com/blogs/compute/understanding-vpc-links-in-amazon-api-gateway-private-integrations/)