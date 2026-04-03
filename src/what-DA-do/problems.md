# Types of Data and Analytical Problems

Data analytics begins with understanding two things clearly:

1. **What kind of data you have**
2. **What kind of question you are trying to answer**

A strong analyst does not jump straight into charts or models. They first identify the structure of the data, the meaning of each field, the time dimension, and the decision the analysis is meant to support. The same dataset can be used for very different analytical purposes depending on the business problem.

---

## Why data types matter

Data type is not just a technical detail. It determines:

* how data is stored and cleaned
* what summaries are meaningful
* which visualizations make sense
* what statistical methods are valid
* what limitations or biases may exist

For example, averaging customer IDs is meaningless, but averaging revenue is useful. Sorting job titles alphabetically may help organization, but sorting customer satisfaction levels as an ordered scale has analytical meaning. Good analysis depends on these distinctions.

---

## Structured, Semi-Structured, and Unstructured Data

One of the first ways to classify data is by **how organized it is**.

### Structured data

**Structured data** follows a predefined schema. It is organized into rows and columns, usually in spreadsheets, databases, or data warehouses.

Examples:

* sales transactions
* customer records
* inventory tables
* payroll data
* website session logs stored in tabular form

Typical characteristics:

* each field has a defined type
* easy to query with SQL
* relatively easy to aggregate and join
* common in dashboards and reporting systems

Example:

| customer_id | order_date | product_category | order_amount |
| ----------- | ---------: | ---------------- | -----------: |
| C101        | 2026-01-14 | Electronics      |       249.99 |
| C102        | 2026-01-14 | Books            |        18.50 |

Structured data is the foundation of most business analytics because it is easy to filter, summarize, and visualize.

### Semi-structured data

**Semi-structured data** does not fit neatly into a rigid table, but it still contains patterns, tags, or keys that provide organization.

Examples:

* JSON API responses
* XML documents
* application event logs
* emails with metadata
* clickstream data

Typical characteristics:

* flexible schema
* fields may vary across records
* nested objects and arrays are common
* often requires parsing or transformation before analysis

Example JSON:

```json
{
  "user_id": "U1004",
  "event_name": "purchase",
  "timestamp": "2026-04-03T09:15:00Z",
  "properties": {
    "product_id": "P200",
    "price": 49.99,
    "coupon_used": true
  }
}
```

Semi-structured data is common in modern software systems and digital products. Analysts often work with it after it has been flattened into structured tables.

### Unstructured data

**Unstructured data** has no fixed schema and is usually harder to analyze directly.

Examples:

* free-text customer reviews
* call center transcripts
* PDFs
* images
* videos
* audio recordings
* social media posts

Typical characteristics:

* rich in context and meaning
* difficult to summarize with standard tabular methods
* often requires natural language processing, computer vision, or manual coding
* can provide qualitative insight not available in transactional data

A customer support ticket may contain emotional tone, complaint details, and product issues that never appear in a simple support category field. This makes unstructured data extremely valuable, even though it is more difficult to process.

### Practical comparison

| Type            | Organization                   | Ease of analysis | Common tools                | Example                 |
| --------------- | ------------------------------ | ---------------- | --------------------------- | ----------------------- |
| Structured      | Fixed schema                   | High             | SQL, spreadsheets, BI tools | Sales table             |
| Semi-structured | Flexible schema with tags/keys | Medium           | JSON parsers, SQL, Python   | App event logs          |
| Unstructured    | No fixed schema                | Lower            | NLP, OCR, ML, manual review | Reviews, images, emails |

---

## Numerical, Categorical, Ordinal, Temporal, and Text Data

Another critical classification focuses on the **meaning of individual variables**.

---

### Numerical data

**Numerical data** represents quantities or counts and supports arithmetic operations.

Two broad forms are common:

#### Continuous numerical data

Can take many possible values within a range.

Examples:

* revenue
* temperature
* delivery time
* product weight
* account balance

#### Discrete numerical data

Represents counts, usually whole numbers.

Examples:

* number of purchases
* website visits
* support tickets
* employees per team

Common analyses:

* averages
* sums
* variance and standard deviation
* correlation
* trend analysis
* forecasting

Important caution: not every number is analytically numerical. A ZIP code or employee ID contains digits but is better treated as a category or identifier.

---

### Categorical data

**Categorical data** groups observations into labels or classes.

Examples:

* country
* product category
* payment method
* customer segment
* subscription status

Common analyses:

* frequency counts
* proportions
* cross-tabulations
* bar charts
* conversion rates by category

Categorical variables help answer questions like:

* Which region sells the most?
* Which marketing channel converts best?
* Which product category has the highest return rate?

---

### Ordinal data

**Ordinal data** is categorical data with a meaningful order, but the distance between categories is not necessarily equal.

