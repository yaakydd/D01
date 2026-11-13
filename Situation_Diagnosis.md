# Deliverable 1: Situation Diagnosis(Kloud Kart)

## 1. Identification, Cost and Ranking of Problems

| Rank | Identified problem | Potential cost to Kloud Kart | Why it matters to the board |
|---|---|---|---|
| 1 | Poor customer-data governance | Staff time spent locating customer information and responding to deletion requests, alongside potential regulatory, legal and reputational exposure. | The DPC complaint gives Kloud Kart 90 days to respond. The company must demonstrate that it can locate and manage customer data wherever relevant copies exist. |
| 2 | Website performance slowdowns | Potential lost orders, customer dissatisfaction and developer time spent investigating performance incidents. | Monday exports have slowed the live website twice in the last month, creating a risk to sales and customer confidence. |
| 3 | Inconsistent business reporting | Staff time spent rebuilding and reconciling reports, alongside the risk of decisions based on conflicting figures. | Nana's figures do not match Finance's figures, weakening confidence in management reporting and information presented to investors. |

## 2. Detailed Problem Analysis

### 2.1 Poor Customer-Data Governance

**Root Cause:**

Marketing exports a customer list containing approximately 300,000 people without tracking how many copies exist or where they are stored. This reveals a lack of ownership and control over how personal data is distributed, stored and retained. Consequently, Kloud Kart may struggle to locate relevant customer information and demonstrate how deletion requests have been handled.

**Compliance:**

The Ghana Data Protection Act, 2012 (Act 843) requires organisations controlling personal data to register with the Data Protection Commission and comply with principles covering lawful processing, openness, purpose limitation, data minimisation, accuracy, storage limitation, security and individual rights.

Customers can request access to, correction of or deletion of their personal data. However, a deletion request does not automatically require every record associated with a customer to be erased. Kloud Kart must assess what should be deleted and what may legitimately need to be retained.

The concern is that untracked exports make it difficult to identify and assess all relevant copies. This is urgent because the company has 90 days to respond to the Data Protection Commission complaint and demonstrate how the customer's request was handled.

**Ranked Findings:**

1. The Data Protection Commission complaint creates immediate compliance pressure because of the 90-day response window.
2. Marketing's untracked exports make it difficult to identify where customer information is stored.
3. The absence of a reliable copy inventory makes it harder to demonstrate appropriate handling of deletion requests.

**Assumptions:**

- The number and locations of customer-data copies are unknown.
- It is not confirmed whether the customer involved in the complaint appears in Marketing's exports, Nana's CSV files, Finance's spreadsheets, email attachments or backups.
- Kloud Kart's DPC registration status is unknown.
- The precise grounds of the complaint have not been established.

**Cost Assessment:**

- **Wasted Labour:** Staff time spent locating customer information, investigating data copies and responding to deletion requests, taking time away from their other responsibilities.
- **Direct Loss:** No direct financial loss has been established.
- **Risk-Weighted Exposure:** Kloud Kart faces potential regulatory, legal and reputational consequences if it cannot demonstrate appropriate control over customer information. The financial impact cannot be reliably quantified without further evidence.

**Risk Ranking Justification:**

This problem ranks first because the active Data Protection Commission complaint creates a defined 90-day response deadline, while Kloud Kart lacks a reliable way to account for customer-data copies. Failure to address this weakness could undermine the company's ability to demonstrate accountability and could make future data systems harder to govern.

### 2.2 Website Performance Slowdowns

**Root Cause:**

Kloud Kart hosts its live website and MySQL database on the same server. Nana's Monday exports retrieve hundreds of thousands of records from this database, meaning reporting workloads compete with live website transactions for shared resources. This resource contention is the likely cause of the slowdowns, although the exact technical bottleneck has not been confirmed.

**Ranked Findings:**

1. Monday exports have slowed the live website twice in the last month, demonstrating an existing operational problem.
2. Reporting workloads and customer transactions depend on the same server and database resources.
3. Continued business growth could increase resource demands and make further slowdowns more likely.

**Assumptions:**

- Shared-resource contention is the likely cause, but the exact bottleneck has not been confirmed.
- The number of customers affected and the duration of the slowdowns are unknown.
- The number and value of potentially lost orders have not been established.
- The average order value and website conversion rate are unknown.

**Cost Assessment:**

- **Wasted Labour:** Developer time may be spent investigating and resolving performance incidents. This can be calculated as incident-related hours multiplied by the developer's loaded hourly rate.
- **Direct Loss:** Slow website responses may cause customers to abandon purchases. Potential lost sales can be estimated using:

  `Lost sales = Number of incidents x Estimated lost orders per incident x Average order value`

  The number of lost orders and average order value must be established before assigning a cedi amount.
- **Risk-Weighted Exposure:** Recurring slowdowns could result in lost sales, customer dissatisfaction and reputational damage. The financial impact remains uncertain because incident duration and affected customer numbers are unknown.

**Risk Ranking Justification:**

This problem ranks second because the slowdowns have already affected the live website twice in one month. Unlike inconsistent reporting, this problem directly affects a production system customers depend on to place orders. However, the Data Protection Commission complaint ranks higher because of its immediate response deadline and potential compliance consequences.


### 2.3 Inconsistent Business Reporting

**Root Cause:**

Nana and Finance produce separate reports from exported MySQL data, but their figures do not match. The underlying problem is the absence of agreed and owned definitions for key business measures, such as revenue. Without one authoritative calculation, departments can apply different reporting rules and produce conflicting figures from the same data. Manual spreadsheet calculations also make results harder to reproduce and verify.

**Ranked Findings:**

1. Nana's figures do not match Finance's figures, demonstrating an existing consistency problem.
2. Both teams rebuild reports independently instead of using one agreed reporting process.
3. The absence of shared definitions and ownership allows different reporting methods to produce conflicting results.
4. Manual spreadsheet calculations make reports harder to reproduce, check and maintain.

**Assumptions:**

- The exact reasons for the differences have not been established.
- Differences may arise from calculation methods, reporting periods, data selection, extraction times or spreadsheet formulas.
- The time spent rebuilding and reconciling reports is unknown.
- It has not been established whether conflicting figures have affected business decisions.

**Cost Assessment:**

- **Wasted Labour:** Nana and Finance spend time rebuilding and checking reports instead of focusing on their other responsibilities. This wastes valuable staff time every week.
- **Direct Loss:** No direct financial loss has been established. However, decisions based on incorrect figures could result in poor business choices such as management making wrong budget decisions.
- **Risk-Weighted Exposure:** Conflicting figures could weaken management's confidence in reporting and investors' confidence in Kloud Kart's ability to explain its performance. The financial impact has not been established.

**Risk Ranking Justification:**

This problem ranks third because it creates wasted labour and uncertainty, but the case does not establish a direct financial loss or an incorrect business decision. It remains important because management and investors need consistent figures to assess performance and guide business growth.


**Conclusion:** Kloud Kart's immediate challenge is not a lack of advanced data technology. It is the lack of sufficient control over customer information, separation between reporting and live operations and consistency in business reporting. These foundational problems must be addressed before the company invests heavily in more advanced data capabilities.