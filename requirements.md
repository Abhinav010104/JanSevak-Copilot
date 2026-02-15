# Requirements Document: JanSevak Copilot

## 1. Introduction
JanSevak Copilot is an **Agentic AI System** designed to bridge the last-mile governance gap for India’s 900M rural citizens by empowering 3M+ frontline workers. Unlike standard chatbots, JanSevak Copilot is an **Action-Oriented Assistant** built on Amazon Bedrock that reasons over policy and autonomously executes documentation workflows.

## 2. Target Users & Stakeholders
- **Primary:** ASHA/Anganwadi workers, Panchayat clerks (Vernacular-first users).
- **Secondary:** District Supervisors (Insight-driven users).

## 3. Functional Requirements (EARS Format)

### FR-1: Vernacular Agentic Interaction
- **When** a worker provides voice input in a supported Indian dialect (e.g., Bhojpuri, Marathi, Tamil), **the system shall** use Llama 3 on Bedrock to extract functional intents and entities.
- **When** background noise interferes with transcription, **the system shall** prompt the user for clarification in the same vernacular language.

### FR-2: Autonomous Policy Reasoning (RAG)
- **While** a worker is inquiring about a specific scheme (e.g., PM-Kisan), **the system shall** retrieve the latest official SOP from Amazon Bedrock Knowledge Bases to ensure 100% accuracy.
- **When** a policy query is processed, **the system shall** provide an "Explainability Trail" citing the specific section of the government circular used.

### FR-3: Autonomous Data Synthesis & Form-Filling
- **When** unstructured voice data is collected from a field interview, **the system shall** synthesize it into structured JSON objects ready for API consumption.
- **When** a required field for a government form is missing, **the system shall** autonomously trigger a "Clarification Loop" to ask the worker for the specific missing data point.

### FR-4: Human-in-the-Loop (HITL) Execution
- **Before** any data is pushed to a government API, **the system shall** present a vernacular summary for explicit human confirmation.
- **If** a worker corrects an AI-generated draft, **the system shall** update its session memory and adjust subsequent workflow steps accordingly.

### FR-5: Supervisor Intelligence (Amazon Q)
- **When** a district official queries the system via Amazon Q, **the system shall** generate aggregated, anonymized insights regarding systemic bottlenecks (e.g., "Why are applications failing in Block X?").

## 4. Technical Constraints (The "Win" Factor)
- **Model Choice:** Use **Claude 3.5 Sonnet** for reasoning and **Llama 3** for vernacular synthesis.
- **Architecture:** Must be **Serverless** (AWS Lambda) and **Agent-driven** (Bedrock Agents).
- **Safety:** Use **Guardrails for Amazon Bedrock** to prevent non-governance-related interactions.

## 5. Success Metrics
- 50% reduction in manual data entry errors.
- Support for 12+ Indian languages.
- Successful autonomous mapping of 20+ core government schemes.