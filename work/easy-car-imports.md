# Easy Car Imports

A vehicle sourcing and ordering platform that brings U.S. dealer inventory, landed-cost estimates, and delivery milestones into one buyer workflow.

Role — Full-Stack Web Developer & Platform Creator
Period — Sep 2021 – Jul 2023
Focus — Inventory synchronization, Pricing calculations, Boundary testing, Order tracking

## The buyer’s question

For buyers in Africa comparing U.S. dealer listings, the advertised price covered only the vehicle. The decision to place an order depended on the cost of getting that vehicle to the destination port.

## From listings to orders

I built the sourcing and ordering platform and wrote synchronization scripts for 12 U.S. dealer inventory feeds. My work followed the order beyond the listing page, through the price estimate, customer tracking, and milestone notifications.

## Keeping four costs visible

The calculator combines the dealer price, inland transport, ocean freight, and import fees. Keeping those inputs separate made a revised freight estimate traceable. I could change one charge and check exactly how it moved the preorder total.

## Testing the boundary

I used boundary-value tests to validate preorder totals. One illustrative check holds three inputs constant and sets inland transport to zero. The total should fall by exactly that charge. An unknown transport charge needs a separate case because silently treating it as zero would understate the estimate.

## After the order

The customer portal followed a vehicle from acquisition to destination-port delivery. Milestone notifications gave buyers a specific event to follow up on. Between recorded events, the last confirmed milestone was the information the platform could support.

[Open the interactive example](https://alek-wayne.github.io/work/easy-car-imports/#demo)
