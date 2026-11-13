# ADR-003: Use scheduled incremental batch processing for warehouse updates

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Kloud Kart leadership

## Context

Kloud Kart needs reliable reporting for revenue, customers and management decisions. Nana currently rebuilds Monday figures from large CSV exports, while Finance produces different figures using spreadsheets.

Most reporting requirements do not need second-by-second updates. The company has only two data hires and must avoid introducing a processing system that requires more monitoring and operational support than the team can provide.

The reporting warehouse will receive permitted data from the MySQL read replica rather than extracting directly from the production database.

## Decision

Use scheduled incremental batch processing to update the reporting warehouse, with daily updates for the main business reports. Load new or changed records where practical instead of repeatedly extracting the full reporting dataset.

## Alternatives considered

### Alternative A: Run a full nightly extract of the reporting data

- **How it would work:** Extract the full reporting dataset from the read replica every night and reload or replace the warehouse data with the latest copy.
- **Why it is attractive:** It is straightforward to understand and implement. The team does not need to track which records have changed since the previous run, and a complete reload can make it easier to produce a fresh copy of the source data.
- **Why rejected:** Repeatedly extracting the full dataset wastes processing time and resources as the database grows. It also creates unnecessary work when most records have not changed. Incremental processing is more suitable for a growing business that wants to control recurring costs.

### Alternative B: Use continuous streaming to update the warehouse

- **How it would work:** Capture database changes continuously and send them to the warehouse as transactions occur, keeping reporting data close to real time.
- **Why it is attractive:** Reports can reflect new transactions much sooner than daily batch processing. This could appeal to investors requesting real-time analytics and support decisions that genuinely depend on current information.
- **Why rejected:** Kloud Kart's main reporting requirements do not currently justify continuous updates. Streaming introduces additional complexity around failed events, duplicates, ordering and monitoring. A two-person data team would have to support this system even though most business reports only need daily updates.

## Consequences

- **What this buys:** Daily incremental updates provide Nana and Finance with consistent reporting without repeatedly extracting the entire dataset. They reduce unnecessary processing and help keep warehouse costs manageable as the business grows.

- **What this costs:** Reports will not show every transaction immediately. The team must also build and monitor processes that identify new or changed records, handle failed runs and prevent records from being loaded incorrectly or more than once.

- **What it costs the client if I am wrong:** If management makes a decision that depends on information more recent than the daily update, it could act on incomplete figures. Nana might present outdated revenue or customer figures, and management could miss a developing business problem because the latest transactions have not yet reached the warehouse.

- **What would make me revisit this:** Revisit the schedule if management identifies a business decision that cannot wait for the next daily update, or if the daily processing window becomes too long to deliver reports on time. Any move towards more frequent processing must demonstrate a clear business benefit that justifies its additional operating and monitoring costs.

## What this survives

Daily incremental batch processing can support growth in order volumes without requiring the company to reload the entire dataset every night. It also gives Kloud Kart a manageable starting point for the Nigeria expansion. If future business requirements demand faster reporting, the company can evaluate more frequent batches or change-capture technology without immediately committing to streaming across the whole data environment.