Examples:

* customer satisfaction: very dissatisfied, dissatisfied, neutral, satisfied, very satisfied
* education level
* ticket priority: low, medium, high, urgent
* risk rating: 1 to 5

Common analyses:

* rank comparisons
* distribution by level
* median or percentile summaries
* trend in movement between levels

Important caution: the difference between “low” and “medium” is not guaranteed to equal the difference between “medium” and “high.” Treating ordinal variables like continuous numbers can be misleading.

---

### Temporal data

**Temporal data** describes time-related information.

Examples:

* timestamps
* dates
* weeks
* months
* quarters
* event durations

Temporal data is central in analytics because businesses change over time. Nearly every important question eventually becomes temporal:

* Are sales rising or falling?
* Did the campaign improve conversions after launch?
* Are churn rates worse this quarter than last quarter?

Common analyses:

* trend analysis
* seasonality analysis
* cohort analysis
* lag comparisons
* retention analysis
* forecasting

Temporal data often requires careful handling of:

* time zones
* missing periods
* calendar effects
* seasonality
* weekends and holidays
* irregular intervals

---

### Text data

**Text data** includes words, sentences, and language-based content.

Examples:

* survey responses
* support tickets
* chat transcripts
* product reviews
* social posts
* internal notes

Text can be analyzed in simple or advanced ways.

Simple approaches:

* keyword counts
* tagging themes
* manual coding
* sentiment categories

Advanced approaches:

* topic modeling
* sentiment analysis
* clustering
* embeddings and semantic search
* classification models

Text data is valuable because it captures nuance. Numeric metrics may show **what** happened, while text often helps explain **why**.

---

## Cross-Sectional, Time-Series, and Panel Data

A dataset’s time structure strongly affects what questions can be answered.

### Cross-sectional data

**Cross-sectional data** captures many entities at a single point in time, or over a very short period treated as one snapshot.

Examples:

* customer demographics as of today
* employee salaries in March 2026
* store performance during one month

Typical questions:

* How do different groups compare?
* Which regions outperform others?
* What factors are associated with high-value customers?

Common methods:

* comparison across groups
* segmentation
* classification
* regression
* summary statistics

Example:

| customer_id | age | region | annual_spend |
| ----------- | --: | ------ | -----------: |
| C001        |  29 | West   |         1200 |
| C002        |  45 | East   |         3400 |

This supports comparison across customers, but not analysis of how each customer changed over time.

---

### Time-series data

**Time-series data** tracks one entity or aggregate measure across time.

Examples:

* daily website traffic
* monthly revenue
* weekly inventory levels
* hourly sensor readings

Typical questions:

* Is there a trend?
* Is there seasonality?
* Can future values be forecast?
* Did something unusual happen this week?

Common methods:

* moving averages
* decomposition
* time-series forecasting
* anomaly detection
* intervention analysis

Example:

| date       | daily_sales |
| ---------- | ----------: |
| 2026-04-01 |       15230 |
| 2026-04-02 |       14980 |
| 2026-04-03 |       16710 |

This structure is ideal for trend monitoring and forecasting.

---

### Panel data

**Panel data** combines cross-sectional and time-series dimensions. It tracks multiple entities over multiple time periods.

Examples:

* monthly spend by customer
* quarterly sales by region
* daily output by machine
* annual performance by employee

Typical questions:

* How do entities differ from one another?
* How does each entity change over time?
* Are observed changes driven by time effects, entity effects, or both?

Common methods:

* cohort tracking
* retention analysis
* longitudinal analysis
* fixed effects or mixed models
* panel regression

Example:

| customer_id | month   | orders | spend |
| ----------- | ------- | -----: | ----: |
| C001        | 2026-01 |      2 |    80 |
| C001        | 2026-02 |      1 |    25 |
| C002        | 2026-01 |      4 |   210 |

Panel data is especially useful in business because many important problems involve repeated behavior by the same users, stores, products, or accounts.

---

## Common Business Questions

Most analytical work exists to answer recurring business questions. These usually fall into a handful of broad categories.

### Performance questions

* How are we doing?
* Are we meeting targets?
* Which areas are underperforming?

### Diagnostic questions

* Why did revenue fall last month?
* Why are customers churning?
* Why is this region underperforming?

### Predictive questions

* What will demand look like next quarter?
* Which customers are likely to cancel?
* How many support tickets should we expect next week?

### Prescriptive questions

* What action should we take?
* Which customers should receive retention offers?
* How should budget be allocated across channels?

The same business area may require all four. For example, a marketing team may first monitor campaign performance, then diagnose underperformance, then forecast future leads, then decide how to reallocate spend.

---

# Core Analytical Problem Types

## KPI Tracking

**KPI tracking** focuses on monitoring key performance indicators over time to measure whether the business is progressing toward its goals.

