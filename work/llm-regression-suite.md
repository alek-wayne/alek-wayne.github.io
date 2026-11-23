# LLM Regression Suite

A Python harness that grades 48 synthetic policy cases, gates pull requests in GitHub Actions, and publishes replayable comparisons.

- [Open the 48-Case Demo](https://alekwayne.dev/llm-regression-suite/)
- [View Source on GitHub](https://github.com/alek-wayne/llm-regression-suite)

Role — Independent developer
Period — Independent project
Focus — Python, Anthropic SDK, React, PostgreSQL, GitHub Actions

## What Counts as a Regression

In CMP-02, the seeded candidate returns the correct mount code, cites the wrong product policy, and promises unsupported compatibility. JSON, decision, and value pass. Attribution and wording fail, and the runtime guard withholds the reply.

## Grading and Runtime Guard

The Python grader checks the JSON contract, decision and value, exact supporting passage IDs, and approved wording. Both fixture runs and the optional Anthropic SDK path use this grader and the same runtime guard.

## Binding Wording to Policy Revisions

The runtime guard requires wording approved for the exact revision of a cited passage. Each approval binds wording to the passage ID, SHA-256 of the policy text, and response decision. Exact matching flags unauthorized promises and also rejects harmless paraphrases.

## Pinning the Baseline

On pull requests, GitHub Actions loads the baseline from the target revision. Request hashes bind each frozen reply to the model ID, prompt, ordered policy passages, and response schema. A change to those inputs makes the old evidence stale.

## Enforcing the Release Gate

The fixture gate fails on any drop in suite accuracy, candidate accuracy below 90%, candidate p95 latency over 5 seconds, or modeled cost over $0.01 on a candidate trial. Missing or stale evidence makes the run inconclusive. Exit codes 1 (failure) and 2 (inconclusive) both fail the required check.

## Reading the Release Evidence

CI replays each case from the saved JSON and verifies the Markdown report before uploading both. On the same 48 cases across 12 policy families, the repaired candidate passes 48/48 and the seeded candidate fails the gate at 40/48. Both runs use synthetic replies, timing, and token counts. Live accuracy, latency, and cost require separate measurement.

[Read the Release Reports](https://github.com/alek-wayne/llm-regression-suite/releases/tag/v1.0.1)

[Open the Interactive Example](https://alekwayne.dev/work/llm-regression-suite/#demo)
