# Kloud Kart: Data Strategy Recommendation

Kloud Kart should do three things, in this order. First, give reports their own copy of the database, so they stop slowing the shop. Second, agree one written meaning for revenue, completed orders and cancellations. Third, build one shared place for reports that updates once a day. Stock stays in the live shop system. Kloud Kart has about 40 GB of data, about 4,000 orders a day, one developer and money for two data hires, and the plan is sized to that.

## 1. Architecture and Tools

Use four parts and no more. Every extra part is something two new hires must keep running.

- **A separate copy of the live database for reports (a read replica).** The website and database share one server, and a Monday export of a few hundred thousand rows competes with customers for it. That is the likely reason the shop slowed twice last month. The second server is approved but not running, so nothing is fixed until the copy is tested for speed and for how far behind it falls.
- **An automatic daily job** that copies only new and changed records from the copy, never from the live database, and alerts someone if it fails.
- **One shared place for reports (a data warehouse)**, holding the agreed calculations.
- **One reporting tool** that Nana and Finance both open.

**Why a shared place, if 40 GB is small?** Size is not the reason. Even at 15 to 20% growth a year, this stays small. The reason is control. Today two teams calculate the same figure two ways, and customer data sits in untracked files. A shared place gives the calculations one home, and customer data one designed place where it can be found and deleted. It is built only after Nana and Finance agree what their figures mean.

**Larger systems are rejected.** A lake or lakehouse (systems for large amounts of varied raw data) would add work for data Kloud Kart does not have. Machine-learning forecasting stays on the wish list for later.

**Customer data.** Personal details that reports do not need are removed or masked first. The shared place is another copy, so a deletion request must reach it. How long to keep data needs legal advice.

## 2. Processing Approach

Reports update once a day. The test: what decision would change if a figure were seconds old instead of a day old? For revenue, customer and management reports, none would. Updating continuously runs all the time, is harder to fix and needs someone on call, which two hires who also keep a shop running cannot manage.

Stock is the one exception, and it needs no new system. The live database stays the one record the shop trusts, and placing an order checks and updates stock there. Reports never approve orders, because a day-old stock count means selling items Kloud Kart no longer has.

**Answer to investors who ask for "real-time analytics":** "Which decision, made by whom, is late today? Today it is the Monday figure. Nana rebuilds it by hand and it does not match Finance's. One agreed figure ready every morning fixes that. If you name a decision that needs fresher data, we will cost it and add it."

## 3. People and Responsibilities

Agreeing the meaning of revenue, completed orders and cancellations is cheap, needs no hire and unlocks everything else, so it happens first, in Q1, between Nana, Finance and a senior sponsor (assumption: they are available).

**First hire: Data Engineer,** because reporting is hurting the shop now. Work on the copy starts in Q1 even if hiring is late (assumption: the existing developer can begin it). Within 90 days:

- The Monday report runs from the copy, with before-and-after site speed shown to Nana and the board.
- How far behind the copy runs is measured and written down.
- A failed daily update alerts a named person the same day.

**Second hire: Analytics Engineer,** from the start of Q2 (assumption). Within 90 days:

- The agreed meanings are built into the shared place.
- One full month of Nana's and Finance's figures is compared, and every difference explained.
- The first shared Monday report is published, and Nana opens it herself.

**Customer data.** Management names one accountable person now. The hires build and maintain the technical controls.

## 4. Main Trade-offs and Alternatives

**Strongest alternative: the separate copy plus scheduled reports, with no shared place.** It is cheaper, has fewer parts and holds fewer copies of customer data. I reject it because calculations would spread across separate scripts with no single owner of the agreed meanings. I accept another system to run, another copy of customer data to delete from, a charge each time it runs, and a skill nobody here has used. If I am wrong, Kloud Kart pays for something a simple report could have done. I would hold the shared place at the end of Q2 if scheduled reports already give Nana and Finance the same figure and nobody needs more.

**A reporting store for Operations only.** Rejected: Finance needs the same figures, so one department's store risks two versions again. This is my reasoning from the case.

**Continuous updating for all reports.** Rejected for the reasons in section 2, and reconsidered only if someone names a decision that needs fresher data and the cost is justified.

## 5. Cost and Immediate Priorities

No quotes exist yet, so I give no total and will not invent one. Figures must come from salary estimates and supplier quotes before anything is bought.

- **One-off:** setting up the copy, the shared place and the first reports.
- **Running costs:** the second server, the shared place (charged each time it runs), the reporting tool and monitoring.
- **People:** two salaries, likely the largest ongoing cost (my assumption).

To control cost: start small, avoid unnecessary refreshes, and review cost every month.

**The Data Protection Commission (DPC) complaint cannot wait for the hires.** As I understand Act 843, and not as legal advice, management must investigate, find every copy of the customer's data, assess what must be deleted and what may lawfully be kept (an assumption needing legal advice), record what was done, and respond within 90 days.

**Expected result:** One set of figures for Nana and Finance, reports that no longer slow the shop, and customer data the company can account for, run by a team of two.
