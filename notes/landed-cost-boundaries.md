# Testing the Edges of a Landed Cost

A confirmed zero-dollar fee and a missing fee lead to different decisions for a buyer. The calculator needs to preserve that difference.

## Make Each Amount Visible

A vehicle’s dealer price covers the purchase. A buyer comparing cars across borders also needs inland transport, ocean freight, and import fees. In this illustrative order, a $12,000 car needs $450 of inland transport and $850 of ocean freight. With a confirmed zero import fee, the estimate comes to $13,300.

If the fee field is blank, the buyer still needs that figure to compare the final price. Automatically filling a blank with zero would make an incomplete quote look ready to accept. The input and the calculation therefore need a way to carry an unknown value all the way to the screen.

## Exercise the Boundary in Cents

The example accepts USD amounts in whole cents after the form has parsed them. Adding integer cents gives an exact result. The form can format the total in dollars at the end. A negative amount or a fractional cent raises a validation error. A missing amount leaves the estimate incomplete.

The two assertions change just the last input. For a third test, enter a fee of one cent and expect the total to increase by exactly one cent. A useful companion test supplies a blank fee and a negative freight charge together. The invalid charge should still reach the operator as an error.

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

An estimated fee can change after a car is purchased. That change belongs to a revised estimate with its own inputs and calculation time. A shipment advances when a transport event occurs, such as departure from the origin port. Each update needs an identifiable source.

I would test those paths together. Save a revised fee for a purchased car and check that its current milestone still reads “purchased.” Then deliver the same departure event twice and check for one milestone and one customer notification. The buyer can look up the estimate they accepted at purchase and the latest confirmed shipment event independently.
