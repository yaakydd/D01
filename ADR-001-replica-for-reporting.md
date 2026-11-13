# ADR-001: Provision a second server and use a MySQL read replica for reporting

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Kloud Kart leadership

## Context

Kloud Kart stores orders, inventory and customer accounts in one MySQL database on the same server as its live website. Large Monday reporting exports have slowed the website twice in one month because reporting queries compete with live operations for server resources.

The company has approval to provision a second server or establish a read replica. However, this does not mean the second server or replica is already running. The company has only two data hires, so the solution must also be manageable by a small team.

## Decision

Provision the approved second server and configure a MySQL read replica for reporting. Direct reporting queries and data extracts to the replica, while keeping the production database responsible for live website operations and stock transactions.

## Alternatives considered

### Alternative A: Keep reporting on the production database and schedule or throttle exports

- **How it would work:** Continue using the existing database for reporting, but run large exports during quieter hours and limit the resources they consume.
- **Why it is attractive:** It avoids the cost of another server, requires no replication setup and does not create another copy of customer information. It could also be implemented more quickly.
- **Why rejected:** Kloud Kart has already experienced two website slowdowns caused by reporting work. Scheduling exports for quieter hours reduces the likelihood of another slowdown but does not remove the competition for resources. As order volumes grow, the problem could return.

### Alternative B: Extract data directly from production into a managed cloud warehouse

- **How it would work:** Connect the warehouse extraction process directly to the production MySQL database and load reporting data into the warehouse on a schedule.
- **Why it is attractive:** It establishes a dedicated reporting environment immediately and avoids the need to operate a separate MySQL replica.
- **Why rejected:** The extraction process would still place reporting workloads on the database that supports the live website. The warehouse would separate reporting after the data has been extracted, but it would not prevent extraction itself from affecting production. Establishing the replica first addresses that risk.

## Consequences

- **What this buys:** Reporting queries and large exports are separated from the production database. This reduces the risk of reporting work slowing down the live website and provides a separate source from which permitted data can be loaded into the reporting warehouse.

- **What this costs:** Kloud Kart must pay to provision and operate the second server. The team must configure and monitor replication, investigate failures and manage another copy of customer information. The additional copy increases the company's data-protection and deletion responsibilities.

- **What it costs the client if I am wrong:** If the replica cannot handle reporting workloads or repeatedly falls behind, Nana may still receive delayed reports and have to rely on manual exports. If reporting uses outdated data without showing its last update time, management could make decisions using figures that no longer reflect the latest transactions.

- **What would make me revisit this:** Revisit the design if replication repeatedly falls behind, the replica cannot support reporting demand, or its maintenance becomes too difficult for the two-person data team. A significant increase in reporting demand during the Nigeria expansion may also justify reviewing the architecture.

## What this survives

This decision allows reporting activity to grow without deliberately increasing reporting workloads on the production database. It provides separation between the live shop and reporting as order volumes increase and the Nigeria operation develops. It does not guarantee that the replica is always up to date, so replication must be monitored and live stock decisions must remain on production.