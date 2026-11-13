# Kloud Kart: Data Strategy Recommendation

Kloud Kart should first move reporting off the live shop and agree one definition of its key figures. It should then build a modest managed data warehouse fed from a MySQL read replica, updated once a day. Stock decisions stay in the live database. This gives Nana and Finance one trusted set of figures, stops reporting slowing the website, and gives the company a controlled place to account for customer data. It fits about 40 GB of structured data, about 4,000 orders a day and one developer.

## 1. Architecture and Tools

Use four parts and no more. Each extra part is another failure point for two hires to support.

- **MySQL read replica** on the approved second server. Large reporting queries run here, not on the live database. It is not running yet, so nothing is fixed until its speed and delay behind the live data are tested.
- **Scheduled extract with a failure alert.** Extraction is what took the website down twice. It runs outside busy periods, reads from the replica, and copies only changed rows.
- **Modest managed warehouse**, where the agreed calculations are written in SQL.
- **One business intelligence tool** for shared reports.

**Why a warehouse, not size.** Forty GB is small, so size does not justify it. The reason is control: one place for agreed definitions and one designed place where customer data can be found and deleted. For structured data, known reporting questions and two hires, a modest warehouse is proportionate. A lake or lakehouse is rejected because Kloud Kart has no varied data or machine-learning need. Definitions are not yet agreed, so the warehouse is built only after they are.

**Privacy.** Mask or remove personal information that reporting does not need before it enters the warehouse, then calculate in SQL. The warehouse is another copy of customer data, so a deletion request must reach it, and "keep everything raw forever" is not acceptable. Retention periods need management and legal advice. No Python is planned unless SQL cannot do a task.

## 2. Processing Approach

Use daily batch processing. The test is: what decision changes if this number is ten seconds old instead of twenty-four hours old? For revenue, customer and management reports, none does. Streaming runs constantly, is harder to debug and needs someone on call, so for two hires it is unstaffable.

**Stock is the one exception, and needs no streaming system.** The live MySQL database stays the source of truth, and placing an order checks and updates stock there. The warehouse never approves orders, because its figures can be a day old.

**Answer to investors asking for real-time analytics:** "Which decision, made by whom, is late today? Today it is the Monday figure, which Nana rebuilds by hand and which does not match Finance's. One agreed figure ready every morning fixes that. If you name a decision needing data fresher than a day, we will cost it and add it."

## 3. People and Responsibilities

Agreeing the definitions of revenue, completed orders and cancellations is cheap, needs no hire and unblocks everything, so it happens first, in Q1, between Nana, Finance and a management sponsor (assumption: they are available). The warehouse is harder to reverse, so it follows.

**First hire: Data Engineer**, because reporting is slowing the shop now. Replica work should start in Q1 even if hiring slips (assumption: the existing developer can begin it). In 90 days:

- The Monday extract runs from the replica, with before-and-after site timings to show Nana and the board.
- The replica's delay is measured and written down.
- A failed update alerts a named person the same day.

**Second hire: Analytics Engineer**, at the start of Q2 (assumption). In 90 days:

- The agreed definitions are written into the warehouse.
- One full month of Nana's and Finance's figures is reconciled, with every difference explained.
- The first shared Monday report is published, and Nana opens it herself.

**Customer data.** Management names an accountable person now. The hires build and maintain the technical controls.

## 4. Main Trade-offs and Alternatives

**Strongest alternative: replica plus scheduled SQL reports, no warehouse.** Cheaper, fewer systems, fewer copies of customer data. I reject it because reporting logic would spread across scripts with no single governed home for definitions. I accept the cost of another system, another copy of customer data, a charge each time something runs, and a skill nobody here has used. If I am wrong, the company pays for a warehouse a replica report could have replaced. At the Q2 checkpoint, if replica reports already give Nana and Finance the same figure and nobody needs more, I would hold the warehouse.

**Operations-only data mart.** Rejected: Finance needs the same figures, and a mart for one department risks two versions of the truth. This is my reasoning from the case, not a course finding.

**Streaming for general reporting.** Rejected for the reasons above, and reconsidered only if a named decision needs fresher data and its cost is justified.

## 5. Cost and Immediate Priorities

There are no quotes yet, so I give no total. Exact amounts must come from salary estimates and vendor quotations before a platform is chosen.

- **One-off:** setting up the replica, warehouse and first reports.
- **Recurring:** the second server, warehouse usage (charged each time something runs), the reporting tool, monitoring.
- **Staffing:** two salaries, the largest ongoing cost.

For comparison, Nana's manual rebuild is about five working weeks a year, on my placeholder of four hours a week (Deliverable 1). Start with a small warehouse allocation, avoid unnecessary refreshes, and review cost monthly.

**The DPC complaint cannot wait for the hires.** As I understand Act 843, and not as legal advice, management must investigate, find every copy of the customer's data, assess what must be deleted and what may lawfully be kept (an assumption needing legal advice), document the actions, and respond within 90 days.

**Expected result:** One set of figures for Nana and Finance, reporting off the live shop, and customer data the company can account for, in a setup two hires can run.
