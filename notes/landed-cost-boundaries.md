# Edge Cases in Landed-Cost Pricing

A confirmed $0 import fee completes the estimate when other costs are known. A missing fee keeps it incomplete from input to display.

## Surface Every Cost Input

A dealer’s asking price covers the vehicle. Landed cost also includes inland transport, ocean freight, and import fees. With a $12,000 vehicle, $450 in inland transport, and $850 in ocean freight, a confirmed $0 import fee produces a $13,300 estimate.

Coercing a blank fee to zero makes an incomplete estimate look ready to accept. The form keeps a blank fee unknown and leaves the estimate incomplete. The Python function below represents the same unknown input as None.

## Test Boundaries in Whole Cents

The calculator parses USD inputs into whole cents and sums integers to avoid floating-point drift. The display formats the final total in dollars. The Python function rejects negative values and fractional cents before it returns None for missing inputs.

Both assertions vary only the import fee. Add one cent and assert that the total rises by exactly one cent. Pair a blank fee with a negative freight charge and assert a validation error, which takes precedence over an incomplete result.

```python
def landed_cents(dealer, inland, ocean, fees):
    amounts = (dealer, inland, ocean, fees)
    for value in amounts:
        if value is None:
            continue
        if type(value) is not int or value < 0:
            raise ValueError("Use nonnegative whole cents")
    return None if None in amounts else sum(amounts)

car = (1_200_000, 45_000, 85_000)
assert landed_cents(*car, 0) == 1_330_000
assert landed_cents(*car, None) is None
```

## Decouple Quote Revisions from Shipment Progress

Preserve the quote accepted at purchase. Record each later fee revision as a new estimate with its own inputs and timestamp. Update shipment progress on confirmed transport events and keep the source of each event.

Verify both rules in one integration test. Save a revised fee and assert that the milestone stays “purchased.” Deliver the same port-departure event twice to test idempotency, expecting one milestone update and one buyer notification. Verify that the accepted quote and latest confirmed shipment milestone remain independently accessible.
