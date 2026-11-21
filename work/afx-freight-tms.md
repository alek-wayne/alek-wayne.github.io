# AFX Freight TMS

A freight brokerage platform that turns a shipment request into a quote and gives operators a clear point to review incomplete cargo details.

Role — Software Development Associate · Melton Truck Lines
Period — Jan 2025 – Oct 2026
Focus — React, Node.js, Express, PostgreSQL, Anthropic SDK

## From shipment request to booking

A shipper starts with an origin, a destination, equipment, and cargo details. The brokerage needs to price the shipment and decide whether it has enough information to proceed. Those two decisions can have different answers for the same request.

## The system I built

I built the React shipper and carrier portals and the Express API behind them. During my work at Melton, the system spanned 18 PostgreSQL tables and 35+ REST endpoints. I worked with engineering staff and leadership to turn brokerage requirements into technical specifications and acceptance tests.

## Keeping pricing and eligibility separate

The server calculates the price and evaluates cargo eligibility separately. That gives a shipper a useful estimate even when an operator still needs to clarify part of the request. The interface can show a calculated amount and a request for more information at the same time.

## A one-input replay

I replayed a fictional Tulsa-to-Dallas dry van request for 12 pallets of machine parts at 18,000 lb. With a fixed market input, the pricing engine returned $2,300 and marked the request eligible. Removing only the weight produced the same $2,300 quote and sent the booking decision to operator review.

## Checking an AI briefing

Application code calculates recent activity before asking the model to summarize it. In an offline replay, the sample day had eight quote requests against a seven-day average of four. A valid simulated response produced a briefing. An empty response raised a warning and produced no briefing. Judging the quality of the writing would require real model outputs.

[Open the interactive example](https://alek-wayne.github.io/work/afx-freight-tms/#demo)
