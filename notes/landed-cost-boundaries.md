# Testing the Edges of a Landed Cost

A confirmed zero-dollar fee and a missing fee lead to different decisions for a buyer. The calculator needs to preserve that difference.

## Make Each Amount Visible

A vehicle’s dealer price covers the purchase. A buyer comparing cars across borders also needs inland transport, ocean freight, and import fees. A $12,000 car with $450 in inland transport and $850 in ocean freight comes to $13,300 when the import fee is confirmed at zero.

If the fee field is blank, the buyer still needs that figure to compare the final price. Automatically filling a blank with zero would make an incomplete quote look ready to accept. The input and the calculation therefore need a way to carry an unknown value all the way to the screen.

## Exercise the Boundary in Cents

After parsing form inputs into whole USD cents, the calculator sums integers and formats the total in dollars for display. Negative amounts and fractional cents raise a validation error, while a missing amount leaves the estimate incomplete.

The two assertions change only the fee. Add a one-cent fee and assert that the total rises by exactly one cent. Then combine a blank fee with a negative freight charge and assert a validation error.

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

## Keep Price Changes Separate from Order Progress

A fee revision after purchase belongs to a new estimate with its own inputs and calculation time. A shipment advances when a transport event occurs, such as departure from the origin port. Each update needs an identifiable source.

Save a revised fee for a purchased car and assert that its milestone still reads “purchased.” Deliver the same departure event twice to test idempotency and expect one milestone and one notification. The buyer looks up the estimate accepted at purchase and the latest confirmed shipment event independently.
