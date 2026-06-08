# Structuring Agent Behavior: Agent Orchestration Patterns

**Overview:** Explore orchestration patterns that structure decision-making and collaboration—single-agent strategies (tool loops, ReAct, plan-and-execute) and multi-agent models (Manager-Worker, decentralized handoffs)—and when to apply each.

---

The previous lesson covered how agents perceive, remember, reason, and act in a loop. As capabilities grow, so does the need for **structure**: how does an agent decide what to do next, sequence actions, choose tools, or collaborate with others?

**Orchestration** defines internal decision flow and, in complex setups, coordination across agents. These patterns enable dynamic routing, parallel sub-goals, and reliable multi-step behavior.

> **Note:** In this course, orchestration patterns are **implementation strategies** for structuring behavior—not a fixed, mutually exclusive taxonomy.

## Learning objectives

By the end of this lesson, you will understand:

- Single-agent patterns: tool calling loops, ReAct, plan-and-execute
- Multi-agent patterns: Manager-Worker, decentralized handoffs
- How to choose patterns based on task complexity and system needs
- How frameworks like LangChain, AutoGen, and CrewAI support orchestration

---

## Single-agent orchestration patterns

A **single-agent system** has one model in charge: it receives input, decides, and acts—possibly with tools.

Patterns differ in how structured reasoning is, how tools are chosen, and how many steps run before output.

### Tool calling loop

The simplest structure: decide tool (if any) → execute → observe → repeat until done or stop.

Uses the LLM as reasoning core, a tool layer, and often short-term memory for state.

**Example:** *"Send an email summary of this document."*

1. Parse document
2. Call summarization tool
3. Send via messaging API
4. Exit

Common in LangChain `AgentExecutor` and OpenAI tool-calling setups.

**Trade-off:** Simple, but long brittle chains are hard to debug or recover from.

### ReAct (reasoning + acting)

Alternates **explicit reasoning steps** with tool actions: think → act → observe → repeat.

Improves transparency—thoughts and actions are logged for debug and audit. Requires structured "Thought" output from the LLM.

**Example:** *"Find the most affordable flight to Tokyo."*

- Think: "I need flight aggregators."
- Act: Call flight search API
- Observe: Several options
- Think: "Filter by price and airline."
- Act: Return best result

Used in OpenAI function-calling agents, LangChain, AutoGen.

**Trade-off:** Better traceability; higher latency and token use; long chains still hard to debug on failure.

### Plan-and-execute

Separates planning from execution: first produce a full plan, then execute each step.

Useful when the goal is complex but can be decomposed upfront. Often uses a planning LLM call, an execution module, and memory for plan and results.

**Example:** *"Write a report on Q2 revenue and email it to the team."*

Plan:

1. Retrieve Q2 revenue data
2. Create chart
3. Write summary
4. Send email

Then execute sequentially.

Supported in AutoGen (hierarchical agents) and LangChain planners/executors.

**Trade-off:** Clear structure; initial plans may stale if the environment changes—requiring re-planning.

---

## Multi-agent coordination patterns

When scope, specialization, or parallelism exceeds one agent, **multi-agent architecture** distributes work.

### Manager-Worker pattern

A **manager** decomposes goals, assigns **workers**, and integrates results.

| Role | Responsibility |
|------|----------------|
| Manager | Planning and delegation |
| Workers | Specialized subtasks with distinct tools/instructions |
| Shared memory | Task queues and results |

**Flow:** Goal → decompose (*research*, *outline*, *introduction*, *visuals*) → assign workers → stitch output.

Mirrors human teams; strong coordination.

**Trade-offs:** Central bottleneck and single point of failure; poor delegation breaks the workflow.

### Decentralized handoff pattern

No central manager. **Peer agents** pass control based on task state or input type, using handoff protocols and shared state.

**Example — travel planning:**

- Agent A handles query → identifies flight need → hands off to Agent B (flights)
- Agent B books → triggers Agent C (hotel)

