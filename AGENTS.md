# Instructions for AI coding agents

Read `README.md` and every document in `docs/` before proposing architecture or writing code.

## Priorities

1. Preserve the planner/router separation.
2. Keep the MVP browser-first, local-first, and API-optional.
3. Implement a vertical slice before adding providers.
4. Prefer assisted dispatch over brittle full automation.
5. Keep provider-specific DOM logic behind adapters.
6. Do not extract credentials, cookies, tokens, or hidden API requests.
7. Every routing decision must be explainable and overridable.

## First deliverable

Create a runnable Chrome/Edge Manifest V3 extension with:

- a dashboard page;
- typed core schemas;
- a deterministic mock planner;
- a configurable capability matrix;
- routing explanations;
- mocked provider cards;
- unit tests for plan validation and routing.

Do not implement live ChatGPT/Claude DOM automation in the first commit.
