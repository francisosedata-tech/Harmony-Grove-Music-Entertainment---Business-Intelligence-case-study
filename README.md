# Harmony Grove Music & Entertainment – Business Intelligence Case Study

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

https://github.com/francisosedata-tech/Harmony-Grove-Music-Entertainment---Business-Intelligence-case-study/blob/56262fb59e4d8fc6ed8b0d8c673879a62e72a45f/Data/Harmony%20Grove%20logo.jpeg
---

## 📌 The Business Problem

Harmony Grove is a multi-service music education and events business operating across six Nigerian cities. Revenue comes from three streams:
- **Bookings** – Individual and school lesson bookings
- **Corporate Contracts** – Pre-paid session packages
- **Subscriptions** – Prodigies Prime & Pro

Before this project, performance data was scattered across spreadsheets and systems. Leadership could not answer basic operational questions:

- *Which tutors are at risk of leaving?*
- *Are corporate clients getting value from their contracts?*
- *Which client acquisition channels are actually worth investing in?*
- *Why is subscription renewal below target?*
- *Does having more tutors in a city actually drive more revenue?*

This project builds a structured data model and interactive Power BI dashboard to answer these questions directly from the data — and surface insights the business could act on immediately.

---

## 🔍 The Investigation

### Question 1: Does client rating predict tutor churn?

**Finding:** Churn rises from 10% (top-rated tutors) to a peak of **50%** in the 3.0-3.49 rating band — a five-fold increase — before easing slightly to 36.4% below 3.0.

**Why this matters:** The 3.0-3.49 range is a clear early-warning zone. This is a concrete, data-backed trigger for intervention, not a vague "watch low performers" policy.

---

### Question 2: Why are tutors actually leaving?

**Finding:** "Low bookings/pay" is the single largest driver of tutor exits — ahead of better opportunities, policy violations, low ratings, relocation, and attendance issues.

**Why this matters:** Attrition is driven by income/utilization, not skill or conduct. This reframes the retention conversation from *"who is underperforming"* to *"how are bookings being distributed."*

---

### Question 3: Which segment drives the most revenue?

**Finding:** Bookings account for **61.39%** of revenue, corporate contracts **32.3%**, and subscriptions just **6.31%**.

**Why this matters:** Subscriptions are heavily under-monetized relative to the other two streams — a dedicated growth push is warranted.

---

### Question 4: Are pre-paid corporate sessions being used?

**Finding:** Corporate contracts are utilized at only **47.80%** on average, and utilization is broadly similar across Active, Renewed, Completed, and even Cancelled contracts (46-51% range).

**Why this matters:** Under-utilization is a business-wide pattern, not isolated to at-risk accounts. Clients may not be fully aware of or able to easily redeem their paid sessions.

---

### Question 5: How does referral source affect engagement?

**Finding:** Word of Mouth brings 69 clients who generate **1,880 completed transactions** — far outpacing Facebook and Google Search, which bring more or equal clients (72 each) but only 1,064 transactions.

**Why this matters:** Word-of-mouth clients are dramatically more engaged than paid-channel clients — and cost nothing to acquire.

---

### Question 6: Does tutor headcount by city predict revenue?

**Finding:** No. Enugu (20 tutors) and Lagos (17 tutors) generate the lowest revenue and transactions per tutor (₦678K and 45.4 transactions; ₦805K and 52.3 transactions respectively). Uyo (13 tutors) and Benin City (14 tutors) generate the highest (₦1.11M and 106.6 transactions; ₦1.14M and 88.7 transactions respectively) despite far fewer tutors and clients.

**Why this matters:** Revenue is driven by tutor productivity and client engagement per city, not by headcount. Enugu and Lagos may be over-staffed relative to demand; Uyo and Benin City show a leaner, higher-performing model worth studying and replicating.

---

## 📊 Dashboard Pages

### Page 1 – Revenue Overview
- Revenue Generated: ₦80.37M | Gross Revenue: ₦96.68M
- Revenue by Segment, City, Instrument, and Referral Source
- Revenue Trend Over Time

