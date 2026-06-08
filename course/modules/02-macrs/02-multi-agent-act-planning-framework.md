# MACRS Multi-Agent Act Planning Framework

**Overview:** Explore how MACRS delegates conversational tasks to specialized responder agents and uses a planner agent to select the best response—through shared memory and strategic oversight for goal-directed dialogue.

---

In the previous lesson, MACRS reimagined conversational recommendation as a multi-agent system. A key question remains: **even with well-designed agents, who decides what actually gets said?**

Imagine chatting about what to watch tonight. The assistant asks about thrillers, throws out a random movie, then loops back to *"What genre do you enjoy?"* Each line may sound fine; the conversation feels **scattered**.

That is the **act planning** problem—not what *can* be said, but what **should** be said next to move forward.

In goal-directed dialogue, every turn should be:

- **Purposeful**
- **Context-aware**
- **Strategically chosen**

Many LLM chat systems generate plausible replies without clear planning—they stall or meander.

MACRS splits the problem into two coordinated steps:

1. **Generate options** with specialized responder agents
2. **Select the best** with a central planner agent

This is a concrete instance of the **Manager-Worker orchestration pattern** from Module 1, tailored for goal-directed CRS dialogue.

---

## Generating response options

Instead of one model juggling all tasks, MACRS uses **three responder agents**:

| Agent | Goal |
|-------|------|
| **Asking agent** | Elicit preferences through targeted questions |
| **Recommending agent** | Suggest relevant items from the current user profile |
| **Chit-chat agent** | Keep conversation engaging when no immediate goal move is available |

Each operates independently but draws from a **shared user profile and memory**—like a brainstorming session where each agent proposes what the system should say next.

### Profiling instructions

Each responder is primed with **role-specific prompts** and access to:

- **Dialogue history** — Avoid repetition or irrelevance
- **User profile** — Revealed, liked, skipped, or responded-to preferences
- **Agent goal** — Ask, recommend, or engage lightly

Example instructions from the MACRS paper (simplified):

| Agent | Core instruction |
|-------|------------------|
| **Asking** | *"You should elicit user preferences by asking questions."* |
| **Chit-chat** | *"You should chit-chat with the user to learn about their preferences… express admiration for item elements to guide the conversation."* |
| **Recommending** | *"You should recommend an item to the user and generate an engaging description."* |
| **Planner** | *"Choose one of the candidate responses based on three dialogue acts: recommending, asking, and chit-chatting."* |

> **Note on prompt engineering:** Production prompts are typically far richer—extensive context, few-shot examples, JSON output formats, safety guidelines, and persona definitions. MACRS examples show the *essence* of each role; real deployments need more sophisticated prompt design.

### Example candidate responses

User context: general interest in a relaxing animated film.

- **Asking:** *"Do you usually prefer series or standalone movies?"*
- **Recommending:** *"You might like Inception. It's a top-rated thriller."*
- **Chit-chat:** *"Some people say watching thrillers at night is the best!"*

Each is valid; **only one** is used.

---

## Selecting the final response

After responders propose candidates, a **fourth agent—the planner**—selects the reply that best advances the system's goal.

If responders are creative team members, the planner is the **team lead** choosing the option that moves the conversation forward.

### What the planner evaluates

- **User preferences** — What do we already know?
- **Dialogue progress** — Still gathering info, or ready to recommend?
- **Candidate options** — Which adds most value now?
- **Engagement balance** — Natural tone while nudging progress

The planner favors:

- Follow-up questions when the user is hesitant or preferences are thin
- Recommendations when the user engaged with similar items

The planner has access to:

- Full dialogue history
- Shared memory structure
- Current user profile (including inferred preferences)
- Summary of all three candidate responses

It reasons over **semantic relevance**, **dialogue strategy**, and **conversational timing**—not just keywords.

### Example in action

**User:** *"I want to watch a relaxing animated film."*

| Agent | Candidate |
|-------|-----------|
| Recommending | Suggest *Zootopia* |
| Asking | *"Are you looking for classic films or more recent ones?"* |
| Chit-chat | Chat about Disney |

**Planner choice:** The clarifying question—*classic vs. recent*—guides toward a useful recommendation without losing fluency.

---

## Discussion: why not one big prompt?

**Question:** Why not use one powerful LLM with a complex prompt that simulates asking, recommending, chit-chatting, and choosing the best response in a single call?

<details>
<summary>Sample answer</summary>

A single prompt overloads one context with competing goals—elicitation, recommendation, engagement, and meta-selection. Roles blur, strategy is implicit, and debugging is hard. MACRS separates **generation** (specialized responders) from **selection** (planner), mirroring human teams. You get clearer logic, agent-level observability, and explicit strategic control—at the cost of multiple LLM calls per turn.

</details>

---

## Agentic design takeaways

| Principle | How MACRS applies it |
|-----------|----------------------|
| **Delegate, don't overload** | Specialized responders instead of one do-everything agent |
| **Strategize with oversight** | Planner reasons across options to advance the goal |
| **Maintain shared memory** | Dialogue history, user profile, strategy suggestions, dialogue act history, corrective experiences—all inform every agent |
| **Orchestrate, don't dominate** | Planner selects output but doesn't micromanage how responders propose ideas |

### Trade-off: latency and cost

Each turn typically requires **four LLM calls** (three responders + one planner). That increases latency and cost vs. a single monolithic call.

The overhead is often justified by:

- Better goal-directed dialogue performance
- Improved interpretability (log planner decisions)
- Modularity for development and maintenance

MACRS results demonstrate that this trade-off can be worthwhile for CRS use cases.

---

## Summary

MACRS plans its next move through structured multi-agent flow: responders propose; the planner selects contextually.

This embodies **division of responsibility**, **shared memory**, and **coordinated decision-making**.

**Next:** [User Feedback-Aware Reflection Mechanism →](./03-user-feedback-aware-reflection-mechanism.md)

**Previous:** [← Introduction to MACRS](./01-introduction-to-macrs-and-design-challenge.md)
