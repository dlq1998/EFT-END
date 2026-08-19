# 🌿 EFT-Ψ: A Multi-Agent Framework for Generating Emotion-Focused Mental Health Support Dialogues with Progressive Disclosure

[中文](README.md) | [English](README_en.md)

[![Dataset](https://img.shields.io/badge/ModelScope-EFT--END-blue)](https://modelscope.cn/datasets/dlq1998/EFT-END)
[![Model](https://img.shields.io/badge/ModelScope-EFT--Chat-orange)](https://modelscope.cn/models/dlq1998/EFT-Chat)

> **EFT-Ψ → EFT-END → EFT-Chat**

📚 **Dataset:** [EFT-END](https://modelscope.cn/datasets/dlq1998/EFT-END)  
🤗 **Model:** [EFT-Chat](https://modelscope.cn/models/dlq1998/EFT-Chat)

---

## 🌟 Project Overview

Welcome to the **EFT-END** project repository.

Existing LLM-based mental health dialogue generation methods often simulate clients who disclose their psychological difficulties too clearly and too early, while counselors may be provided with excessive prior case information. Such settings make it difficult to reproduce the gradual disclosure, emotional exploration, and information asymmetry commonly observed in real mental health support interactions.

To address these limitations, we propose **EFT-Ψ**, an Emotion-Focused Therapy-oriented, knowledge-driven multi-agent framework for generating multi-turn mental health support dialogues.

EFT-Ψ integrates:

* 🧩 **Structured psychological knowledge** through an Emotion–Need Diagram (END)
* 👤 **Client process modeling** based on emotional awareness and protective resistance
* 🔐 **Information-asymmetric interaction** between clients and counselors
* 🌊 **Progressive disclosure** of latent psychological information
* 🧠 **Dialogue-grounded reconstruction** of the counselor's working psychological understanding
* 🤖 **Multi-agent collaboration** for client simulation, reconstruction, counseling, and disclosure regulation

Based on EFT-Ψ, we construct **EFT-END**, a Chinese multi-turn mental health support dialogue dataset, and further fine-tune a compact open-source model, **EFT-Chat**.

---

## 🧠 EFT-Ψ Framework

EFT-Ψ models mental health support dialogue generation as a process in which latent psychological knowledge is **progressively expressed, observed, and reconstructed through interaction**.

The framework consists of two main stages:

### Stage I: Hidden Case Knowledge Initialization

For each help-seeking case, EFT-Ψ constructs:

* a **Complete Hidden END**, representing structured psychological knowledge related to the client's current difficulty;
* a **Client Process Profile**, describing individual differences in emotional awareness and protective resistance.

These components define the latent case information available to the simulated client while remaining inaccessible to the counselor.

### Stage II: END-Guided Multi-Agent Interaction

During multi-turn interaction, EFT-Ψ maintains three different knowledge states:

* 🔒 **Complete Hidden END** — the complete latent psychological knowledge of the case
* 👤 **Client-Visible END** — psychological information currently available for client expression
* 🧠 **Counselor-Side Working END** — the counselor's evolving understanding reconstructed from observable dialogue

The counselor cannot directly access the Complete Hidden END or Client-Visible END and must gradually form a working psychological understanding from the dialogue evidence that has emerged.

---

## 🧩 Emotion–Need Diagram (END)

The **Emotion–Need Diagram (END)** is a structured representation of psychological knowledge designed according to the emotional processing logic of Emotion-Focused Therapy.

END contains seven components:

* **Presenting Context**
  The main event, relational context, and real-world situation related to the client's difficulty.

* **Surface Narrative**
  The client's direct interpretation, concern, self-evaluation, or understanding of the current situation.

* **Case Material Cues**
  Concrete events, interaction details, behavioral responses, and relational cues that may be progressively disclosed during dialogue.

* **Secondary Emotions**
  Emotional experiences that are relatively accessible and easier for the client to recognize or express.

* **Primary Emotion**
  A possible deeper emotional experience that is more directly connected to the current situation.

* **Unmet Needs**
  Possible psychological or relational needs, such as understanding, safety, responsiveness, respect, or boundaries.

* **Protective Response**
  Self-protective responses such as avoidance, minimization, self-blame, or other strategies that may regulate contact with vulnerable experiences.

> END is designed as a structured working representation for dialogue generation rather than a clinical diagnosis or formal case conceptualization.

---

## 👤 Client Process Modeling

To simulate individual differences in psychological expression and disclosure, EFT-Ψ models the client process along two dimensions.

### Emotional Awareness

Clients are assigned one of three emotional awareness levels:

* **Low**
* **Medium**
* **High**

Different awareness levels regulate how clearly clients can recognize and express their emotional experiences.

### Protective Resistance

Protective resistance contains two levels:

* **Low**
* **Moderate**

Five forms of protective resistance are modeled:

* Minimal Disclosure
* Emotional Avoidance
* Defensive Reframing
* Self-Protective Devaluation
* Hopeless Withdrawal

The client process profile influences **expression clarity, disclosure pace, and protective responses** without changing the underlying case facts represented in END.

---

## 🤖 Multi-Agent Collaboration

EFT-Ψ consists of four specialized agents:

### 👤 Client Agent

The Client Agent generates natural client utterances based on:

* the currently visible END information;
* dialogue history;
* emotional awareness;
* protective resistance;
* interaction progress.

The agent can only express psychological information that has already been made available through the disclosure mechanism.

### 🧠 Reconstruction Agent

The Reconstruction Agent periodically reconstructs a **Working END** based solely on observable dialogue evidence.

Its purpose is to organize psychological information distributed across multiple dialogue turns while avoiding unsupported inferences.

### 💬 Counselor Agent

The Counselor Agent generates EFT-oriented mental health support responses based on:

* observable dialogue history;
* the current Working END;
* EFT-oriented emotional processing functions.

The counselor focuses on concrete experiences that have already emerged in the interaction and avoids premature diagnosis, direct cognitive correction, or unsupported interpretation.

### 🌊 Mediator Agent

The Mediator Agent regulates the progressive disclosure of hidden END information.

It determines when additional psychological information can become available to the Client Agent based primarily on evidence already emerging in the dialogue.

The Mediator does not use the counselor's Working END, preventing counselor-side hypotheses from directly influencing subsequent client disclosure.

---

## 🌊 Progressive Disclosure

A central feature of EFT-Ψ is the explicit modeling of **progressive psychological disclosure**.

```text
Complete Hidden END
        │
        │ Controlled Disclosure
        ▼
Client-Visible END
        │
        │ Natural Expression
        ▼
Observable Dialogue
        │
        │ Dialogue-Grounded Reconstruction
        ▼
Counselor-Side Working END
```

Rather than providing complete psychological information at the beginning of the interaction, EFT-Ψ allows emotional experiences, concrete events, needs, and protective responses to gradually emerge through multi-turn dialogue.

This design creates an information-asymmetric interaction in which the counselor must progressively understand the client from the evidence that has actually been expressed.

---

## 📚 EFT-END Dataset

Based on EFT-Ψ, we construct **EFT-END**, a Chinese multi-turn mental health support dialogue dataset.

### Dataset Statistics

| Statistic                          |              EFT-END |
| ---------------------------------- | -------------------: |
| Dialogues                          |            **9,523** |
| Utterances                         |          **238,062** |
| Average Interaction Turns          |            **12.50** |
| Average Client Utterance Length    | **66.81 characters** |
| Average Counselor Utterance Length | **62.57 characters** |
| Train / Validation / Test Split    |        **8 : 1 : 1** |
| Psychological Concern Categories   |                **9** |

### Psychological Concern Categories

EFT-END covers nine categories of common psychological concerns:

* Interpersonal Relationships
* Marriage
* Family
* Romantic Relationships
* Emotions
* Personal Growth
* Therapy
* Career
* Behavior

The original help-seeking scenarios are derived from **PsyQA**, while the corresponding multi-turn dialogues are generated through the EFT-Ψ framework.

---

## 💬 Dialogue Characteristics

EFT-END is designed to support research on multi-turn mental health dialogue processes involving:

* progressive psychological disclosure;
* emotional awareness and emotional deepening;
* protective resistance;
* information-asymmetric interaction;
* exploration of emotional experiences;
* exploration of psychological and relational needs;
* counselor-side psychological understanding;
* EFT-oriented mental health support.

Compared with conventional direct dialogue generation, EFT-Ψ explicitly constrains the information available to each interaction role and models how latent psychological knowledge gradually becomes observable through conversation.

---

## 📊 Dataset Evaluation

EFT-END is evaluated from both the **client side** and the **counselor side**.

### Client-Side Evaluation

The client-side evaluation focuses on:

* **Authenticity and Progressive Disclosure**
* **Emotional Experience and Processing Depth**
* **Depth of Self-Exploration**

### Counselor-Side Evaluation

The counselor-side evaluation focuses on:

* **Empathy**
* **Active Listening**
* **Problem Understanding and Clarification**
* **Helpfulness**

In professional human evaluation, EFT-END achieved an overall counselor-side quality score of **4.44 / 5**, compared with **3.82** for PsyDT and **3.37** for SimPsyDial.

Its scores for **Active Listening** and **Problem Understanding and Clarification** reached **4.77** and **4.78**, respectively.

---

## 🔬 END Mechanism Evaluation

We additionally evaluate whether the core END mechanism operates as intended through three tasks:

### END-to-Dialogue Expression

Evaluates whether psychological information represented in the Complete Hidden END is naturally expressed throughout the generated dialogue.

### Dialogue-Grounded END Reconstruction

Evaluates whether the counselor-side Working END can form a reasonable psychological understanding based only on observable dialogue evidence.

### END Structural Alignment

Evaluates the degree to which the Working END and Complete Hidden END remain aligned along major psychological dimensions under information asymmetry.

These evaluations examine whether EFT-Ψ can support the intended process of:

> **Latent Psychological Knowledge → Progressive Expression → Dialogue Evidence → Counselor-Side Reconstruction**

---

## 🤗 EFT-Chat

To examine the usefulness of EFT-END for domain-specific model training, we fine-tune **Qwen2.5-7B-Instruct** on EFT-END using supervised fine-tuning with **Low-Rank Adaptation (LoRA)**.

The resulting model is named:

> **EFT-Chat**

EFT-Chat is designed as a compact open-source model specialized for **emotion-focused mental health support**.

The model is evaluated against:

* closed-source general-purpose LLMs;
* open-source general-purpose LLMs;
* domain-specific psychological support models.

Experimental results show that EFT-Chat achieves strong performance in automatic evaluation and is highly competitive in professional human evaluation on core psychological support dimensions including empathy, active listening, and problem understanding and clarification.

---

## 🔓 Open Materials

To support open and reproducible research, this repository provides the core research materials related to EFT-Ψ and EFT-END.

The released materials may include:

* EFT-Ψ framework implementation
* Agent definitions and prompts
* END construction materials
* Client process profile definitions
* Progressive disclosure mechanisms
* EFT-END dataset
* Dataset processing scripts
* Evaluation scripts
* EFT-Chat training and inference configurations

Please refer to the repository directories for the currently available resources.

---

## 📖 Citation

If **EFT-Ψ**, **EFT-END**, **EFT-Chat**, or the related framework and materials are useful for your research, please consider citing our work.

> The formal citation information will be updated after publication.

---

## 🙏 Acknowledgements

This work was supported by:

* **Youth Innovation Talent Project of the Department of Education of Guangdong Province**
  No. **2025KQNCX148**

* **University-Level Research Project of Guangdong University of Foreign Studies South China Business College**

* **Research on Positive Psychological Qualities of College Students from the Perspective of Healthy China: A Case Study of Private Universities in Guangdong Province**
  No. **2024GXJK553**

We sincerely thank all collaborators, annotators, and supporting institutions involved in this research.

---

## ⚠️ Disclaimer

EFT-Ψ, EFT-END, and EFT-Chat are developed primarily for **academic research, education, and research on AI-assisted mental health support**.

* This project focuses on non-clinical mental health support and does **not** constitute psychological diagnosis, psychotherapy, psychiatric treatment, or medical care.
* EFT-END consists of LLM-simulated multi-turn interactions constructed from real help-seeking texts. Although the framework is designed to improve process authenticity, the generated dialogues should not be treated as equivalent to real psychotherapy sessions.
* END is a computational representation used to organize psychological information for dialogue generation and should **not** be interpreted as a clinical diagnosis or formal psychological case conceptualization.
* Outputs generated by EFT-Chat or other models trained on EFT-END may be inaccurate, inappropriate, incomplete, or unsafe in some situations.
* The models and framework **must not replace qualified mental health professionals**.
* The current framework does not provide dedicated mechanisms for professional risk assessment or referral in high-risk situations such as self-harm or suicide.
* Users experiencing severe psychological distress, suicidal ideation, self-harm risk, psychiatric emergencies, or other high-risk situations should seek assistance from qualified professionals and appropriate local services.
* Users must comply with the licenses, terms of service, and usage policies of all underlying language models, datasets, APIs, and third-party dependencies.
* Researchers and developers are responsible for independently assessing privacy, ethics, safety, cultural applicability, and deployment risks when using this project.

At its current stage, this project is intended primarily for **research and technical validation** and should not be directly deployed as an autonomous psychological treatment system.

---

## ⭐ Support

If you find **EFT-Ψ**, **EFT-END**, or **EFT-Chat** useful for your research, please consider giving this repository a **Star ⭐**.

We hope this project can support further research on **multi-agent systems, mental health dialogue generation, progressive disclosure, and computational modeling of psychotherapy processes**.
