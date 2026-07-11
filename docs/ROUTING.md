# Planning and Routing

## Separation of concerns

The planner answers: **What work must be done?**

The router answers: **Which available service should do each task?**

These must remain separate. Provider preferences must not distort task decomposition.

## Task schema

Minimum fields:

```json
{
  "id": "ui-design",
  "title": "Design dashboard information architecture",
  "type": "ui_ux_design",
  "description": "Create layout and interaction specification.",
  "deliverable": "Component-level design specification",
  "acceptanceCriteria": ["covers desktop layout", "defines empty and error states"],
  "dependencies": ["requirements-analysis"],
  "requiredCapabilities": ["visual_design", "long_context"],
  "complexity": 3,
  "risk": 2,
  "parallelizable": true
}
```

## Provider capability profile

```json
{
  "id": "claude-web",
  "displayName": "Claude Chat",
  "capabilities": {
    "ui_ux_design": 90,
    "software_architecture": 85,
    "code_review": 82,
    "current_web_research": 40
  },
  "tools": ["attachments", "long_context"],
  "availability": "available",
  "limitPressure": 0.2,
  "userPreference": 0.8
}
```

Scores are user-editable priors, not objective truth.

## Routing process

1. Eliminate providers missing hard requirements.
2. Eliminate unavailable providers.
3. Calculate suitability score.
4. Apply strategy weights.
5. Select primary and ordered fallbacks.
6. Present rationale and allow override.

## Baseline scoring

```text
score =
  0.40 × capability fit
+ 0.15 × tool fit
+ 0.15 × historical success
+ 0.10 × context continuity
+ 0.10 × user preference
+ 0.10 × availability
- 0.15 × limit pressure
- 0.10 × expected latency
- 0.10 × handoff overhead
```

Weights are normalized by the implementation. Hard constraints always dominate scoring.

## Execution strategies

### Balanced

Use the least expensive/limited capable service while reserving stronger services for high-risk decisions.

### Quality

Maximize task fit; add independent review for high-risk outputs.

### Fast

Minimize handoffs and parallelize independent tasks.

### Preserve limits

Avoid providers with high limit pressure and prefer already-open context where adequate.

## Decomposition policy

Do not split work merely because multiple providers exist. Split when at least one condition holds:

- distinct specialist capabilities are required;
- tasks can run meaningfully in parallel;
- one task produces an artifact required by another;
- independent review materially reduces risk;
- context would become unnecessarily large for a single conversation.

Collapse tasks when handoff overhead is greater than expected benefit.

## Fallback policy

Fallback is task-specific. It must preserve:

- goal and acceptance criteria;
- completed work;
- decisions and constraints;
- relevant output excerpts;
- unresolved items;
- exact continuation point.

Limit detection should first be explicit/manual. DOM-based automatic detection is an enhancement, not the only source of truth.

## Feedback learning

MVP records feedback but does not train a model. Update routing priors through transparent statistics:

- success/failure;
- user rating;
- reassignment frequency;
- completion time;
- manual provider override.

Any adaptive score must remain inspectable and resettable.
