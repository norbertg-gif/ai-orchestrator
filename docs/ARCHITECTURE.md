# Architecture

## Architectural style

Browser-first, local-first, adapter-based modular monolith for the MVP.

The product consists of a Manifest V3 browser extension and a central dashboard. Core logic is provider-independent. Provider-specific DOM interaction is isolated behind adapters.

## Components

```text
User Goal
   │
   ▼
Intent Normalizer
   │
   ▼
Planner ───────────────► Plan Validator
   │                         │
   ▼                         ▼
Task Graph ───────────► Routing Engine
   │                         │
   ▼                         ▼
Execution Coordinator ─► Provider Adapters
   │                         │
   ▼                         ▼
State Store ◄────────── Responses / Errors / Limits
   │
   ▼
Integrator / Handoff Builder
```

### Dashboard

Provides the central input, plan editor, provider panels, status, logs, and human controls.

### Intent normalizer

Turns the raw request into a stable goal statement, identifies explicit constraints, records assumptions, and flags ambiguities without forcing unnecessary clarification.

### Planner

Produces a bounded directed acyclic graph of tasks. Each task includes:

- type;
- description;
- deliverable;
- acceptance criteria;
- dependencies;
- required capabilities;
- complexity and risk;
- context inputs.

### Plan validator

Rejects malformed, cyclic, excessively deep, duplicated, or unbounded plans. It can collapse over-decomposed plans.

### Routing engine

Applies hard capability constraints, scores eligible providers, selects a primary and fallback chain, and records the explanation.

### Execution coordinator

Controls task state transitions, dispatch, concurrency, retries, handoffs, cancellation, and human approval gates.

### Provider adapters

Encapsulate DOM selectors and interaction semantics for each service. Adapters never expose credentials or depend on undocumented private endpoints.

### Integrator

Checks completeness, resolves incompatible outputs through explicit review tasks, and prepares the final consolidated result or next handoff.

### State store

Use browser-local persistence initially (IndexedDB). Store normalized data, not full browser pages.

## Runtime model

Recommended extension contexts:

- dashboard page: main UI;
- service worker: orchestration and cross-tab messaging;
- content scripts: provider-page interaction;
- IndexedDB: persistent state;
- optional offscreen document only when required by browser constraints.

## Task state machine

```text
DRAFT
→ READY
→ APPROVED
→ DISPATCHING
→ RUNNING
→ WAITING_FOR_USER | BLOCKED | FAILED | COMPLETED
→ HANDOFF_READY
→ REASSIGNED | INTEGRATED
```

Transitions must be explicit and logged.

## Security boundary

The extension may access only explicitly declared provider domains. It must not:

- read browser cookies;
- extract access tokens;
- call hidden provider APIs;
- bypass CSP or authentication controls;
- silently upload arbitrary files;
- execute provider-generated code locally.

## Initial technology choice

- TypeScript;
- Chrome/Edge Manifest V3;
- React for dashboard UI;
- Zustand or a small reducer-based store;
- IndexedDB through a thin typed wrapper;
- Zod or JSON Schema for plan validation;
- Vitest for unit tests;
- Playwright for extension integration tests where feasible.

Avoid a local Python backend in v0.1 unless browser constraints prove it necessary.
