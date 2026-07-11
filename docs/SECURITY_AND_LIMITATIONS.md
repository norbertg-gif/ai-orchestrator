# Security, Privacy, and Limitations

## Security principles

- local-first storage;
- least-privilege extension permissions;
- no credential or token extraction;
- no undocumented provider endpoints;
- explicit user approval before dispatch;
- sanitized logs;
- clear indicator whenever a provider page is being controlled.

## Data handling

The orchestrator may store goals, plans, prompts, output excerpts, and routing metadata locally. Sensitive project content must be clearly identifiable and deletable.

Provide:

- per-project delete;
- delete all local data;
- export/import of sanitized project state;
- configurable retention.

## Provider terms and UI automation

The orchestrator interacts with visible user interfaces. Provider terms and interfaces can change. Automatic actions must be optional, conservative, and disableable. The product must not claim official provider integration unless one exists.

## Known technical limitations

- provider DOM changes can break adapters;
- response completion is not always unambiguous;
- consumer subscription limits may not expose precise machine-readable usage;
- browser security prevents true cross-origin embedded provider frames;
- file upload automation is restricted;
- some specialized experiences may need distinct adapters;
- desktop-only conversations may not appear on the web.

## Failure posture

When uncertain, the system must stop and request user action rather than guess, send unintended prompts, or copy unrelated chat content.
