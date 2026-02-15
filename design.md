### design.md: JanSevak Copilot Architecture
1. Executive Summary
JanSevak Copilot is a Serverless Agentic Solution designed for high-availability last-mile governance. By utilizing Amazon Bedrock Agents, the system moves beyond simple information retrieval to Workflow Execution, allowing frontline workers to automate documentation through vernacular voice commands.

2. Well-Architected Pillars Integration
🔒 Security & Privacy (Requirement 8)
Identity & Access: Uses AWS IAM roles for granular service-to-service permissions and Amazon Cognito for worker authentication.

Data Protection: All PII is encrypted at rest and in transit via AWS KMS with customer-managed keys.

Safety Guardrails: Implementation of Guardrails for Amazon Bedrock to redact sensitive PII from logs and prevent model hallucinations or off-topic queries.

📈 Reliability & Performance
Model Selection: Claude 3.5 Sonnet acts as the high-reasoning orchestrator, while Llama 3 handles high-throughput vernacular synthesis.

Resilience: Built on a regional serverless stack to ensure the agent remains available even during high-traffic rural enrollment periods.

💰 Cost Optimization
Inference Efficiency: Uses Provisioned Throughput only for core reasoning, while utilizing serverless on-demand models for lighter translation tasks to minimize costs.

3. High-Level Architecture Diagram
4. Technical Component Deep-Dive
A. The Vernacular Voice Interface
Ingress: Amazon Transcribe provides real-time speech-to-text for major Indian languages.

Egress: Amazon Polly uses Neural TTS to read back form summaries in a natural-sounding vernacular voice.

B. The Agentic Brain (Amazon Bedrock)
Reasoning Engine: Amazon Bedrock Agents orchestrate the "Thought-Action-Observation" loop.

Knowledge Base: A vector store of 500+ government circulars enables the agent to cite official SOPs with zero hallucinations.

C. The Action Layer (AWS Lambda)
Function: Lambda serves as the "Action Group" for the agent.

Logic: When the agent decides to "Fill a Form," the Lambda function executes the API calls to external government portals (e.g., CoWIN or Jan Samarth).

D. Supervisor Dashboard (Amazon Q)
Insight Engine: Amazon Q Business allows district managers to ask, "Why are applications failing in Block X?" and receive a synthesis of agent logs.

5. Deployment Workflow
Input: Worker speaks command in local dialect.

Transcription: Amazon Transcribe converts audio to text.

Inference: Bedrock Agent identifies the "Scheme Intent" using Llama 3.

Retrieval: Claude 3.5 Sonnet fetches correct legal requirements from Bedrock Knowledge Bases.

Execution: Lambda "Form_Filler" prepares the data packet.

Confirmation: Worker confirms via voice; Lambda pushes data to the final API.