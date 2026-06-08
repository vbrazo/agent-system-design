# Introduction to AI Agents

**Overview:** Discover how AI agents differ from traditional AI models by acting autonomously through perception, reasoning, and action. Learn agent types, their evolution from rule-based systems to LLM-powered agents, and when complex, dynamic tasks require agentic system design.

---

The landscape of AI is changing quickly, especially with the rise of large language models (LLMs). Early LLM applications focused on single-turn interactions or basic text generation. AI agents—rooted in earlier rule-based and learning-based systems—have resurged in a new form.

LLM-powered systems are not limited to processing information in isolation. They carry out complex, multi-step tasks on behalf of users, often without explicit instructions at every step.

In this course, we move beyond individual agents to **agentic system design**: how agents are architected and integrated into larger, cohesive systems. Effective design involves deliberate architectural choices and reusable patterns for reliable, scalable, and adaptive solutions. Real-world systems often involve multiple interacting agents, which makes planning, communication, and arbitration fundamental design concerns.

## Learning objectives

By the end of this lesson, you will be able to:

- Define what makes a system an AI agent
- Distinguish between AI models and agents
- Identify different types of agents and their roles
- Understand the evolution from rule-based to LLM-powered agents
- Evaluate when to use an agent instead of a simpler solution

---

## What is an AI agent?

In artificial intelligence, an **agent** is a system that can perceive its environment, make decisions, and act autonomously to achieve specific goals. This **perceive–reason–act** loop is a cornerstone of classical AI theory, notably popularized by Russell and Norvig.

Unlike a passive model that waits for a query and returns output, an AI agent is an **active entity**. It can sense, think, and act on its own, often without continuous human oversight.

### Three fundamental capabilities

1. **Perception** — The agent senses its environment: user text, images, audio, sensors, or database records. The goal is to extract meaningful information from raw input.

2. **Reasoning and planning** — Given what it perceives, the agent decides what to do. LLMs like GPT-4 often power this step. Agents may be **reactive** (respond to immediate stimuli) or **deliberative** (plan multi-step actions before acting).

3. **Action execution** — The agent acts: send a reply, call an API, move a robot, update a database. Actions are grounded in reasoning and aligned with goals.

Autonomy varies—from partial automation with human approval to full independence—depending on task and safety requirements.

### Real-world analogies

**Simple:** A smart-home assistant hears *"Remind me to call mom at 6 PM."* It parses speech (perception), understands a timed reminder (reasoning), and schedules an alarm (action).

**Complex:** A travel concierge sees your Berlin flight was cancelled (perception), reasons you must still arrive tonight, searches alternatives, books a combo, and messages your hotel (multi-step plan and action).

### Key characteristics

| Feature | Description |
|---------|-------------|
| **Autonomy** | Acts independently, initiating actions without continuous human intervention |
| **Goal-oriented behavior** | Directs actions toward predefined objectives, not isolated outputs |
| **Perception and feedback loop** | Observes the environment and adjusts based on outcomes or new information |
| **Continuity** | Maintains memory or context over time for multi-turn reasoning |
| **Flexibility** | Revises plans when objectives or context change, supported by perception, memory, and planning |

This view aligns with biological intelligence: not just recognizing patterns, but using insight to take meaningful action.

---

## AI models vs. AI agents

A common confusion in system design is the difference between an **AI model** and an **AI agent**. Both are foundational, but they serve different roles.

### AI model

An AI model is a self-contained artifact (e.g., learned weights) consumed by a program to perform a specific function:

- A classifier predicts spam vs. not spam
- A text model completes sentences or writes poetry
- A speech model converts audio to text

Models have no goals, initiative, or context beyond the current input. They wait for a prompt, compute output, and stop. **Powerful, but passive.**

### AI agent

An AI agent is an **active system** that uses one or more models inside a larger decision process. It has autonomy, memory, goals, and the ability to act on what it observes.

An agent might:

- Use a language model to understand instructions
- Call a search tool to gather information
- Store conversation history in a vector database
- Monitor success and adapt over time

**The key difference:** the agent takes initiative and operates over time in a perceive–reason–act loop.

### Comparison

| Feature | AI Model | AI Agent |
|---------|----------|----------|
| **Scope** | Narrow task | Broader system of behavior |
| **Role** | Computes outputs from inputs | Chooses actions toward goals |
| **Context awareness** | Limited to inference window | Maintains and updates internal context |
| **Initiative** | Waits for input | Acts when triggered or scheduled |
| **Tool use** | No | Yes—often multiple tools and models |
| **Example** | Sentiment classifier | Support assistant that answers, escalates, and logs tickets |

**Analogy:** A model is like a calculator; an agent is like a personal assistant who listens, plans, asks questions, and acts on your behalf.

---

## Three categories of AI agents

Agents vary by how they interact with their environment. Three broad categories:

### 1. Software-based agents

Operate entirely in digital spaces—APIs, web UIs, documents, databases.

