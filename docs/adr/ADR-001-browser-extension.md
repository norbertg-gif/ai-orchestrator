# ADR-001: Use a browser extension as the integration layer

- Status: Accepted
- Date: 2026-07-11

## Context

The user primarily uses authenticated AI web applications and does not want an API-first product. Provider pages generally cannot be embedded in third-party iframes.

## Decision

Use a Chrome/Edge Manifest V3 extension with a central dashboard, service worker, and provider content scripts.

## Consequences

Positive:

- reuses existing authenticated sessions;
- no API keys required for MVP;
- can open, focus, and observe provider tabs.

Negative:

- adapters depend on changing DOM structures;
- automatic interaction may require maintenance;
- permissions and provider terms require careful handling.
