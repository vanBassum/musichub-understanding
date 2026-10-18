# Configurable identification decision strategies

Decision: An identification resolver orchestrates identification through a common service interface. Dependency injection selects one of two implementations or interchangeable strategies according to application configuration: a deterministic rule-based resolver and an optional AI-driven resolver. Both use the same independent identification tools and share the same request/result contract. The rule-based implementation works without any AI provider. The AI implementation requires an appropriately configured AI model; missing configuration must not silently cause unidentified files to be identified.

The AI strategy may decide which tools to invoke, whether more evidence is needed, and which identity to propose. Structured actions and outcomes are validated by ordinary code, but code cannot judge the AI's semantic reasoning. Avoid premature numerical thresholds. AI providers, credentials, multiple models and model-selection hierarchy are a separate future design topic; identification may refer to a configured model without prescribing that hierarchy.

Unresolved: exact identification result schema, source integrations, rule heuristics, AI-provider configuration, and catalog linking. No database changes in this slice.
