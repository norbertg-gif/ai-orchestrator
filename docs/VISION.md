# Vision

## One-sentence vision

**The user should never have to think about which AI to use.**

## Problem statement

People increasingly use several AI products because each service has different strengths, tools, interfaces, limits, and subscription economics. The result is manual orchestration:

- deciding which service should receive a request;
- discovering hidden subtasks;
- rewriting context for another model;
- moving partial results between chats;
- watching limits and switching providers;
- reconciling contradictory outputs.

This overhead grows with task complexity. A single sentence such as “redesign this dashboard and make the calculations correct” may imply requirements analysis, data validation, UX design, implementation, testing, review, and integration.

## Product thesis

A prompt is not necessarily a task. It is often an expression of intent or a desired outcome. The system should compile that intent into an executable workflow:

```text
Intent → Goal → Tasks → Subtasks → Dependencies → Delegation → Integration
```

The orchestrator is therefore not merely a multi-chat client. It is a workflow compiler and coordination layer over existing AI applications.

## Target user

The initial user is a technically capable individual who:

- uses several AI services regularly;
- prefers their existing web subscriptions over API billing;
- works on mixed tasks such as programming, UI design, research, documents, data analysis, and review;
- wants one central control surface without abandoning provider-native chats.

## Desired user experience

The user enters one request. The system:

1. identifies the intended outcome and assumptions;
2. discovers hidden work;
3. builds an editable dependency graph;
4. selects the most suitable available service for each subtask;
5. explains every routing decision;
6. dispatches work to authenticated provider tabs;
7. monitors progress and limits;
8. transfers structured context between services;
9. integrates outputs into a coherent result.

The user remains in control and can override any decision.

## Success criteria

The product is successful when it measurably reduces:

- provider-selection decisions made by the user;
- repeated context copying;
- unnecessary use of premium models for routine work;
- abandoned tasks after service limits;
- inconsistent outputs caused by poor handoffs.

It should improve completion rate, transparency, and effective use of subscriptions.
