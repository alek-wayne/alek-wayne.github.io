# LLM Regression & Guardrail Testing Suite

A Python evaluation harness that turns model responses into repeatable checks and reports regressions in continuous integration.

- [Open the 48-Case Demo](https://alekwayne.dev/llm-regression-suite/)
- [View Source on GitHub](https://github.com/alek-wayne/llm-regression-suite)

Role — Independent developer
Period — Independent project
Focus — Python, Anthropic SDK, React, PostgreSQL, GitHub Actions

## What Counts as a Regression

A response can read well and still omit a required field, make an unsupported claim, or cost too much for the task. Each failure needs a specific expectation that a developer can inspect after a run.

## The Evaluation Harness

I built the harness in Python with the Anthropic SDK. Its 30+ structured test cases cover JSON schema compliance, hallucination guardrails, latency, and token cost. Each case gives the runner a concrete expectation for the response it receives.

## Choosing What to Assert

Field names and value types give a schema check a precise answer. A factual check needs a source fact for comparison. Applying exact sentence matching to every response would reject valid paraphrases, so the useful comparison depends on the contract the application actually needs.

## Catching a Change Before Release

I connected the results to GitHub Actions so a drop in accuracy fails the build and publishes a pass/fail report. The failed case gives the developer a place to start investigating which input or expectation changed.

## Reading the Six Example Cases

The portfolio inspector uses six synthetic fixtures to make individual outcomes reproducible. You can inspect the supplied response and the rule behind each verdict. Measuring a model’s current accuracy, latency, or cost would require fresh calls across a representative test set.

[Open the Interactive Example](https://alekwayne.dev/work/llm-regression-suite/#demo)
