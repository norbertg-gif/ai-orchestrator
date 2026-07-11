# Provider Adapter Specification

## Purpose

Provider adapters isolate all service-specific browser behavior from the orchestration core.

## Adapter contract

```ts
interface ProviderAdapter {
  id: string;
  matches(url: URL): boolean;
  detectPage(): Promise<PageDetection>;
  locateComposer(): Promise<ComposerHandle>;
  insertPrompt(prompt: string): Promise<void>;
  sendPrompt(): Promise<void>;
  getRunState(): Promise<RunState>;
  getLatestResponse(): Promise<ResponseSnapshot | null>;
  detectErrors(): Promise<ProviderError[]>;
  focusConversation(): Promise<void>;
}
```

## Required behavior

Adapters must:

- prefer semantic selectors (`aria-*`, roles, labels) over brittle class names;
- tolerate minor DOM changes;
- expose confidence when page state is uncertain;
- avoid destructive actions;
- never scrape passwords, cookies, or tokens;
- avoid undocumented network endpoints;
- support assisted mode where the user performs the final send action.

## Run states

- `idle`
- `prompt_inserted`
- `generating`
- `completed`
- `waiting_for_user`
- `limit_reached`
- `error`
- `unknown`

## Error taxonomy

- authentication required;
- unsupported page;
- composer not found;
- send unavailable;
- generation timeout;
- usage limit;
- network error;
- provider UI changed;
- response extraction failed.

## Robustness strategy

Each adapter should use:

1. multiple selector candidates;
2. semantic text and ARIA detection;
3. MutationObserver for generation changes;
4. bounded timeouts;
5. diagnostics with sanitized DOM metadata;
6. feature flags to disable broken automatic actions.

## Initial providers

### ChatGPT Web

Support the standard authenticated conversation UI. The adapter should not assume desktop-app conversation synchronization.

### Claude Web

Support standard Claude chat first. Claude Design and Claude Code web experiences should become separate adapter profiles if their interaction models differ materially.

## Testing

Maintain provider-specific fixtures and mocked DOM snapshots. Live smoke tests should be manual or opt-in because provider interfaces and accounts vary.