### Page 2 – Tutors' Behavior
- Total Tutors: 88 | Active: 64 | Retention Rate: 72.7%
- Top 20 Tutors by Revenue
- Inactive Tutor Exit Reasons
- Tutor Distribution by City and Instrument

### Page 3 – Clients' Behavior
- Total Subscriptions: 138 | Active: 59 | Renewal Rate: 43%
- Corporate Contracts: 49 | Active: 21 | Utilization: 47.8%
- Top Clients by Revenue
- Referral Source Analysis

---

## 💡 Recommendations

Based on the findings, I recommended the following:

1. **Introduce a proactive tutor check-in** triggered when a tutor's average rating enters the 3.0-3.49 range — the data shows this is the point where churn risk becomes most acute.

2. **Review how bookings are distributed among tutors.** Since "low bookings/pay" is the top driver of attrition, an uneven distribution of client bookings may be quietly driving churn independent of tutor quality.

3. **Investigate why corporate clients consistently under-use their paid sessions.** Since utilization is flat across contract outcomes, a simple fix — clearer session reminders, easier booking access, or account check-ins — could lift usage business-wide.

4. **Formalize a referral incentive programme.** Word of Mouth already outperforms every paid channel on engagement at zero acquisition cost; a modest, structured incentive could scale this organically.

5. **Reassess the subscription product's positioning and value proposition.** With renewal well below its 70% target and a small share of overall revenue, subscriptions need either a pricing/value review or a more deliberate growth strategy.

6. **Study what Uyo and Benin City are doing differently and assess whether it can be replicated.** With substantially fewer tutors and clients, both cities out-produce Enugu and Lagos on every per-tutor and per-client metric — this may reflect stronger client relationships, better booking allocation, or simply a leaner, better-matched tutor base relative to local demand.

7. **Reassess tutor staffing levels in Enugu and Lagos against actual demand.** The lowest revenue and transactions per tutor in the business, despite the largest tutor headcounts, suggests these markets may be over-staffed relative to booking volume — worth investigating before adding further tutors in these cities.

---

## 🛠️ Technical Implementation

### Data Model (SQL Schema)

```sql
-- Tutors Table
CREATE TABLE tutors (
    id VARCHAR(10) PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(50),
    instrument VARCHAR(50),
    rating DECIMAL(3,2),
    rating_band VARCHAR(10),
    status VARCHAR(20),
    exit_reason VARCHAR(100),
    join_date DATE
);

-- Clients Table
CREATE TABLE clients (
    id VARCHAR(10) PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(50),
    status VARCHAR(20),
    referral_source VARCHAR(50),
    segment VARCHAR(20)
);

-- Transactions Table
CREATE TABLE transactions (
    id VARCHAR(10) PRIMARY KEY,
    client_id VARCHAR(10),
    tutor_id VARCHAR(10),
    amount DECIMAL(10,2),
    refund_amount DECIMAL(10,2),
    status VARCHAR(20),
    segment VARCHAR(20),
    instrument VARCHAR(50),
    city VARCHAR(50),
    transaction_date DATE,
    FOREIGN KEY (client_id) REFERENCES clients(id),
    FOREIGN KEY (tutor_id) REFERENCES tutors(id)
);

-- Subscriptions Table
CREATE TABLE subscriptions (
    id VARCHAR(10) PRIMARY KEY,
    client_id VARCHAR(10),
    plan_name VARCHAR(50),
    status VARCHAR(20),
    renewed_flag BOOLEAN,
    start_date DATE,
    end_date DATE,
    FOREIGN KEY (client_id) REFERENCES clients(id)
);

-- Corporate Contracts Table
CREATE TABLE contracts (
    id VARCHAR(10) PRIMARY KEY,
    client_id VARCHAR(10),
    sessions_purchased INT,
    sessions_used INT,
    status VARCHAR(20),
    start_date DATE,
    end_date DATE,
    FOREIGN KEY (client_id) REFERENCES clients(id)
);
