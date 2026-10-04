# AWS Certified Generative AI Developer – Professional (AIP-C01)

> Free study references, hands-on resources, and legitimate practice-question sources for AWS Certified Generative AI Developer – Professional.

## 1. What is the exam?

**Certification:** AWS Certified Generative AI Developer – Professional  
**Exam code:** AIP-C01

The exam focuses on building, integrating, securing, operating, and evaluating production-grade generative AI applications on AWS.

### Domain weights

| Domain | Weight |
|---|---:|
| Foundation Model Integration, Data Management & Compliance | 31% |
| Implementation & Integration | 26% |
| AI Safety, Security & Governance | 20% |
| Operational Efficiency & Optimization | 12% |
| Testing, Validation & Troubleshooting | 11% |

Official source:

- [AWS Certified Generative AI Developer – Professional](https://aws.amazon.com/certification/certified-generative-ai-developer-professional/)
- [AIP-C01 Official Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/ai-professional-01/ai-professional-01.html)
- [AIP-C01 Technologies and Concepts](https://docs.aws.amazon.com/aws-certification/latest/ai-professional-01/ai-professional-01-technologies-concepts.html)

---

## 2. Free official learning resources

### 2.1 AWS Skill Builder Exam Prep

Start here for exam-oriented preparation.

Use the official exam prep plan to review:

- domain objectives;
- AWS-specific service selection;
- official practice questions;
- architecture trade-offs;
- scenario-style reasoning.

Entry point:

- [AWS Certification: Generative AI Developer – Professional](https://aws.amazon.com/certification/certified-generative-ai-developer-professional/)

Recommended use:

1. Read the official exam guide.
2. Convert every task statement into a checklist.
3. Complete the corresponding Skill Builder domain review.
4. Mark each task as:
   - know;
   - can explain;
   - can implement;
   - can choose correctly in an architecture scenario.

---

## 3. Free hands-on resources

### 3.1 Amazon Bedrock Workshop

Repository:

- [aws-samples/amazon-bedrock-workshop](https://github.com/aws-samples/amazon-bedrock-workshop)

Use it to practice:

- Bedrock model invocation;
- inference APIs;
- prompt handling;
- Knowledge Bases;
- RAG;
- OpenSearch Serverless;
- Agents;
- AgentCore-related workflows;
- IAM-aware integration;
- application deployment.

This should be one of the primary hands-on resources for AIP-C01.

---

### 3.2 Amazon Bedrock Samples

Repository:

- [aws-samples/amazon-bedrock-samples](https://github.com/aws-samples/amazon-bedrock-samples)

Useful areas include:

- prompt engineering;
- foundation-model invocation;
- RAG;
- embeddings;
- agents;
- multimodal applications;
- responsible AI;
- evaluation;
- observability;
- production patterns.

Use this repository as a reference implementation library rather than reading it linearly.

---

### 3.3 Agentic AI on AWS Workshop

Repository:

- [aws-samples/sample-aws-agentic-ai-workshop](https://github.com/aws-samples/sample-aws-agentic-ai-workshop)

Focus areas:

- agents;
- tool use;
- MCP;
- Bedrock Knowledge Bases;
- multi-agent systems;
- AgentCore Memory;
- AgentCore Runtime;
- observability;
- OpenTelemetry;
- CloudWatch.

This is particularly useful for architecture questions involving autonomous workflows and tool integration.

---

### 3.4 AWS GenAI RAG Workshop

Repository:

- [aws-samples/aws-genai-rag-workshop](https://github.com/aws-samples/aws-genai-rag-workshop)

Use it to compare:

- managed RAG;
- custom RAG;
- Bedrock Knowledge Bases;
- OpenSearch-based retrieval;
- retrieval optimization;
- advanced RAG patterns.

Important exam skill:

```text
Requirement
    ↓
Managed Bedrock Knowledge Base?
    ↓
Custom retrieval pipeline?
    ↓
OpenSearch / another retrieval backend?
    ↓
What gives the required control, latency, cost, and operational simplicity?
```

The exam is more likely to test the decision than low-level implementation syntax.

---

### 3.5 Generative AI Evaluation Workshop

Repository:

- [aws-samples/sample-gen-ai-evaluations-workshop](https://github.com/aws-samples/sample-gen-ai-evaluations-workshop)

Focus areas:

- LLM evaluation;
- agent evaluation;
- tool-call evaluation;
- multi-turn evaluation;
- LLM-as-a-Judge;
- red teaming;
- production evaluation;
- observability.

Do not skip evaluation simply because its exam weight is lower. It is also connected to troubleshooting, safety, and production-readiness questions.

---

## 4. Practice questions — legitimate alternatives to exam dumps

Do **not** rely on leaked or recalled live exam questions.

Use legitimate practice-question banks to learn the exam's scenario style and AWS decision-making patterns.

### 4.1 Official AWS Practice Questions

Highest priority.

Use the official question set provided through AWS Skill Builder.

Reason:

- closest wording to the actual AWS certification style;
- teaches how AWS frames architecture constraints;
- good calibration for scenario-based questions.

---

### 4.2 Free full-length practice exam

- [Mastery Exam Prep — AIP-C01 Free Practice Exam](https://masteryexamprep.com/exams/aws/aip-c01/free-practice-exam/)

Use it as a timed mock after completing the main study path.

---

### 4.3 Additional free practice bank

- [CertSafari — AWS Generative AI Developer Professional Practice Questions](https://www.certsafari.com/aws/gen-ai-developer-professional/practice-questions)

Use it as a supplementary question bank.

Do not treat third-party explanations as the source of truth when they conflict with AWS documentation.

---

### 4.4 Additional weighted practice questions

- [ReadRoost — AIP-C01 Practice Questions](https://readroo.st/blog/aip-c01-practice-questions-free)

Useful as another small question set after the official questions.

---

## 5. Community study references

### 5.1 Bilingual Vietnamese / English guide

- [ihatesea69/aws-aip-c01-exam-guide](https://github.com/ihatesea69/aws-aip-c01-exam-guide)

Useful for:

- fast review;
- Vietnamese explanations;
- domain-by-domain study;
- Bedrock, Knowledge Bases, Guardrails, Agents, and CloudWatch review.

Use the official AWS exam guide as the final source of truth.

---

### 5.2 Study notes focused on reasoning

- [vicsz/aip-c01-study-notes](https://github.com/vicsz/aip-c01-study-notes)

Useful for:

- architecture reasoning;
- service-selection trade-offs;
- reviewing common decision patterns;
- avoiding pure memorization.

---

## 6. Recommended study sequence

```text
Official Exam Guide
        ↓
AWS Skill Builder Domain Reviews
        ↓
Official Practice Questions
        ↓
Amazon Bedrock Workshop
        ↓
Amazon Bedrock Samples
        ↓
RAG Workshop
        ↓
Agentic AI / AgentCore Workshop
        ↓
Evaluation Workshop
        ↓
Community Study Notes
        ↓
Third-party Practice Banks
        ↓
Re-read Exam Guide
        ↓
Timed Full Mock
```

### Why this order?

The sequence moves from:

```text
Exam scope
 → AWS concepts
 → implementation
 → architecture trade-offs
 → production concerns
 → exam simulation
```

This reduces the risk of memorizing isolated service facts without understanding when each service should be selected.

---

## 7. Minimum hands-on capability

At minimum, be able to invoke a Bedrock model using the AWS SDK.

```python
import boto3

# Create a client for the Amazon Bedrock Runtime API.
client = boto3.client(
    "bedrock-runtime",
    region_name="us-east-1",
)

response = client.converse(
    # Replace this with a model ID enabled in your AWS account.
    modelId="<your-bedrock-model-id>",

    # Bedrock Converse uses role-based conversational messages.
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "text": "Explain Retrieval-Augmented Generation briefly."
                }
            ],
        }
    ],

    # Inference parameters control response generation.
    inferenceConfig={
        "maxTokens": 300,
        "temperature": 0.2,
    },
)

# Extract the generated text from the response payload.
answer = response["output"]["message"]["content"][0]["text"]

print(answer)
```

But AIP-C01 preparation must go beyond SDK syntax.

A stronger architecture-level capability is understanding:

```text
Client / API
    ↓
Authentication + IAM
    ↓
Application orchestration
    ↓
Bedrock Runtime
    ↓
Guardrails
    ↓
Knowledge Base / Custom Retrieval
    ↓
Foundation Model
    ↓
Evaluation
    ↓
CloudWatch / Tracing
    ↓
Cost + Latency + Reliability Optimization
```

You should be able to explain what each layer does, what can fail, and what AWS service or design choice addresses the requirement.

---

## 8. Important architecture decision patterns

### Frequently changing enterprise knowledge

Prefer:

```text
RAG
```

because the knowledge can be updated independently from the model.

### Need model behavior or style adaptation

Consider:

```text
model customization / fine-tuning
```

depending on the supported Bedrock model and requirement.

### Deterministic business workflow

Prefer explicit orchestration such as:

```text
application workflow
Step Functions
event-driven services
```

rather than introducing autonomous agent behavior unnecessarily.

### Autonomous reasoning and tool invocation

Consider:

```text
Agent
    ↓
Reasoning
    ↓
Tool selection
    ↓
Tool execution
```

### Content-safety enforcement

Consider:

```text
Bedrock Guardrails
```

but do not confuse guardrails with IAM authorization.

### Resource-level authorization

Use:

```text
IAM
resource policies
application authorization
```

The model should not be responsible for deciding whether a user is authorized to access protected data.

---

## 9. Fast-track priority

If time is limited, prioritize:

1. Official Exam Guide
2. AWS Skill Builder Exam Prep
3. Official AWS Practice Questions
4. Amazon Bedrock Workshop
5. Amazon Bedrock Samples
6. RAG architecture
7. Agents / AgentCore
8. IAM, KMS, VPC, CloudWatch, CloudTrail
9. Evaluation and troubleshooting
10. Full timed mock

The objective is not merely to recognize AWS service names.

The target capability is:

> Given a production GenAI requirement, identify the safest, simplest, most operationally appropriate AWS architecture.

---

## 10. Reference index

| Resource | Type | Priority |
|---|---|---:|
| [Official Certification Page](https://aws.amazon.com/certification/certified-generative-ai-developer-professional/) | Official | Highest |
| [Official Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/ai-professional-01/ai-professional-01.html) | Official | Highest |
| [Technologies and Concepts](https://docs.aws.amazon.com/aws-certification/latest/ai-professional-01/ai-professional-01-technologies-concepts.html) | Official | Highest |
| AWS Skill Builder Exam Prep | Official | Highest |
| [Amazon Bedrock Workshop](https://github.com/aws-samples/amazon-bedrock-workshop) | Hands-on | Highest |
| [Amazon Bedrock Samples](https://github.com/aws-samples/amazon-bedrock-samples) | Hands-on / Reference | High |
| [Agentic AI Workshop](https://github.com/aws-samples/sample-aws-agentic-ai-workshop) | Hands-on | High |
| [AWS GenAI RAG Workshop](https://github.com/aws-samples/aws-genai-rag-workshop) | Hands-on | High |
| [GenAI Evaluation Workshop](https://github.com/aws-samples/sample-gen-ai-evaluations-workshop) | Hands-on | High |
| [vicsz AIP-C01 Study Notes](https://github.com/vicsz/aip-c01-study-notes) | Community notes | Medium |
| [Vietnamese / English AIP-C01 Guide](https://github.com/ihatesea69/aws-aip-c01-exam-guide) | Community guide | Medium |
| [Mastery Exam Prep](https://masteryexamprep.com/exams/aws/aip-c01/free-practice-exam/) | Practice | Medium |
| [CertSafari](https://www.certsafari.com/aws/gen-ai-developer-professional/practice-questions) | Practice | Medium |
| [ReadRoost](https://readroo.st/blog/aip-c01-practice-questions-free) | Practice | Medium |

---

## Glossary

| Term | Meaning |
|---|---|
| AIP-C01 | Exam code for AWS Certified Generative AI Developer – Professional |
| FM | Foundation Model |
| RAG | Retrieval-Augmented Generation |
| Amazon Bedrock | AWS managed platform for building generative AI applications with foundation models |
| Bedrock Runtime | Runtime API used to invoke models hosted through Amazon Bedrock |
| Knowledge Bases for Amazon Bedrock | Managed retrieval and RAG capability in Amazon Bedrock |
| Agent | AI component that can reason about a task and invoke tools or actions |
| AgentCore | AWS capabilities for operating production agentic systems |
| Guardrails | Amazon Bedrock controls for applying AI safety policies |
| IAM | Identity and Access Management |
| KMS | Key Management Service |
| OpenSearch Serverless | Managed OpenSearch deployment model commonly used for search and vector workloads |
| CloudWatch | AWS monitoring, logging, metrics, and observability service |
| CloudTrail | AWS API activity and audit logging service |
| SDK | Software Development Kit |
| MCP | Model Context Protocol |
| LLM-as-a-Judge | Evaluation technique where an LLM scores or compares model outputs |
| Practice exam | Legitimate simulated exam questions used for preparation |
| Exam dump | Recalled or leaked live exam questions; not a recommended preparation source |