Examples of KPIs:

* revenue
* profit margin
* churn rate
* customer acquisition cost
* average order value
* on-time delivery rate
* conversion rate

Typical questions:

* Are we above or below target?
* How does this week compare with last week, last month, or last year?
* Which business unit is driving the change?
* Is performance improving consistently or just fluctuating?

Typical data used:

* structured transactional data
* time-series aggregates
* dimensional attributes such as region, product, or channel

Common outputs:

* dashboards
* scorecards
* alerts
* variance analysis

Key analyst tasks:

* define KPIs precisely
* ensure consistent metric logic
* choose appropriate comparison periods
* segment by useful dimensions
* distinguish signal from noise

A KPI is only useful if it is clearly defined. For example, “active user” must be specified precisely or teams may interpret it differently.

---

## Root Cause Analysis

**Root cause analysis** investigates why an observed outcome changed or why a problem occurred.

Examples:

* sales dropped in one region
* delivery times increased
* defect rates rose after a process change
* user retention declined after product redesign

Typical questions:

* What changed?
* Where did the issue start?
* Which factors are most associated with the outcome?
* Is the problem broad or isolated?

Typical methods:

* drill-down analysis
* segmentation
* funnel analysis
* before/after comparison
* cohort comparison
* correlation and regression
* process mapping
* issue tree decomposition

A useful workflow is:

1. confirm that the problem is real
2. measure its size
3. localize where it occurs
4. compare affected vs unaffected groups
5. identify likely drivers
6. validate whether those drivers are causal or merely associated

Root cause analysis is often harder than KPI tracking because it requires judgment. Many variables move together, and not every association is a true cause.

---

## Forecasting

**Forecasting** estimates future values based on historical patterns and relevant drivers.

Examples:

* next month’s demand
* quarterly revenue
* staffing requirements
* website traffic
* inventory needs
* cash flow

Typical questions:

* What is likely to happen next?
* What range of outcomes should we expect?
* How uncertain is the forecast?
* What assumptions drive the prediction?

Typical data used:

* time-series data
* seasonal patterns
* external drivers such as holidays, promotions, weather, or prices
* panel data when forecasting many entities

Common methods:

* moving averages
* exponential smoothing
* ARIMA-type models
* regression
* machine learning models
* scenario analysis

Important forecasting concepts:

* **trend**: long-term direction
* **seasonality**: repeating calendar patterns
* **cyclicality**: broader business cycles
* **noise**: random variation
* **forecast horizon**: how far ahead the prediction goes

Good forecasting is not just about producing a number. It also means communicating uncertainty and explaining what assumptions would cause the result to change.

---

## Segmentation

**Segmentation** groups entities into meaningful subsets so the business can understand differences and tailor decisions.

Entities may include:

* customers
* products
* stores
* employees
* suppliers
* transactions

Examples:

* high-value vs low-value customers
* frequent vs occasional buyers
* profitable vs unprofitable products
* high-risk vs low-risk accounts

Typical questions:

* Are all customers behaving the same way?
* Which groups have the highest value or risk?
* Should we treat certain groups differently?
* What patterns emerge when similar observations are grouped?

Segmentation methods range from simple to advanced:

### Rule-based segmentation

Uses business-defined logic.

Example:

* new customers
* active customers
* churned customers

### Statistical or machine learning segmentation

Uses patterns in the data.

Example methods:

* clustering
* latent class analysis
* behavioral scoring

Segmentation is useful because averages hide variation. Two customer groups may have the same average spend but very different retention patterns, support needs, or profit margins.

---

## Experimentation

**Experimentation** tests whether a change causes an improvement.

Examples:

* testing a new landing page
* comparing pricing strategies
* evaluating a recommendation algorithm
* measuring the effect of a retention email

Typical questions:

* Did the intervention work?
* How large was the effect?
* Was the effect statistically credible?
* Did different user groups respond differently?

Common experimental designs:

* A/B tests
* multivariate tests
* randomized controlled trials
* holdout groups
* quasi-experiments when randomization is not possible

Core concepts:

* treatment group
* control group
* randomization
* sample size
* statistical significance
* confidence interval
* practical significance

A good analyst distinguishes between:

* **correlation**: two things changed together
* **causation**: one thing caused the other to change

Experimentation is one of the strongest ways to support decision-making because it can establish causal evidence more reliably than observational analysis.

---

## Risk and Anomaly Detection

**Risk and anomaly detection** identifies events, observations, or patterns that are unusual, suspicious, or likely to lead to negative outcomes.

Examples:

* fraudulent transactions
* credit default risk
* cybersecurity anomalies
* equipment failure warning signs
* sudden drop in conversion rate
* abnormal spikes in returns or cancellations

Typical questions:

