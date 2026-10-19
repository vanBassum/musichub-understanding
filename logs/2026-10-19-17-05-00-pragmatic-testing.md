# Decision: proportionate automated testing

Status: accepted by owner on 2026-10-19.

Context: New UI testing infrastructure for the upload queue raised concern that test effort could grow out of proportion to product development.

Decision:
- Test effort is proportional to the risk and complexity of the behavior.
- Prioritize critical business logic, concurrency, cancellation, integrity/data-loss risks and complex state transitions.
- Do not require exhaustive tests for trivial UI components, labels, straightforward wiring or simple presentation.
- Reuse existing test tools and tests; avoid expanding frameworks or infrastructure without clear benefit.
- Passing existing CI/review gates remains required. Tests are not a goal in themselves and must not impose disproportionate maintenance cost.
- Vitest is explicitly approved as a devDependency for the upload queue tests; its introduction does not imply blanket unit-test coverage for all frontend code.

Rationale: Preserve confidence in failure-prone behavior without letting testing overhead dominate feature delivery.

Boundary: This does not waive tests for significant risks or authorize weakening existing required checks.
