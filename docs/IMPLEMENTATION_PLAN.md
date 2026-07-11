# Implementation Plan

## Milestone 0 — Project foundation

- TypeScript workspace;
- linting, formatting, tests;
- Manifest V3 extension skeleton;
- dashboard route;
- typed message protocol;
- IndexedDB abstraction;
- CI workflow.

## Milestone 1 — Planning and routing vertical slice

- goal form;
- deterministic decomposition templates;
- task graph schema and validation;
- provider capability profiles;
- routing score and explanation;
- editable plan and assignment UI.

## Milestone 2 — ChatGPT adapter

- page detection;
- assisted prompt insertion;
- optional send;
- generation-state observation;
- response excerpt extraction;
- common error diagnostics.

## Milestone 3 — Claude adapter

Same contract and tests as ChatGPT adapter.

## Milestone 4 — Handoff and execution coordination

- task state machine;
- structured handoff builder;
- reassignment;
- limit/error fallback;
- execution log.

## Milestone 5 — Hardening

- adapter confidence and fallback behavior;
- local data controls;
- security review;
- integration tests;
- packaging and installation guide.

## First coding task for Codex

Create the repository foundation and a runnable extension dashboard. Implement only the core schemas, a static provider capability matrix, deterministic routing, and mocked provider cards. Do not automate real provider pages until the architecture and message protocol tests pass.
