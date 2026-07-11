# ADR-004: Human approval is the default execution gate

- Status: Accepted
- Date: 2026-07-11

## Context

Provider-page automation can mis-detect UI state or dispatch a prompt to the wrong conversation.

## Decision

The MVP defaults to assisted dispatch. Automatic send is opt-in per provider and only after the plan/task is explicitly approved.

## Consequences

- safer initial releases;
- easier debugging;
- slightly more user interaction;
- a clear migration path to greater automation.
