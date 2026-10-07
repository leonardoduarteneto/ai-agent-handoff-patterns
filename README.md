# AI Agent Handoff Patterns

Practical patterns for deciding when AI agents should respond, ask, use tools, escalate or hand off to humans.

## Why this project exists

AI agents should not try to handle every situation autonomously.

In real-world products, a good agent needs to recognize when it has enough context to act, when it needs more information, when a tool should be used and when a human should take over.

This repository explores reusable interaction and decision patterns for building safer, clearer and more human-centered AI experiences.

## Core decisions

An AI agent should be able to decide whether to:

1. **Respond**
   Answer directly when the request is clear and within its capabilities.

2. **Ask**
   Request additional context when important information is missing.

3. **Use a tool**
   Retrieve data or perform an action through an external system.

4. **Escalate**
   Route the situation to a specialized flow or higher-confidence process.

5. **Hand off to a human**
   Transfer control when human judgment, authorization or empathy is required.

## Handoff principles

Good handoff decisions should consider more than technical capability.

The agent should evaluate:

### Confidence
How certain is the agent that it understands the request and can respond correctly?

Low confidence should increase the likelihood of asking for clarification or escalating.

### Risk
What is the potential impact of a wrong answer or action?

Higher-risk situations should require stronger safeguards, additional validation or human review.

### User intent
Does the user explicitly want human assistance, or is the request better suited to human judgment?

A clear request for a person should be respected whenever possible.

### Authorization
Is the agent allowed to perform the requested action?

Some actions may require approval, identity verification or permissions that the agent does not have.

### Context completeness
Does the agent have enough information to make a reliable decision?

Missing critical information should trigger clarification instead of guessing.

### Emotional sensitivity
Does the situation involve frustration, conflict, vulnerability or a need for empathy?

Some interactions are better handled by a human even when the agent technically knows the answer.

### Recoverability
Can a wrong decision be easily reversed?

Irreversible or costly actions should have a lower threshold for escalation or human confirmation.

## Decision matrix

The following matrix provides a simple starting point for choosing the next action.

| Situation | Recommended action |
|---|---|
| Clear request, sufficient context, low risk | **Respond** |
| Important context is missing | **Ask** |
| External information or an action is required | **Use a tool** |
| Low confidence or higher-risk situation | **Escalate** |
| User explicitly requests a person | **Hand off to a human** |
| Authorization is required and unavailable | **Hand off to a human** |
| Emotionally sensitive or conflict-heavy interaction | **Hand off to a human** |
| Irreversible or high-impact action | **Escalate or require human confirmation** |

### Important

These patterns are not intended to replace domain-specific rules.

## Decision flow

A simple decision path can help make the handoff logic explicit.

```mermaid
flowchart TD
    A[User request] --> B{Is the request clear?}

    B -- No --> C[Ask for clarification]
    B -- Yes --> D{Is external data or an action required?}

    D -- Yes --> E{Is the agent authorized?}
    E -- No --> H[Hand off to a human]
    E -- Yes --> F[Use a tool]

    D -- No --> G{Is confidence sufficient and risk acceptable?}
    F --> G

    G -- No --> I{Can the situation be safely escalated?}
    I -- Yes --> J[Escalate]
    I -- No --> H

    G -- Yes --> K{Does the user request human help?}
    K -- Yes --> H
    K -- No --> L{Is human judgment or empathy required?}

    L -- Yes --> H
    L -- No --> M[Respond]

The appropriate thresholds for confidence, risk and authorization depend on the product, organization and regulatory context in which the agent operates.