* What looks unusual?
* Which cases need attention first?
* Who or what is at greatest risk?
* Has the process shifted from normal behavior?

Types of detection problems:

### Rule-based detection

Uses thresholds or business rules.

Examples:

* flag refunds above a certain amount
* alert when conversion rate drops below threshold
* identify accounts with repeated failed logins

### Statistical anomaly detection

Looks for points outside expected ranges.

Examples:

* z-scores
* control charts
* deviation from seasonal baseline

### Predictive risk scoring

Estimates probability of a bad outcome.

Examples:

* default likelihood
* churn propensity
* fraud risk score
* failure probability

Important challenges:

* false positives
* false negatives
* changing baselines
* class imbalance
* explainability

In many real business settings, anomaly detection must work in near real time and balance accuracy with operational cost. A model that flags too many normal events becomes unusable.

---

# Linking Data Types to Analytical Problems

Different problem types often rely on different data structures.

| Analytical problem     | Common data types                               | Common structure                                       |
| ---------------------- | ----------------------------------------------- | ------------------------------------------------------ |
| KPI tracking           | Numerical, categorical, temporal                | Structured time-series or panel                        |
| Root cause analysis    | Numerical, categorical, ordinal, temporal, text | Structured and semi-structured; sometimes unstructured |
| Forecasting            | Numerical, temporal                             | Time-series or panel                                   |
| Segmentation           | Numerical, categorical, ordinal, text           | Cross-sectional or panel                               |
| Experimentation        | Numerical, categorical, temporal                | Structured experimental data                           |
| Risk/anomaly detection | Numerical, categorical, temporal, text          | Structured, semi-structured, and event data            |

This mapping is not rigid, but it shows a core analytical truth: the question determines the method, and the data determines what is feasible.

---

# Practical Examples

## Example 1: Retail company

Available data:

* transaction records
* product catalog
* store attributes
* promotion calendar
* customer reviews

Possible analyses:

* **KPI tracking**: weekly sales, margin, return rate
* **Root cause analysis**: why returns rose in one product category
* **Forecasting**: holiday demand by store
* **Segmentation**: high-frequency vs low-frequency shoppers
* **Experimentation**: effect of a coupon campaign
* **Anomaly detection**: suspicious refund activity

## Example 2: SaaS company

Available data:

* user event logs
* subscription records
* support tickets
* customer survey responses

Possible analyses:

* **KPI tracking**: monthly recurring revenue, activation rate, churn
* **Root cause analysis**: why onboarding completion dropped
* **Forecasting**: future renewals or ticket volume
* **Segmentation**: power users vs at-risk users
* **Experimentation**: impact of UI redesign
* **Risk detection**: accounts likely to churn

---

# Common Mistakes Beginners Make

## Confusing identifiers with numeric variables

Just because a field contains numbers does not mean it should be averaged or modeled as continuous.

Examples:

* customer ID
* ZIP code
* phone number

## Ignoring time structure

Averages across time can hide trends, seasonality, or structural breaks.

## Treating ordinal data as interval data without caution

A 1-to-5 satisfaction scale is ordered, but the distance between each step may not be equal.

## Using unstructured data as an afterthought

Text, comments, and transcripts often contain the explanation missing from KPI dashboards.

## Starting with methods instead of business questions

Analysts sometimes jump into clustering, regression, or dashboards before defining the decision problem. This usually produces output, not insight.

---

# What good analysts do

A capable analyst can usually answer these early questions before doing deeper work:

* What is the unit of analysis?
* What does each row represent?
* Which variables are numerical, categorical, ordinal, temporal, or text?
* Is the dataset cross-sectional, time-series, or panel?
* What decision is this analysis supposed to inform?
* Is the problem descriptive, diagnostic, predictive, prescriptive, or causal?
* What limitations in the data could distort the answer?

This framing step is often more important than the technique itself.

---

# Summary

Understanding data types and analytical problem types is foundational to data analytics.

* **Structured, semi-structured, and unstructured data** describe how information is organized.
* **Numerical, categorical, ordinal, temporal, and text data** describe the meaning of variables.
* **Cross-sectional, time-series, and panel data** describe how observations relate to time and entities.
* Business analytics commonly focuses on **KPI tracking, root cause analysis, forecasting, segmentation, experimentation, and risk or anomaly detection**.

The best analytical work comes from matching the right problem to the right data and the right method. Before building a dashboard, model, or report, a strong analyst asks: **what kind of data is this, and what question are we actually trying to answer?**

---

## Key Takeaways

* Data structure affects how easily data can be stored, cleaned, and queried.
* Variable type affects what summaries and models are valid.
* Time structure affects whether you can compare, explain, or forecast.
* Most business analyses fit into a small number of recurring problem categories.
* Good analytics starts with problem framing, not tool selection.
