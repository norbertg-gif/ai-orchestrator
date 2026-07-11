# Browser Integration

## Why a browser extension

The user already authenticates directly with each AI provider. A browser extension can coordinate existing tabs while preserving provider-native sessions and history.

A normal web application cannot reliably embed provider pages because framing is commonly blocked by CSP or `X-Frame-Options`. The dashboard therefore displays synchronized status and response previews, not literal embedded provider pages.

## UX model

The dashboard presents provider cards that behave like subframes:

- provider and mode;
- assigned task;
- state;
- latest response excerpt;
- limit/error indicator;
- open-original action;
- reassign/handoff action.

The real provider interaction occurs in ordinary authenticated tabs.

## Extension permissions

Use the minimum possible permissions:

- `tabs` only if required;
- `storage`;
- `scripting`;
- explicit host permissions for supported provider domains.

Prefer optional host permissions so the user grants access per provider.

## Messaging

```text
Dashboard
  ↕ runtime messages
Service worker
  ↕ tab messages
Provider content scripts
```

Every message must use a typed envelope containing request ID, task ID, provider ID, action, timestamp, and payload version.

## Assisted mode

Default for early releases:

- orchestrator activates the correct tab;
- inserts the prompt;
- user reviews and clicks Send;
- adapter observes the result.

## Automatic mode

Opt-in per provider. It may send prompts automatically only after explicit task approval. If adapter confidence is low, it must fall back to assisted mode.

## Response preview

Store plain text/Markdown excerpts and structured metadata. Do not clone whole provider pages or styles.

## Tab management

The extension should:

- reuse a designated orchestrator conversation where appropriate;
- avoid hijacking unrelated user chats;
- allow one or multiple sessions per provider;
- make conversation ownership visible;
- never close user-created tabs automatically without approval.
