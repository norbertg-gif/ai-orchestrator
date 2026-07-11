# Core Data Model

## Project

A logical workspace containing goals, provider preferences, and history.

## Goal

The user's normalized desired outcome with constraints and success criteria.

## Plan

A versioned task graph generated from a goal. Editing creates a new plan revision.

## Task

A bounded unit of work with dependencies, required capabilities, deliverable, and acceptance criteria.

## Assignment

The selected provider/mode, routing score, rationale, fallback chain, and approval state for one task.

## Run

One execution attempt of one assignment. Stores timestamps, status, prompt snapshot, response excerpt, and error metadata.

## Handoff

A structured continuation package from one task/run/provider to another.

## Provider profile

Capability scores, availability, limit pressure, supported interaction modes, and user preferences.

## Feedback

User evaluation tied to a task and provider assignment.

## Versioning

All persisted records should include:

- schema version;
- stable UUID;
- created/updated timestamps;
- project ID;
- source/revision metadata where relevant.