**Examples:**

- Retail customer-service chatbot
- Email triage agent that categorizes and replies
- Trading bot monitoring news and executing trades

**Characteristics:** No physical sensors; act through code and digital data; often use web search, file access, and LLMs.

### 2. Physical agents (embodied systems)

Interact with the real world via sensors and actuators.

**Examples:**

- Domestic cleaning robot
- Autonomous vehicle
- Factory robotic arm

**Characteristics:** Sense via cameras, LiDAR, microphones; act via motors and arms; must handle uncertainty, delay, and safety.

### 3. Hybrid and adaptive agents

Combine digital and physical capabilities and adapt from feedback.

**Examples:**

- Traffic system analyzing camera feeds and adjusting signals
- Healthcare assistant monitoring wearables and coordinating with doctors
- Warehouse robot using online inventory data and moving goods physically

**Characteristics:** Cross-domain operation; multi-modal data; improve through real-world feedback loops.

Complexity and opportunity both grow as you move from software-only to hybrid systems.

---

## Evolution: rule-based → learning-based → LLM-powered

Autonomous agents are not new—but their capabilities have expanded dramatically.

### Rule-based agents

Fixed logic: *if X, then Y.* Works for repetitive, well-defined tasks; fails in dynamic environments.

Systems like MYCIN and XCON (1970s–80s) relied on hand-written rules:

- *If the user says "I forgot my password," show reset form.*
- *If temperature > 30°C, turn on the fan.*

**Pros:** Understandable and controllable. **Cons:** Poor generalization; scaling requires thousands of manual rules.

### Learning-based agents

Machine learning shifted rule authoring from humans to data.

- **Supervised learning** (CNNs, RNNs) advanced perception—e.g., speech in virtual assistants
- **Reinforcement learning (RL)** learns via trial, reward, and penalty—the most "agent-like" paradigm for sequential decisions

**Example:** AlphaGo (2016) learned by playing millions of games; robot arms learn grasping without precise location data.

**Pros:** More flexible than rules. **Cons:** Heavy training, compute, and structured environments—less practical for general-purpose apps.

### LLM-powered agents

Models like GPT-4, Claude, and Gemini bring **zero-shot generalization**: vast world knowledge and reasoning in parameters, without retraining for every new task.

When embedded in agent systems, LLMs enable:

- **Tool use** — Selecting tools and parameters for each action
- **Dynamic task planning** — Decomposing goals into steps
- **Conversational memory** — Awareness across turns
- **Generalization** — Novel tasks without hardcoded behavior

**Example:** *"Summarize this research paper and email the key points to my team."* The agent understands, summarizes, formats, and calls an email API—none of it hardcoded.

**Limitations matter too:** hallucinations, interpretability, bias, latency, and security. Designing trustworthy systems requires understanding both capability and risk.

### Practice question

For each scenario, decide whether a **rule-based system** or an **LLM-powered agent** is more appropriate, and why:

1. Turn off office lights at 7 p.m. every weekday
2. Respond to customer emails, categorize them, escalate complex cases, and learn from past interactions
3. Flag financial transactions over $10,000 for manual review

<details>
<summary>Sample answers</summary>

1. **Rule-based** — Deterministic schedule; no reasoning needed.
2. **LLM-powered agent** — Unstructured language, nuance, escalation, and adaptation over time.
3. **Rule-based** — Simple threshold; auditable and predictable.

</details>

---

## When should you build an agent?

> **Course convention:** When we say "agent," we mean an **LLM-powered agent**.

Not every problem needs an agent. Simple scripts or rule-based automation may suffice. Agents add complexity, cost, and uncertainty—use them strategically.

Consider an agent when the use case involves **contextual decisions**, **dynamic context**, or **flexible execution** that traditional automation cannot handle.

### Three signals an agent may be the right choice

**1. Contextual decision-making**

Outcomes depend on nuanced judgment—ambiguous input, trade-offs, or prior interactions.

*Example:* Refund approval based on customer history, message tone, and return reason. Rules miss cues; an agent can reason like a support rep.

**2. Rules are too complex to maintain**

Dozens of branches, exceptions, and edge cases make static logic a liability.

*Example:* Vendor security review with evolving compliance and unstructured docs. An agent can read and interpret documents in the workflow instead of encoding every case.

**3. Unstructured or natural language data**

Pipelines must extract meaning from documents, emails, or conversations.

*Example:* Insurance intake where customers describe events in free text. An agent extracts entities, asks follow-ups, and routes the case.

If a deterministic solution suffices, prefer it.

---

## Summary

AI agents are autonomous systems that **perceive, reason, and act** toward goals. Unlike passive models, they operate over time, maintain context, and take initiative.

We covered three agent categories (software, physical, hybrid), evolution from rules to LLMs, and when agentic design is worth the complexity.

Understanding **when and why** to build agents sets the stage for designing them effectively.

**Next:** [Core Agent Components →](./02-core-agent-components.md)
