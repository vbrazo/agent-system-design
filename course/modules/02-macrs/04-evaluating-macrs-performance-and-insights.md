# Evaluating MACRS: Performance and Insights

**Overview:** Learn how to evaluate multi-agent conversational recommenders—success rates, adaptation, efficiency metrics—and how MACRS's coordination, reflection, and planning translate into measurable gains.

---

In agentic system design, **evaluation** means assessing the **entire system's behavior over time**, not just individual output accuracy.

An effective agentic system must:

- Reason strategically
- Adapt to user behavior
- Maintain progress toward its goal

—in dynamic, unpredictable environments.

Success is not only correct responses but **how effectively** the system manages dialogue, gathers information, decides, and adjusts to feedback—especially when **multiple agents collaborate**.

This lesson covers how MACRS was evaluated and what that reveals about well-designed agentic systems.

---

## Experimental setup

MACRS was evaluated in a **controlled simulation** mimicking conversational recommendation scenarios.

Instead of unpredictable human users alone, researchers used an **LLM-based user simulator**:

- Built with **GPT-3.5**
- Conditioned on the item catalog and target user preferences
- Responded in natural language, selected or ignored recommendations, occasionally changed preferences

This enabled consistent testing of whether MACRS:

- Collects preferences through dialogue
- Adapts across turns
- Delivers relevant, persuasive recommendations
- Recovers from failed recommendations or uncooperative behavior

Simulation supports **fair comparisons** across system variants and baselines—critical for evaluating agentic design choices.

> **Caveat:** Simulators built from the same LLM family as the system under test (e.g., GPT simulator evaluating GPT-based MACRS) can introduce **positive bias**. Diverse **human user studies** are typically needed for full generalizability.

For agentic designers, simulation is part of the **design feedback loop**—surfacing edge cases and testing coordination before going live.

**Scope note:** The MACRS paper's reported experiments did not explicitly evaluate extreme edge cases (e.g., extreme impatience, highly ambiguous preferences outside simulator conditioning) or detailed error recovery for tool/API failures.

---

## Evaluation metrics

Three metrics capture different dimensions of agentic performance:

| Metric | What it measures | Agentic interpretation |
|--------|------------------|------------------------|
| **Success Rate** | User selects a recommended item before dialogue ends | **Goal-completion score** |
| **Hit Ratio@K** | Correct/liked item appears in top-K recommendations | **Reasoning and ranking quality** |
| **Average Number of Turns** | Turns needed to reach success | **Dialogue efficiency**—enough elicitation without tiring the user |

Together they answer:

- Did the system achieve its objective?
- Did it recommend the right items?
- Did it use dialogue turns wisely?

These are the questions to ask of **any** agentic system—sustained, adaptive performance across interaction, not perfection on isolated turns.

---

## Comparative results

MACRS was compared to baselines including traditional and LLM-only approaches:

| Model | Success Rate | Hit Ratio@K | Avg. Turns |
|-------|--------------|-------------|------------|
| Fine-tuned GPT | 40.2% | 58.6% | 7.9 |
| GPT-RS | 42.5% | 60.1% | 7.4 |
| GPT-RL | 48.7% | 64.3% | 6.8 |
| **MACRS** | **58.3%** | **69.5%** | **5.9** |

### Design perspective

- **Higher Success Rate** — Modular design and strategy control guide users more purposefully toward recommendations.
- **Higher Hit Ratio@K** — User modeling and reflection help surface items aligned with inferred preferences.
- **Fewer turns** — Better timing, strategic transitions, and adaptive planning move dialogue forward without circling.

These gains reflect **structural choices**—multi-agent collaboration, shared memory, reflection—not just better prompting or fine-tuning.

MACRS didn't only sound fluent—it **acted intelligently**. Case-study dialogues in the MACRS paper show superior strategic planning and adaptability vs. single-agent ChatGPT-style baselines.

---

## Mapping design features to performance

| Agentic design feature | What it enables | Performance impact |
|------------------------|-----------------|-------------------|
| **Multi-agent role specialization** | Focused asking, recommending, chit-chat | Higher dialogue diversity, improved goal alignment |
| **Central planner with reasoning** | Optimal response given context and user state | Fewer redundant turns, higher success rate |
| **Shared user profile memory** | Persistent preferences across turns | Better personalization, more relevant recommendations |
| **Feedback-aware reflection** | Learn from behavior; adjust strategy | Increased adaptability, reduced recommendation failure |

---

## Learning from ablations

Ablation studies stress-test design: disable a component and observe performance drop.

MACRS was evaluated with:

| Configuration | What was removed |
|---------------|------------------|
| **No information-level reflection** | No profile updates from subtle signals (skips, browsing) |
| **No strategy-level reflection** | Planner/responders don't learn from failures |
| **No multi-agent separation** | Single agent generates full response |
| **No planner** | Random choice among candidates |

**Result:** Each removal caused significant degradation—especially Success Rate and early relevant recommendations.

This confirms that MACRS gains come from **architecture**, not any single trick.

---

## Wrapping up the MACRS case study

We started with a design challenge: a goal-directed conversational recommender that gathers preferences, engages users, and drives successful recommendations through natural dialogue.

| Limitation | MACRS response |
|------------|----------------|
| Traditional CRSs | Lacked adaptability |
| LLM-only CRSs | Lacked control |

MACRS addressed both with:

- **Role specialization** — Distinct responder agents
- **Centralized planning** — Strategic coordination
- **Feedback-aware reflection** — Real-time adaptation
- **Shared memory** — Coherence across turns

Each choice was a deliberate commitment to **modularity**, **adaptability**, and **strategic reasoning**.

---

## Key takeaways for agentic system designers

Principles that extend beyond recommenders:

| Principle | MACRS example | Broader application |
|-----------|---------------|---------------------|
| **Design for role clarity** | Asking / recommending / chit-chat agents | Legal research: retrieval, summarization, drafting specialists |
| **Plan, don't just prompt** | Planner selects best conversational act | Dev agent: planner breaks features into code, test, docs subtasks |
| **Reflect and adapt** | Dual reflection loops | Manufacturing agent adjusts from sensor feedback and anomalies |
| **Optimize the system, not just the model** | Gains from architecture, not bigger LLM alone | Universal: architectural excellence over model scaling alone |

Build systems that **reason, adapt, and learn across time**—from supply-chain logistics to scientific discovery with hypothesis and experiment-planning agents.

---

## Summary

Evaluate agentic CRSs with **goal-oriented metrics** (success, hit rate, efficiency), **simulation plus human validation**, and **ablations** that tie components to outcomes.

MACRS demonstrates that multi-agent planning plus feedback-aware reflection can outperform monolithic LLM approaches on goal-directed conversational recommendation.

**Previous:** [← User Feedback-Aware Reflection Mechanism](./03-user-feedback-aware-reflection-mechanism.md) · **Back to module:** [MACRS Overview](./README.md)

**Related:** [Module 1: Agent Design Fundamentals](../01-agent-design-fundamentals/README.md)
