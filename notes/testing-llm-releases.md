# Three checks before an AI release

A shipment-status fixture shows how to check an assistant’s reply, the supporting record, and the action it took.

## Start with one answer you can check

Suppose a broker asks whether shipment S17 has arrived. The tracking record says it is in transit. The assistant returns valid JSON with the right shipment ID and says it has been delivered. An operator who trusts that answer could close a load early.

For this example, the fixture contains the tracking record, the assistant’s reply, and the tool calls captured by the test runner. Each comes from a different part of the interaction. Keeping them separate lets us check what the assistant said against the evidence it received and the actions it took.

## Check structure, support, and action

The first check requires two fields with string values. The second compares the shipment ID and status with the source record. The third reads the tool trace. This request calls for exactly one read-only lookup. An extra call should surface in the report even when the final answer looks correct.

Run the illustrative Python fixture below. It prints “supported status” and exits with code 1. Change the status in the reply to “in_transit” and the same fixture passes. Add a second call and the tool check fails independently.

```python
record = {"shipment": "S17", "status": "in_transit"}
reply = {"shipment": "S17", "status": "delivered"}
calls = ["read_status"]

checks = {
    "schema": isinstance(reply, dict)
        and reply.keys() == record.keys()
        and all(isinstance(v, str) for v in reply.values()),
    "supported status": isinstance(reply, dict)
        and all(reply.get(k) == v for k, v in record.items()),
    "tool trace": calls == ["read_status"],
}
failed = [name for name, passed in checks.items() if not passed]
print(", ".join(failed) or "pass")
raise SystemExit(1 if failed else 0)
```

## Give a failed check a consequence

A CI job can use that exit code to fail a required check. I would keep the fixture ID and the failed rule in its report so the reviewer can reproduce the failure. Budgets belong in the report too. An illustrative budget might allow two seconds and half a cent per request. A trace costing $0.006 crosses that cost limit even if the answer is accurate.

Replaying a fixed trace verifies that the gate catches a known regression. Evaluating a new model or prompt takes fresh runs across representative cases. For that comparison, I would record the model version, case set, token counts, pricing date, and elapsed times. Repeated runs show how often a failure occurs. The fixed fixture makes sure yesterday’s failure is still detectable today.
