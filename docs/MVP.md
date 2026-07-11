# MVP Definition — v0.1

## Objective

Validate that a central browser interface can decompose a user goal, route work transparently, and coordinate authenticated web chats without APIs.

## Primary user flow

1. User opens the orchestrator dashboard.
2. User enters a goal.
3. Planner proposes subtasks and dependencies.
4. Router proposes a provider for each subtask and explains why.
5. User approves or edits the plan.
6. Orchestrator opens or activates the provider tab.
7. Provider adapter inserts and optionally sends the generated prompt.
8. Dashboard shows status and a response preview.
9. User may create a handoff to another provider.

## Required features

### Central dashboard

- goal input;
- execution mode: assisted or automatic;
- plan/task graph view;
- provider status cards;
- response preview;
- execution log;
- pause, cancel, reassign, and open-original controls.

### Planner v0.1

- deterministic decomposition templates;
- optional AI-assisted decomposition through a selected provider;
- output validated against a local JSON schema;
- maximum task count and recursion depth;
- explicit dependencies and acceptance criteria.

### Router v0.1

- configurable capability matrix;
- deterministic scoring;
- hard constraints before preferences;
- manual provider availability and limit state;
- visible routing rationale;
- fallback chain per task category.

### Provider integration

Initial adapters:

- ChatGPT Web;
- Claude Web.

Each adapter must implement:

- detect authenticated usable page;
- find prompt editor;
- insert prompt;
- send prompt in automatic mode;
- detect generation state;
- extract latest assistant response;
- detect common limit/error states;
- expose “open original tab”.

### Handoff

A handoff package contains:

- original goal;
- assigned subtask;
- relevant prior outputs;
- decisions and constraints;
- unresolved questions;
- requested deliverable and acceptance criteria.

### Persistence

Store locally:

- projects;
- goals;
- plans;
- task states;
- routing decisions;
- provider preferences;
- response excerpts;
- feedback.

Do not store passwords, cookies, auth tokens, or hidden provider requests.

## Acceptance criteria

The MVP is complete when a user can:

- submit a goal in the dashboard;
- receive an editable multi-step plan;
- approve routing to ChatGPT or Claude;
- dispatch a prompt through the browser extension;
- observe task status;
- capture a response;
- reassign or hand off the task without manually reconstructing context.

## Explicitly deferred

- Gemini and Grok adapters;
- Claude Design and Claude Code specialized adapters;
- autonomous local file/repository edits;
- learning-based routing;
- multi-user cloud synchronization;
- mobile support;
- provider usage-cost accounting beyond user-supplied status.