**Trade-offs:** Flexible and robust in dynamic environments; risk of conflicts, deadlocks, or missed handoffs without careful design.

---

## Choosing the right orchestration strategy

### Single agent vs. multi-agent

| Factor | Single agent | Multi-agent |
|--------|--------------|-------------|
| **Task scope** | Focused, narrow tasks | Multiple domains or independent subgoals |
| **Specialization** | Generalist sufficient | Distinct competencies (legal, code, comms) |
| **Execution** | Linear step-by-step | Parallel threads (e.g., moderation checks) |
| **Observability** | Centralized logic, easier debug | Modular but needs coordination and shared memory |

**Examples:**

- Meeting scheduler → often single agent
- Assistant that summarizes reports, generates agendas, and negotiates across departments → multi-agent
- Document translate → summarize → format → single loop
- Content moderation (bias + misinformation + language) → parallel agents

### Selecting a pattern within each approach

**Single-agent:**

| Pattern | When to use |
|---------|-------------|
| **Plan-and-execute** | Steps known upfront; sequential accuracy (travel booking, multi-part docs) |
| **Tool calling loop** | Dynamic exploration; act–observe–iterate (debugging, search, synthesis) |
| **ReAct** | Transparency matters—regulated or educational contexts |

**Multi-agent:**

| Pattern | When to use |
|---------|-------------|
| **Manager-Worker** | Central planner can decompose and delegate with clear roles |
| **Decentralized handoffs** | Independent agents, environmental change, no single agent has full context |

---

## Frameworks in practice

Patterns are concept-agnostic; frameworks make them easier to implement.

### LangChain / LangGraph

- **Agent executors** — Step-by-step tool selection
- **LangGraph** — Workflows as graphs: branching, retries, explicit state
- Integrations: search, APIs, files, databases; memory and session state
- Extensible; integrates with AutoGen, CrewAI, custom platforms

Best for structured pipelines with control over tools and memory.

### AutoGen (Microsoft)

- Agents as conversational entities with roles, goals, toolsets
- Structured message threads; sync/async handoffs
- **Human-as-agent** for approval and oversight
- Strong for negotiation, verification, multi-step refinement (code review, peer review)

### CrewAI

- Built around Manager-Worker; also supports hybrid and parallel models
- **Crew:** project manager + specialized workers + shared task queue/memory
- Human approval hooks; integrates with external LLMs, vector DBs, APIs

Across all frameworks, core concepts persist: **planning, delegation, handoff, memory sharing.**

A well-structured system:

- Defines agent roles clearly
- Tracks progress and shares context
- Handles failures and disagreements gracefully

---

## Case study: AI research assistant

Design an assistant for a product team using:

- Competitor announcements (web)
- Customer reviews (pain points, feature requests)
- Internal sales reports
- Synthesized product update recommendations

**Requirements:** Parallel tasks; coordinated review/synthesis; **human approval** before sending to stakeholders.

**Exercise:** Choose the most appropriate orchestration pattern and explain your reasoning.

<details>
<summary>Sample approach</summary>

**Manager-Worker** with parallel workers fits well: one manager coordinates research agents (web, reviews, sales) running in parallel, then a synthesis worker drafts the recommendation. **Human-in-the-loop** approval gates the final send. LangGraph or CrewAI can model the workflow with explicit state and approval nodes.

</details>

---

## Summary

Orchestration structures how agents think and act—solo or in teams. Single-agent patterns (tool loop, ReAct, plan-and-execute) trade simplicity, transparency, and upfront planning. Multi-agent patterns (Manager-Worker, handoffs) trade coordination against flexibility.

Choose based on task structure, specialization, parallelism, and observability needs—then implement with frameworks that match your control and collaboration requirements.

**Previous:** [← Component Interaction and Memory](./03-component-interaction-and-memory.md) · **Next:** [Guardrails and Human Oversight →](./05-guardrails-and-human-oversight.md)
