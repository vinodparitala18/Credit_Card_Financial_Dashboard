# 💳 Credit Card Weekly Dashboard — Power BI & PostgreSQL

An end-to-end business intelligence solution that monitors credit card operations in real time, delivering weekly insights into revenue, transactions, customer behavior, and risk metrics through interactive Power BI dashboards.

---

## 📌 Project Overview

This project connects a **PostgreSQL database** to **Power BI** to build a live, auto-refreshing dashboard across two report pages — one focused on transaction-level KPIs and one on customer demographics. The goal is to give stakeholders a single pane of glass for credit card performance monitoring, reducing manual reporting and enabling faster, data-driven decisions.

---

## 📊 Dashboard Pages

### Page 1 — CC Transaction Report
Tracks weekly credit card transaction performance including:
- **Revenue by Card Category** (Blue, Silver, Gold, Platinum)
- **Week-over-Week (WoW) Revenue** — current week vs. previous week with % change
- **Total Transaction Amount & Count** trends over time
- **Revenue by Expenditure Type** (Bills, Entertainment, Grocery, Fuel, Travel, Food)
- **Revenue by Chip Usage** (Swipe, Chip, Online)
- **Quarterly performance breakdown**

### Page 2 — CC Customer Report
Profiles the customer base behind the transactions:
- **Revenue by Age Group & Income Group**
- **Customer Satisfaction Score** (avg. CSAT)
- **Revenue by Education Level, Marital Status, and Job Type**
- **Dependent Count & Income distribution**
- **Activation rate (30-day)** and **Delinquency rate** by segment
- **State-wise** customer distribution
- **Gender-based** revenue split

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard design & visualization |
| PostgreSQL | Backend database for raw credit card data |
| DAX | Custom measures (WoW Revenue, Current/Previous Week Revenue) |
| Power Query (M) | Data transformation and modeling |

---

## 🗂️ Data Model

**Primary Table:** `public.cc_detail`

Key fields used across the dashboard:

| Field | Description |
|-------|-------------|
| `client_num` | Unique customer identifier |
| `card_category` | Card tier (Blue / Silver / Gold / Platinum) |
| `Revenue` | Total revenue generated |
| `total_trans_amt` | Total transaction amount |
| `total_trans_ct` | Total transaction count |
| `interest_earned` | Interest revenue |
| `week_num2` | Week number for time-series analysis |
| `week_start_date` | Week start date (Day / Month / Year) |
| `current_week_revenue` | DAX measure — current week revenue |
| `previuos_week_revenue` | DAX measure — previous week revenue |
| `wow_revenue` | DAX measure — week-over-week % change |
| `exp_type` | Expenditure type category |
| `use_chip` | Transaction method (Swipe / Chip / Online) |
| `activation_30_days` | 30-day activation flag |
| `delinquent_acc` | Delinquency flag |
| `gender` | Customer gender |
| `Age_group` | Age bracket |
| `Income_group` | Income bracket |
| `education_level` | Highest education attained |
| `marital_status` | Marital status |
| `customer_job` | Occupation |
| `state_cd` | State code |
| `cust_satisfaction_score` | CSAT score |
| `dependent_count` | Number of dependents |

---

## 📐 Key DAX Measures

```dax
-- Current Week Revenue
current_week_revenue = 
    CALCULATE(SUM(cc_detail[Revenue]),
    FILTER(ALL(cc_detail), cc_detail[week_num2] = MAX(cc_detail[week_num2])))

-- Previous Week Revenue
previuos_week_revenue = 
    CALCULATE(SUM(cc_detail[Revenue]),
    FILTER(ALL(cc_detail), cc_detail[week_num2] = MAX(cc_detail[week_num2]) - 1))

-- Week-over-Week Revenue Change
wow_revenue = 
    DIVIDE([current_week_revenue] - [previuos_week_revenue], [previuos_week_revenue])
```

---

## 📈 Visuals Used

| Visual | Purpose |
|--------|---------|
| Clustered Column Chart | Revenue by card category, age group |
| Line Chart | Weekly revenue trend over time |
| Bar Chart | Revenue by job type, state, education |
| Combo Chart (Line + Column) | Transaction count vs. revenue |
| Treemap | Revenue breakdown by expenditure type |
| Pivot / Matrix Table | WoW revenue comparison by week |
| KPI Cards | Total revenue, transaction count, CSAT, interest earned |
| Slicers | Filter by quarter, gender, card category, week |

---

## 🚀 How to Use

1. **Clone this repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/credit-card-weekly-dashboard.git
   cd credit-card-weekly-dashboard
   ```

2. **Set up PostgreSQL**
   - Create the database and load the `cc_detail` table using the provided SQL scripts
   - Update the connection string in Power BI: `Home → Transform Data → Data Source Settings`

3. **Open in Power BI Desktop**
   - Open `credit_card_report.pbix`
   - Refresh data to load latest records from PostgreSQL

4. **Publish (optional)**
   - Publish to Power BI Service for live sharing and scheduled refresh

---

## 💡 Key Business Insights

- **WoW revenue tracking** enables immediate detection of revenue drops or spikes
- **Delinquency rate segmentation** helps risk teams prioritize outreach by card type and demographics
- **30-day activation rate** highlights onboarding effectiveness across customer segments
- **Expenditure type analysis** reveals high-value spending categories for targeted offers
- Automated refresh **reduced manual reporting effort by 30%**

---

