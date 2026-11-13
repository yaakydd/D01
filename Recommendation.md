# Kloud Kart: Data Strategy Recommendation

Kloud Kart should build a modest managed cloud data warehouse using a MySQL read replica as its reporting data source. The aim is to produce consistent business reports, protect the live website from reporting workloads and improve control over customer information without introducing unnecessary technology or costs.

## 1. Architecture and Tools

Kloud Kart should establish a MySQL read replica using the already approved second server. This replica will serve as the reporting data source, separating large reporting queries from the live website's database. Before relying on it, the Data Engineer should test its performance and replication delay. Reporting extracts should run outside busy periods and use incremental updates where practical.

Load the permitted reporting data into a modest managed cloud data warehouse. A warehouse is the best fit because Kloud Kart has approximately 40 GB of mainly structured data, its reporting requirements are already understood, and it has only two data hires.

A data lake would introduce storage and data-management work that the company does not currently need. A lakehouse would provide additional capabilities for more varied data and advanced analytics, but those capabilities would add complexity without a clear business benefit. Neither is justified at Kloud Kart's current size.

Use a hybrid ETL/ELT approach. Remove or mask personal information that is not required for reporting before it enters the warehouse. Then use SQL inside the warehouse to organise the permitted data and calculate business figures. This reduces unnecessary copies of personal information while allowing reporting calculations to be changed when business requirements change. Any personal information that remains in the warehouse must still be covered by appropriate access, retention and deletion procedures.

Keep the tools simple:

- MySQL read replica for reporting extraction.
- Managed cloud warehouse for reporting data.
- SQL for data transformations and calculations.
- Limited Python for automation where SQL is insufficient.
- Scheduled jobs and basic failure alerts.
- One business intelligence tool for reports and dashboards.

Spark and a large modern data stack are unnecessary for the current data size and team. Kloud Kart should introduce additional tools only when a clear business requirement justifies their cost.

## 2. Processing Approach

Use scheduled batch processing for most business reporting, with daily updates. Revenue, customer and management reports do not need second-by-second updates. They need accurate and consistent figures delivered at an agreed time.

Do not introduce streaming across the business simply because investors have requested real-time analytics. Continuous processing would increase infrastructure costs, monitoring requirements and operational complexity, placing unnecessary pressure on a two-person data team.

Stock availability is the exception to the daily reporting schedule, but this does not require a separate streaming analytics system. The live transactional MySQL database must remain the source of truth for stock. When a customer places an order, the live ordering system must check and update the current inventory records. The warehouse must not be used to approve orders or determine available stock because its figures may be outdated.

## 3. People and Responsibilities

Kloud Kart should hire two people in the following order:

### First hire: Data Engineer

The Data Engineer should be hired first because the company needs a safe way to extract data without affecting the live website.

During the first 90 days, this person should:

- Establish and test the MySQL read replica using the approved second server.
- Move reporting extracts away from the live database.
- Establish the initial warehouse and safe data-loading processes.
- Introduce scheduled jobs and basic monitoring to identify failed updates.

### Second hire: Analytics Engineer

The Analytics Engineer should follow because the company needs consistent reporting once safe data extraction is established.

During the first 90 days, this person should:

- Work with Nana and Finance to agree on how revenue and other important business figures are calculated.
- Organise the reporting data using the agreed definitions.
- Check that reports produce consistent figures.
- Deliver the first shared Monday reports to Nana and Finance.

Management and the relevant departments must remain responsible for customer-data governance. The two hires should implement and maintain the technical controls, but legal accountability remains with the company.

## 4. Main Trade-offs and Alternatives

The strongest alternative is to use the read replica with scheduled SQL reports and no warehouse. This would be cheaper, involve fewer systems and reduce the number of locations containing personal data. However, as reporting requirements grow, calculations and reporting logic could become spread across separate scripts and reports.

I recommend the modest warehouse because it provides one dedicated environment for organising reporting data and maintaining consistent business calculations. Kloud Kart accepts the additional hosting and data-management costs in exchange for a more controlled reporting environment. This is not a claim that a warehouse is essential for 40 GB of data; it is a decision to establish a shared reporting foundation that can support the company's expected growth.

I reject a full data lake or lakehouse because Kloud Kart does not currently have the varied data, advanced analytics requirements or team capacity to justify them. I also reject streaming for general reporting because daily updates are sufficient for most business decisions, while the live transactional system already handles the requirement for current stock information.

If investors increase pressure for real-time analytics, Kloud Kart should first identify which business decision requires faster information. It can continue to protect stock freshness through the live ordering system while considering faster reporting only where its business value justifies the additional cost.

## 5. Cost and Immediate Priorities

The main costs will fall into three areas:

- **Initial setup costs:** Establishing the read replica, configuring the warehouse and building the first reporting processes.
- **Recurring technology costs:** The additional server, warehouse usage, business intelligence licences and basic monitoring.
- **Staffing costs:** Salaries for the Data Engineer and Analytics Engineer, which will be major ongoing expenses.

The second server is already approved, but its provisioning and running costs must still be included. Exact amounts should be confirmed through salary estimates and vendor quotations before committing to a platform. Kloud Kart should start with a small warehouse allocation, avoid unnecessary scheduled queries and review monthly usage and costs before increasing capacity.

Customer-data protection and the DPC complaint must be addressed immediately and in parallel with the technical work. Kloud Kart should investigate the complaint, identify the information involved and locate relevant copies across known systems. It must assess what should be deleted and what may legitimately need to be retained, carry out the required actions and document the evidence. Management should assign departmental owners and establish procedures for future access and deletion requests. The company must submit its response within the 90-day deadline.

**Expected Result:** Kloud Kart will have more reliable business reports, reduced risk of reporting work slowing down the live website and better control over customer information. It will achieve these improvements using a small, manageable data environment that fits its current size, budget and available staff.  