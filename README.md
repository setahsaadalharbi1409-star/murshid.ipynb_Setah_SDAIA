@@ -1 +1,265 @@
# murshid.ipynb_Setah_SDAIA
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:102A43,50:087E8B,100:36C9A3&height=190&section=header&text=MURSHID&fontSize=65&fontColor=FFFFFF&animation=fadeIn&fontAlignY=40" width="100%" alt="MURSHID banner" />

MURSHID | مرشد

A Safe, Context-Aware Service Assistant

Reliable answers. Controlled access. Measurable behavior.

Python
Colab
LLM
SDAIA Academy
Status

SDA-AIE-213 · LLM Application Engineering · SDAIA Academy

Prepared by Setah Saad

</div>

📌 Project at a Glance

<div align="center">

Roadmap
Cells
Tests
Data

</div>

|🛡️ Safety    |🔐 Access control|⚡ Efficiency|🧪 Reliability|
|:----------:|:--------------:|:----------:|:-----------:|
|Input guards|Ownership checks|Public cache|Golden cases |

Overview · Architecture · Workflow · Roadmap · Evaluation

01 | Project Overview

Murshid is an educational service-assistant prototype designed to answer known service questions, retrieve application status through an authorized read-only tool, and reject unsuitable or unsupported requests.

The project explores how to engineer reliable LLM-style applications using structured responses, controlled tool access, guardrails, evaluation, and safe caching. The core implementation follows a mock-client approach using synthetic data rather than a production LLM or a live customer database.

02 | Problem & Solution

|Challenge                                 |Murshid’s design approach                            |
|------------------------------------------|-----------------------------------------------------|
|Unsupported or off-topic questions        |Restrict responses to supported service information  |
|Unauthorized access to application records|Validate requests and verify ownership               |
|Inconsistent responses                    |Use a defined response contract and versioned prompts|
|Repeated public questions                 |Reuse eligible answers through exact-match caching   |
|Unexpected behavior after changes         |Use golden cases and regression testing              |

03 | Key Features

● Grounded service answers: respond using a synthetic service directory.

● Structured responses: follow a defined response contract.

● Authorized status lookup: validate tickets and check ownership before returning status.

● Guardrails: reject unsuitable inputs and unsupported requests.

● Prompt versioning: maintain a versioned prompt artifact.

● Evaluation: use ten golden cases and regression checks.

● Safe caching: cache eligible public answers only, not private application-status responses.

These features describe the course project scope; implementation and test completion are to be verified against the final notebook.

04 | System Architecture

The following conceptual diagram illustrates the intended components and access boundaries.

```mermaid
flowchart TD
    U[User request] --> G[Input guards]
    G -->|Rejected| R[Safe rejection]
    G -->|Accepted| P[Assistant pipeline]
    V[Versioned prompt] --> P
    P --> M[Mock client and response contract]
    M --> D[Synthetic service directory]
    M --> T[Read-only status tool]
    T --> A[Ticket validation and ownership check]
    A --> S[Synthetic application records]
    P <--> C[Public exact-match cache]
    P --> O[Structured response]
    E[Golden cases and regression tests] -.-> P
    classDef input fill:#DBEAFE,stroke:#2563EB,color:#172554,stroke-width:2px;
    classDef core fill:#CCFBF1,stroke:#0D9488,color:#134E4A,stroke-width:2px;
    classDef safety fill:#FEF3C7,stroke:#D97706,color:#78350F,stroke-width:2px;
    classDef reject fill:#FEE2E2,stroke:#DC2626,color:#7F1D1D,stroke-width:2px;
    classDef data fill:#EDE9FE,stroke:#7C3AED,color:#3B0764,stroke-width:2px;
    class U,O input;
    class P,M core;
    class G,T,A safety;
    class R reject;
    class V,D,S,C,E data;
```

05 | Request Workflow

```mermaid
flowchart TD
    A[Receive question] --> B{Suitable input?}
    B -->|No| X[Reject safely]
    B -->|Yes| C{Request type}
    C -->|Public service question| D{Eligible cache hit?}
    D -->|Yes| E[Return cached public answer]
    D -->|No| F[Find supported service answer]
    F --> G[Return answer and cache if eligible]
    C -->|Application status| H{Valid ticket and ownership?}
    H -->|Yes| I[Read status and return without public caching]
    H -->|No| J[Deny access]
    C -->|Unsupported| X
    classDef input fill:#DBEAFE,stroke:#2563EB,color:#172554,stroke-width:2px;
    classDef core fill:#CCFBF1,stroke:#0D9488,color:#134E4A,stroke-width:2px;
    classDef safety fill:#FEF3C7,stroke:#D97706,color:#78350F,stroke-width:2px;
    classDef reject fill:#FEE2E2,stroke:#DC2626,color:#7F1D1D,stroke-width:2px;
    classDef data fill:#EDE9FE,stroke:#7C3AED,color:#3B0764,stroke-width:2px;
    class A,E,G,I input;
    class C,F core;
    class B,D,H safety;
    class X,J reject;
```

