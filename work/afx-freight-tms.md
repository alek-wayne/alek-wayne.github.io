# AFX Freight TMS

A freight brokerage TMS that separates rate quoting from booking eligibility across React portals, an Express API, and PostgreSQL.

Role — Software Development Associate · Melton Truck Lines
Period — Jan 2025 – Oct 2026
Focus — React, Node.js, Express, PostgreSQL, Anthropic SDK

## Quoting Before Cargo Review

Shippers sometimes submit a rate request before confirming cargo weight. I built separate rating and booking checks, so a request with enough inputs for a rate retains that result while the booking decision goes to review.

## The System I Built

I built the React shipper and carrier portals and their Express API at Melton Truck Lines. The work spanned 18 PostgreSQL tables and 35+ REST endpoints. I worked with engineering staff and leadership to turn brokerage rules into acceptance tests.

## Separating Rate Quotes from Booking Eligibility

The server checks rate inputs and cargo requirements independently. If the rate is available and the cargo check calls for review, the interface displays the quote and the review status together.

## Authorizing Access in Express

Shippers and carriers use different workspaces over a shared backend. Express checks the caller’s role and the scope of the requested record before returning load details, so access decisions stay on the server.

## Reading Shared Load Records

PostgreSQL stores quote records, loads, and tracking events separately. The portals read load details through the same API, so each view draws shipment status from the shared records.

## Computing Activity Before Summarizing

Application code computes activity counts and seven-day averages before requesting a briefing through the Anthropic SDK. The offline replay used eight sample quote requests against an average of four. A valid reply produced a briefing. An empty reply raised a warning and produced no briefing.

## Checking Deployments and Booking Rules

I set up Git-based releases for the React frontend on Vercel and the Express API on Railway. Health checks verify the deployed service responds. Booking-policy tests separately verify how the code classifies incomplete cargo.

## Verifying the Quote Boundary

I replayed one fictional dry van load with a fixed market input and changed only the weight field. Both inputs returned a $2,300 rate. The 18,000 lb input cleared the cargo check, and the missing-weight input moved the booking decision to operator review.

[Read Three Checks Before an AI Release](https://alekwayne.dev/notes/testing-llm-releases/)

[Open the Interactive Example](https://alekwayne.dev/work/afx-freight-tms/#demo)
