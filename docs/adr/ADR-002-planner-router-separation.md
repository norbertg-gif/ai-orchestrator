# ADR-002: Separate planning from routing

- Status: Accepted
- Date: 2026-07-11

## Context

A provider-aware planner may distort decomposition to suit available tools. The system must first determine what work exists, then decide who should do it.

## Decision

Planner outputs provider-neutral tasks and required capabilities. Router consumes that graph and assigns providers.

## Consequences

- plans can be tested independently;
- provider matrix can change without replanning;
- routing explanations become clearer;
- an additional validation boundary is required.
