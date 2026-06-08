# Module 2: Multi-Agent Conversational Recommender System (MACRS)

A case study in applying agentic system design to goal-directed dialogue. MACRS combines specialized agents, centralized planning, and feedback-aware reflection to build conversational recommenders that are both fluent and strategically controlled.

**Prerequisite:** [Module 1: Agent Design Fundamentals](../01-agent-design-fundamentals/README.md)

## Lessons

| # | Lesson | Topics |
|---|--------|--------|
| 1 | [Introduction to MACRS and the Design Challenge](./01-introduction-to-macrs-and-design-challenge.md) | CRS problem space, LLM-only flaws, single vs. multi-agent, design goals, architecture overview |
| 2 | [Multi-Agent Act Planning Framework](./02-multi-agent-act-planning-framework.md) | Responder agents, planner agent, shared memory, Manager-Worker pattern, trade-offs |
| 3 | [User Feedback-Aware Reflection Mechanism](./03-user-feedback-aware-reflection-mechanism.md) | Information-level vs. strategy-level reflection, real-time adaptation, failure detection |
| 4 | [Evaluating MACRS: Performance and Insights](./04-evaluating-macrs-performance-and-insights.md) | Metrics, baselines, ablations, design-to-performance mapping, takeaways |

## Learning outcomes

After completing this module, you will be able to:

- Explain why goal-directed conversational recommenders need more than a single LLM
- Design a multi-agent act planning workflow with specialized responders and a central planner
- Implement feedback-aware reflection at information and strategy levels
- Evaluate agentic CRS performance with task-oriented metrics and ablation studies
- Transfer MACRS design patterns to other multi-agent, goal-directed systems
