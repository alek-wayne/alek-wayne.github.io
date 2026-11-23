# Easy Car Imports

A WordPress platform that combined 12 U.S. dealer inventory feeds with landed-cost estimates, online orders, and shipment tracking for buyers in Africa.

Role — Founder & Full-Stack Developer
Period — Sep 2021 – Jul 2023
Focus — 12 U.S. dealer feeds, 4 cost components, Shipment milestones

## Seeing the Delivered Price

The dealer’s asking price covered the vehicle. Getting it to the destination port added transport and import fees. I showed the dealer price and the landed-cost estimate on each listing so buyers had both figures before ordering.

## Synchronizing Dealer Inventory

I launched the business in Lagos and wrote scripts that synchronized 12 U.S. dealer inventory feeds into one WordPress catalog. The listings updated as dealer stock changed, and buyers placed orders through the same site.

## Calculating Landed Cost in Cents

The portfolio calculator parses dealer price, inland transport, ocean freight, and import fees into whole USD cents. It sums integers to avoid floating-point drift, capping each input at one quarter of JavaScript’s maximum safe integer. The UI formats the total in dollars.

## Validating Missing and Invalid Inputs

With the other costs filled, a confirmed $0 import fee yields a total. A blank fee leaves the estimate incomplete. A negative charge or fractional cent raises a validation error even when another field is blank, so a missing fee never hides an invalid charge.

## Separating Quotes from Shipment Progress

The portal tracked vehicles from acquisition to port delivery and notified buyers at recorded milestones. A fee revision belongs in a new estimate with its own timestamp, preserving the accepted quote. The companion note specifies an integration test for fee revisions and duplicate departure events.

[Read Edge Cases in Landed-Cost Pricing](https://alekwayne.dev/notes/landed-cost-boundaries/)

[Open the Interactive Example](https://alekwayne.dev/work/easy-car-imports/#demo)
