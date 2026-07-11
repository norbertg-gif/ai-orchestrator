# ADR-003: Keep MVP local-first and API-optional

- Status: Accepted
- Date: 2026-07-11

## Context

The target user wants to use existing web subscriptions and avoid operating or paying for a separate model/API layer.

## Decision

Persist orchestration data locally and require no model API. AI-assisted planning may later use a provider through its ordinary web UI.

## Consequences

- simpler privacy model and deployment;
- no server account required;
- multi-device synchronization is deferred;
- precise automated cost/usage data may be unavailable.
