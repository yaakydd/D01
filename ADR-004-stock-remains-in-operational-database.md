# ADR-004: Keep live stock availability and order decisions in the production MySQL database

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Kloud Kart leadership

## Context

Kloud Kart has a strict requirement that stock counts must not go stale because outdated stock information could cause the company to accept orders for products it no longer has.

The proposed architecture separates reporting from the live website using a MySQL read replica and a managed cloud data warehouse. Both the replica and warehouse may receive updates after transactions occur, meaning their information can temporarily differ from the latest production records.

The company must protect reporting performance without allowing reporting systems to determine whether a customer can successfully purchase an item.

## Decision

Keep the production MySQL database as the source of truth for stock availability. The live ordering system must check and update current inventory records when an order is placed. Neither the read replica nor the reporting warehouse will approve orders or determine available stock.

## Alternatives considered

### Alternative A: Use the MySQL read replica for stock availability checks

- **How it would work:** Direct stock availability queries from the live website to the read replica, reducing read traffic on the production database.
- **Why it is attractive:** It reduces some workload on the production database and allows the website to read stock information from a separate server. If replication is fast, the replica may often show figures close to the latest stock counts.
- **Why rejected:** Replication can introduce delays between a stock change in production and the same change appearing on the replica. During that delay, a customer could see an item as available even though another order has already reduced the stock. This creates an unacceptable overselling risk.

### Alternative B: Use the reporting warehouse as the central source for stock availability

- **How it would work:** Copy inventory data into the warehouse and allow the website or another service to use the warehouse's stock figures when checking product availability.
- **Why it is attractive:** It centralises inventory information alongside sales and customer reporting data. It could also make it easier to analyse stock movement and sales trends in one reporting environment.
- **Why rejected:** A reporting warehouse is designed to support analysis, not to guarantee the latest stock position during a live purchase. Its scheduled updates would make its inventory figures unsuitable for approving customer orders. Using it in this way could cause overselling and customer complaints.

## Consequences

- **What this buys:** Customer orders are checked against the current operational stock records rather than potentially outdated reporting data. It protects the business from using delayed warehouse or replica figures to make live purchasing decisions.

- **What this costs:** The production database continues to handle stock availability checks and inventory updates. This means some operational workload remains on the production system, and the company must ensure that its ordering process handles simultaneous purchases correctly.

- **What it costs the client if I am wrong:** If the production stock process does not correctly check and update inventory during simultaneous orders, two customers could purchase the same remaining item. Nana could face overselling, refunds, customer complaints and damage to the company's reputation. Keeping stock on production does not automatically guarantee accuracy; the ordering process must be tested.

- **What would make me revisit this:** Revisit the implementation if the production database cannot handle the stock workload as order volumes increase, or if the Nigeria expansion introduces inventory requirements that the current system cannot safely support. Any proposed change must demonstrate that stock availability remains accurate during simultaneous purchases before it is approved.

## What this survives

This decision protects stock accuracy while allowing the company to expand its reporting environment. The warehouse and read replica can grow to support additional reports without becoming responsible for approving live orders. If order volumes increase, Kloud Kart can improve the operational inventory process separately, provided the production system remains the trusted source of current stock information.