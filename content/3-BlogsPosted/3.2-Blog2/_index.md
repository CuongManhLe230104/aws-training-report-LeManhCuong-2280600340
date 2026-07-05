---
title: "Proactive Infrastructure Monitoring using Ambient Agents on Amazon Bedrock"
date: 2026-06-20
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Proactive AWS Monitoring with Ambient Agents on Amazon Bedrock (AgentWatch)

In managing large-scale cloud infrastructure (Multi-Account/Multi-Region), handling a massive volume of alarms (Alert Fatigue) from Amazon CloudWatch often consumes significant time from operations teams. Traditional rule-based monitoring systems sometimes only detect issues after they have occurred, making it difficult to correlate log and metric data for Root Cause Analysis.

The **AgentWatch** solution provides a continuous **Ambient Agent** model that supports engineers in gathering infrastructure data, analyzing system behavior, and providing Actionable Insights to optimize operational workflows.

---

## 1. Operational Architecture & Human-in-the-Loop (HITL) Mechanism

AgentWatch is designed to work alongside humans through a combination of automation and strict approval workflows (Human-in-the-Loop - HITL), consisting of two main streams:

* **Scheduled Ambient Monitoring:** Triggered periodically every 15 minutes by Amazon EventBridge. A LangChain Agent task integrated with the Claude model on Amazon Bedrock uses dedicated APIs to query CloudWatch metrics, logs, and alarms across multiple AWS accounts. The data is then processed by the LLM, key information is extracted, and reports are sent to the team's Slack channel.
* **On-demand Interaction and HITL Control:** Engineers can query the Agent directly in real-time via Slack Slash Commands (e.g., `/ask Analyze log patterns for the last hour`). The system classifies tasks based on risk level: read-only tasks or trend analysis are processed automatically; while sensitive configuration changes require a 3-step control workflow: Notify, Question, and Review (waiting for human approval).

![Slack Ambient Agent Architecture](/images/week10_agentwatch.png)

---

## 2. Core AWS Services in the Architecture

The solution builds an automated agentic workflow based on the collaboration of Cloud-Native services:

* **Amazon Bedrock & Bedrock AgentCore Runtime:** The platform providing the Foundation Model and secure serverless runtime environment to operate AI Agents at enterprise scale.
* **Amazon EventBridge & AWS Lambda:** Acts as the scheduler and orchestrator for the Agent's workflow.
* **Amazon CloudWatch & AWS STS:** Provides centralized telemetry data and the cross-account assume role mechanism.
* **Amazon API Gateway & Amazon Cognito:** Ensures access control and security (OAuth 2.0) for webhooks from Slack.

---

## 3. Real-World Application Benefits

* **Anomaly Detection Assistance:** The LLM's natural language understanding (NLU) capability helps correlate disjointed signals from system logs and metrics, helping detect anomalies that rule-based systems might miss.
* **Reduced Mean Time to Resolution (MTTR):** The Agent automatically gathers context and conducts initial analysis upon detecting an alert, providing background information to help engineers diagnose issues faster.
* **Governance and Compliance:** Reduces repetitive manual tasks for operations engineers while maintaining human oversight of Production environments through explicit approval steps.

The AgentWatch solution demonstrates the potential of Generative AI (Agentic architecture) in optimizing cloud operations, transforming traditional passive monitoring displays into proactive data analysis assistants.

---

* **Original Blog Link:** [AgentWatch: Proactive AWS monitoring with ambient agents](https://aws.amazon.com/blogs/machine-learning/agentwatch-proactive-aws-monitoring-with-ambient-agents/)