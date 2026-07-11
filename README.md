# AI Orchestrator

> The user describes the goal. The system decides how to achieve it.

AI Orchestrator is a browser-first coordination layer for people who already use multiple AI services through their normal web interfaces. It converts one natural-language request into a transparent task graph, delegates each subtask to the most suitable available service, tracks progress, and hands work between services when necessary.

The initial target environment is Chrome/Edge on Windows with authenticated sessions for ChatGPT, Claude, Gemini, Grok, Claude Code, Claude Design, and similar web applications.

## Core problem

A seemingly simple prompt often contains hidden work: requirements analysis, research, UI design, implementation, validation, testing, and synthesis. Users should not have to discover those subtasks manually or decide which AI service should handle each one.

## Product principles

1. **Goal first:** the user states intent and desired outcome, not a provider.
2. **Transparent planning:** the system shows the proposed decomposition and routing before execution.
3. **Capability-aware routing:** selection is based on task fit, required tools, context, availability, and observed quality.
4. **Subscription-first:** the MVP coordinates services through the authenticated web interfaces the user already pays for; no API is required.
5. **Human control:** every automated action can be reviewed, overridden, paused, or reassigned.
6. **Graceful fallback:** limits and failures trigger a structured handoff to an appropriate alternative.
7. **No credential extraction:** the system never reads passwords, session tokens, or private internal APIs.

## MVP scope

Version 0.1 will provide:

- a central browser dashboard;
- one input for a user goal;
- deterministic task decomposition with an optional AI-assisted planner;
- editable task graph;
- capability matrix and rule-based router;
- provider adapters for ChatGPT Web and Claude Web;
- assisted and automatic prompt dispatch;
- live status and response preview panels;
- structured handoff between providers;
- manual availability and limit controls;
- local project/history storage.

See [docs/MVP.md](docs/MVP.md) and [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Non-goals for v0.1

- replacing provider applications;
- bypassing usage limits or access controls;
- scraping private endpoints or authentication tokens;
- autonomous modification of arbitrary local repositories;
- perfect cost estimation for subscription products;
- support for every AI service on day one.

## Proposed repository layout

```text
ai-orchestrator/
├── extension/              # Chrome/Edge Manifest V3 extension
├── dashboard/              # central UI
├── core/                   # planner, router, execution graph, handoff
├── providers/              # provider-specific browser adapters
├── storage/                # local persistence and schemas
├── tests/
├── docs/
│   ├── adr/
│   └── specs/
└── README.md
```

## First implementation milestone

Build a vertical slice that accepts a goal, produces an editable plan, routes one subtask to either ChatGPT Web or Claude Web, opens/activates the relevant tab, inserts the prompt, and returns the response status to the dashboard.

The first implementation agent should read all files in `docs/` before creating code.