> The diagrams are conceptual, not a verified trace of the final notebook’s execution order.

06 | Technology Stack

|Technology / concept|Role                                     |
|--------------------|-----------------------------------------|
|Python 3            |Core application logic                   |
|Google Colab        |Development and execution environment    |
|Mock client         |Simulated model behavior                 |
|JSON                |Structured artifacts and result export   |
|Mermaid             |Architecture and workflow documentation  |
|GitHub              |Project documentation and version control|

The core course project uses a CPU runtime and requires no additional installation. Real-model exercises are separate optional extensions.

07 | Development Roadmap

|Phase|Focus                                                      |Notebook cells|
|-----|-----------------------------------------------------------|--------------|
|Day 1|Synthetic directory, mock client, `ask`, response contract |1–3           |
|Day 2|Ticket validation, read-only status lookup, ownership check|4–6           |
|Day 3|Versioned prompt, guards, pipeline, ten golden cases       |7–10          |
|Day 4|Public exact cache, measurements, regression, export       |11–14         |

```mermaid
flowchart LR
    A[01 Foundations] --> B[02 Structure and tools]
    B --> C[03 Guard and test]
    C --> D[04 Measure and finish]
    classDef input fill:#DBEAFE,stroke:#2563EB,color:#172554,stroke-width:2px;
    classDef core fill:#CCFBF1,stroke:#0D9488,color:#134E4A,stroke-width:2px;
    classDef safety fill:#FEF3C7,stroke:#D97706,color:#78350F,stroke-width:2px;
    classDef reject fill:#FEE2E2,stroke:#DC2626,color:#7F1D1D,stroke-width:2px;
    classDef data fill:#EDE9FE,stroke:#7C3AED,color:#3B0764,stroke-width:2px;
    class A input;
    class B core;
    class C safety;
    class D data;
```

📊 Planned notebook structure

```mermaid
pie showData
    title Planned notebook cells by phase (14 total)
    "Day 1 - Foundations" : 3
    "Day 2 - Structure and tools" : 3
    "Day 3 - Guard and test" : 4
    "Day 4 - Measure and finish" : 4
```

The chart shows the course’s planned cell allocation, not implementation progress or measured performance.

08 | Getting Started

1. Open the project’s cumulative .ipynb notebook in Google Colab.

2. Select a Python 3 CPU runtime (no accelerator).

3. Run the notebook cells in order, from the foundations through the final evaluation.

4. Inspect the responses, test outcomes, measurements, and exported artifacts.

The final notebook filename and direct link will be added after upload.

09 | Example Scenarios

Illustrative scenarios, not recorded execution outputs:

|Scenario                                     |Expected behavior                     |
|---------------------------------------------|--------------------------------------|
|Ask a supported service question             |Return a grounded service answer      |
|Ask for the status of an owned application   |Return the authorized status          |
|Request another user’s application status    |Deny access                           |
|Submit an unsuitable or out-of-scope question|Reject safely                         |
|Repeat an eligible public question           |Reuse the cached answer when available|

10 | Evaluation & Results

|Evaluation area       |Measurement / evidence                |Result              |
|----------------------|--------------------------------------|--------------------|
|Functional correctness|Ten golden cases                      |Pending verification|
|Access control        |Ownership and ticket-validation checks|Pending verification|
|Safety                |Unsuitable-input rejection checks     |Pending verification|
|Performance           |Response timing and cache measurements|Pending verification|
|Regression            |Re-run tests after changes            |Pending verification|

Evaluation coverage map

```mermaid
flowchart TD
    A([Evaluation plan]) --> B[Functional correctness]
    A --> C[Access control]
    A --> D[Input safety]
    A --> E[Timing and caching]
    A --> F[Regression checks]
    classDef root fill:#102A43,stroke:#087E8B,color:#FFFFFF,stroke-width:2px;
    classDef test fill:#DBEAFE,stroke:#2563EB,color:#172554,stroke-width:2px;
    classDef safe fill:#CCFBF1,stroke:#0D9488,color:#134E4A,stroke-width:2px;
    class A root;
    class B,E,F test;
    class C,D safe;
```

No measured scores or performance improvements are claimed until the final notebook has been executed and its results reviewed.

11 | Future Improvements

● Integrate a real language model and compare its behavior with the mock client.

● Expand evaluation coverage for ambiguous and adversarial requests.

● Explore Arabic and English service interactions.

● Add a user-facing interface and more detailed observability.

These are proposed extensions, not completed features.

12 | Acknowledgments

Developed by Setah Saad as a learner project for the LLM Application Engineering Program (SDA-AIE-213) at SDAIA Academy, based on the guided four-day course by Meaad Al-Marri.

Special thanks to SDAIA Academy and Meaad Al-Marri for their guidance and support throughout this learning journey.

Official academy GitHub: @SDAIAAcademy

Original course repository

<div align="center">

MURSHID | Engineering reliable AI-style service experiences.

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:102A43,50:087E8B,100:36C9A3&height=100&section=footer" width="100%" alt="Decorative footer" />

</div>
