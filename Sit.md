# Deliverable 1: Situation Diagnosis (Kloud Kart)

## 1. Identification, Cost and Ranking of Problems

| Rank | Identified problem              | Potential cost to Kloud Kart                                                                                                                                               | Why it matters to the board                                                                               |
| ---- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| 1    | Poor customer-data governance   | **Exposure:** regulatory, legal and reputational. A cedi range needs legal advice. **Labour:** time spent locating copies. Hours unknown.                                  | A 90-day DPC deadline, and Kloud Kart cannot yet show where the customer's data was held.                 |
| 2    | Website performance slowdowns   | **Direct loss:** orders lost while the site was slow. Number and value unknown. **Labour:** developer time. Hours unknown.                                                 | Monday exports slowed the live site twice in one month, which puts sales and customer confidence at risk. |
| 3    | Inconsistent business reporting | **Labour:** Nana's weekly rebuild, plus any time Finance spends reconciling. Hours unknown. **Exposure:** decisions and investor information based on conflicting figures. | The board cannot tell which figure is right.                                                              |

**Ranking test:** if the problem is still unresolved at the next board conversation, how much would it damage the client's credibility? I looked at three things: a deadline Kloud Kart does not control, whether it is happening now, and how hard the damage is to undo.

## 2. Detailed Problem Analysis

### 2.1 Poor Customer-Data Governance

**Root Cause:**

A customer asked for deletion and complained to the Data Protection Commission. Kloud Kart has 90 days to respond. Marketing holds a list of about 300,000 people, and nobody tracks how many copies exist.

Data leaves the database through ad hoc exports, and the case names no one accountable for customer data (my assumption). So nobody records where the copies are.

Every copy is a place a deletion request must reach. Kloud Kart cannot show that deletion reached all of them, so it is exposed in the complaint.

**Compliance:**

As I understand Act 843, and not as legal advice: controllers of personal data must register with the Commission. Individuals can ask what is held about them and require correction or deletion. The principles include security and keeping data no longer than necessary, which untracked exports arguably breach. Breaches must be notified to the Commission and the people affected. Whether deletion means erasing every transaction record is an assumption that needs legal advice. I cite no cross-border transfer rule for Nigeria, because I understand the Act has none.

**Ranked Findings:**

1. The open complaint, with its 90-day deadline.
2. Untracked exports, which cause the first finding.
3. Registration and breach readiness, both unknown.

**Assumptions:**

- The number and location of copies are unknown.
- It is unknown whether the complaining customer appears in any copy.
- The registration status, the grounds of the complaint and the date the 90 days started are unknown.
- No one is currently accountable for customer data.

**Cost Assessment:**

- **Wasted Labour:** Staff time finding copies. Hours unknown.
- **Direct Loss:** None established.
- **Risk-Weighted Exposure:** No cedi range is possible without legal advice. At the low end, the complaint closes with a documented response. At the high end, it escalates, with legal fees, management time and reputational cost while the company is raising money. The driver is whether Kloud Kart can show every place the data was held and that deletion reached it.

**Risk Ranking Justification:**

First, because it is the only problem with a deadline Kloud Kart does not control, it is open now, and I judge that damage with a regulator is hard to undo.

The strongest case against: the slowdown is the only confirmed, repeating effect on customers. I would swap the two if lost sales per slowdown proved large, or if the complaint proved narrow. It stays first because a slow Monday recovers and a missed deadline does not. Both can be worked on in the same week.

### 2.2 Website Performance Slowdowns

**Root Cause:**

Twice last month, a Monday export of a few hundred thousand rows slowed the live website to a crawl.

The website and the MySQL database share one server, and reporting has nowhere else to run. The second server is approved but not yet running, and Kloud Kart has one PHP/MySQL developer. This is the likely cause. The exact bottleneck is unconfirmed.

An export competes with customers for the same server, which fits both slowdowns. Whether data size alone plays a part is unconfirmed.

**Ranked Findings:**

1. Two slowdowns in one month, confirmed.
2. A shared server, the likely cause.
3. Growth of 15 to 20% a year makes recurrence likely (my judgement).

**Assumptions:**

- The bottleneck, the length of each slowdown and the number of customers affected are unknown.
- Lost orders and average order value are unknown.

**Cost Assessment:**

- **Wasted Labour:** Developer time on incidents. Hours unknown.
- **Direct Loss:** Orders lost per slowdown, times the number of slowdowns, times the average order value. None of these is known, so I give no cedi amount.
- **Risk-Weighted Exposure:** Recurring slowdowns put sales and customer confidence at risk. The size is unknown.

**Risk Ranking Justification:**

Second, because it has a confirmed effect on customers. It ranks below 2.1 because the DPC deadline is outside Kloud Kart's control and damage with a regulator is harder to undo. It ranks above 2.3 because no wrong decision from conflicting reports is confirmed. I would move it to first if lost sales per slowdown proved large.

### 2.3 Inconsistent Business Reporting

**Root Cause:**

Nana's Monday figures, rebuilt from CSV exports, do not match Finance's spreadsheet.

The cause is not established. The likely explanation (my assumption) is that there is no single owned source, so each calculates separately by its own rules. Four explanations are possible, and each is confirmed by a different question: different definitions of revenue (what counts as a sale, and what about cancellations?), different date cut-offs, different extraction times, or manual errors (can either team rebuild the other's figure?).

The board cannot tell which figure is right, which weakens confidence in management reporting and in what is told to investors. Nana also rebuilds her figures by hand every week.

**Ranked Findings:**

1. The mismatch, confirmed.
2. The cause, unknown.
3. Manual rebuilds, which are hard to check.

**Assumptions:**

- The reasons for the differences and the time spent are unknown.
- No decision is confirmed to have been affected.
- Nana is unavailable, so none of the questions above has been answered.

**Cost Assessment:**

- **Wasted Labour:** Nana's weekly rebuild, plus any time Finance spends reconciling. Hours unknown.
- **Direct Loss:** None established.
- **Risk-Weighted Exposure:** Weaker confidence among management and investors. The size is unknown.

**Risk Ranking Justification:**

Third, because it wastes time and creates uncertainty, but no loss or wrong decision is confirmed, it has no outside deadline, and it can be reconciled.

**Conclusion:** Kloud Kart's immediate challenge is not a lack of advanced data technology. The evidence points to missing control over customer information, no separate place for reporting to run, and figures calculated separately for reasons still to be confirmed.
