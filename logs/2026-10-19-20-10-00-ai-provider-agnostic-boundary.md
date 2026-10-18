# AI usage must be provider-agnostic

## Context and status
Accepted architectural principle discussed on 2026-10-19. The detailed design is deliberately deferred.

## Accepted decision
- Application features using AI must go through a shared provider-agnostic application boundary rather than couple business functionality directly to a particular AI vendor, model or SDK.
- The boundary must permit different AI providers and models later, including selecting different models/providers for different kinds of tasks rather than assuming one global model.
- This is a direction for future AI-dependent features, **not** a request to implement an AI platform now. Service shape, configuration, credentials, model selection/routing, capability matching, fallbacks and cost policies are open for later discussion.
- Non-AI features must continue to work without an AI provider.

## Existing implementation context
Implementation PR #64 introduced optional AI-assisted recording identification and an `IIdentificationAiClient` seam but reported no registered concrete AI provider. This principle guides future integration; no immediate refactor is required.

## Rationale
Keep business features independent of model vendors and allow model choice to follow task requirements.
