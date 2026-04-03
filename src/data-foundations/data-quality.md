# Data Quality

Data quality is the degree to which data is fit for its intended use. A dataset is not “high quality” in the abstract; it is high quality relative to a task, decision, or workflow. Data that is acceptable for a rough internal dashboard may be inadequate for regulatory reporting, financial forecasting, experimentation, or machine learning.

For analysts, data quality is not a side concern. It directly determines whether metrics are trustworthy, whether comparisons are meaningful, and whether decisions based on analysis are defensible. Poor data quality can produce misleading trends, broken dashboards, incorrect forecasts, wasted operational effort, and loss of stakeholder confidence.

A core principle is this: **every analysis contains implicit assumptions about the quality of the underlying data**. Good analysts make those assumptions explicit, test them, and document where the data is weak.

---

## Why Data Quality Matters

Data quality affects every stage of analysis:

* **Measurement:** If values are wrong or incomplete, KPIs are distorted.
* **Aggregation:** Duplicates and inconsistent definitions can inflate totals or misstate rates.
* **Comparison:** If data is not recorded consistently across teams, systems, or time periods, comparisons become unreliable.
* **Modeling:** Predictive models are sensitive to missing values, invalid categories, drift, and mislabeled records.
* **Decision-making:** Poor-quality data leads to false confidence, delayed action, and costly mistakes.

A useful mindset is to treat data quality as both a **technical** issue and a **business** issue. Technical checks identify broken formats, null values, and duplicates. Business checks determine whether the data actually reflects reality as the organization understands it.

---

## Core Dimensions of Data Quality

Several dimensions are commonly used to evaluate data quality. These dimensions overlap, but each highlights a distinct type of problem.

### Accuracy

**Accuracy** is the extent to which data correctly represents the real-world value or event it is supposed to capture.

Examples:

* A customer’s birth date is entered incorrectly.
* Revenue is recorded in the wrong currency.
* A sensor reports temperatures shifted by a calibration error.

Accuracy is often difficult to verify from the dataset alone because the “true” value may be external to the system. Analysts may need to compare against a trusted source, perform reconciliation, or use sampling and manual review.

Questions to ask:

* Does the recorded value reflect reality?
* Is the source system known to capture this field reliably?
* Can the field be cross-checked against another authoritative source?

### Completeness

**Completeness** measures whether required data is present.

Examples:

* Orders exist without customer IDs.
* Survey responses are missing demographic fields.
* Transaction records lack timestamps.

Completeness can be measured at multiple levels:

* **Field completeness:** Is a specific column populated?
* **Record completeness:** Does a row contain all required fields?
* **Coverage completeness:** Are all expected entities or events represented at all?

A dataset can look large and still be incomplete if important segments, dates, or systems are missing.

### Consistency

**Consistency** refers to whether data is represented uniformly across records, datasets, systems, or time.

Examples:

* The same country appears as `USA`, `US`, and `United States`.
* Product categories differ between the operational database and the dashboard extract.
* A “completed order” status means different things in two systems.

Consistency issues often arise when multiple teams define fields independently, when systems evolve over time, or when transformation logic is not standardized.

### Validity

**Validity** asks whether data conforms to allowed formats, rules, domains, and business constraints.

Examples:

* Email addresses without `@`
* Negative ages
* Dates in impossible formats
* Order status values outside the approved list

Validity does not guarantee accuracy. A value can be valid in format but still wrong in meaning. For example, a valid-looking postal code may belong to the wrong customer.

### Uniqueness

**Uniqueness** means that records that should appear only once do, in fact, appear only once.

Examples:

* Duplicate customer profiles
* The same invoice loaded twice
* Multiple rows for one supposedly unique transaction ID

Uniqueness problems can inflate counts, distort conversion rates, and break joins. The presence or absence of duplicates depends on the expected grain of the dataset, so uniqueness must be evaluated relative to keys and business logic.

### Timeliness

**Timeliness** measures whether data is sufficiently current and available when needed.

Examples:

* Sales data arrives two days late for a daily operations dashboard.
* Inventory data refreshes weekly when planners need hourly updates.
* Customer profile data reflects last month’s status rather than current conditions.

Timeliness requirements depend on the use case. Real-time fraud monitoring and quarterly board reporting have very different tolerances for latency.

---

## Missing Data

Missing data is one of the most common data quality issues. It occurs when expected values are absent, blank, null, placeholder-filled, or otherwise unavailable.

### Types of Missingness in Practice

In operational and analytical settings, missing data can arise for many reasons:

* A field was optional and users skipped it.
* A system did not capture the field at the time.
* Data failed during ingestion or transformation.
* A value is not applicable for certain records.
* Privacy rules or redaction removed the value.

Analysts should distinguish between different meanings of “missing”:

* **Unknown:** value should exist but is unavailable
* **Not collected:** system never captured it
* **Not applicable:** the field does not apply to this record
* **Withheld:** intentionally omitted for privacy or policy reasons

Treating all nulls as equivalent can produce misleading results.

### Risks of Missing Data

Missing data can:

* Bias averages, rates, and segment comparisons
* Reduce sample size
* Break business rules and joins
* Distort model training and scoring
* Hide operational problems in data collection

For example, if customer satisfaction scores are missing mostly from dissatisfied users, a simple average of observed responses may overestimate actual satisfaction.

### Handling Missing Data

Common strategies include:

* Leaving values missing and reporting missingness explicitly
* Imputing values using a rule or model
* Adding a “missing” category for categorical fields
* Excluding incomplete records where justified
* Fixing the upstream process so the issue stops recurring

The correct choice depends on the analysis objective. It is usually better to preserve the fact that data is missing than to fill values without justification.

---

## Duplicate Data

Duplicate data occurs when the same real-world entity, event, or record appears more than once when it should appear once.

### Common Causes

* Repeated system loads
* Retry logic without deduplication
* Multiple source systems describing the same entity
* Weak or missing unique identifiers
* Manual data entry variations
* Many-to-many joins performed incorrectly

### Types of Duplicates

* **Exact duplicates:** all fields match
* **Key duplicates:** rows share a supposedly unique ID
* **Near duplicates:** records likely refer to the same entity but differ slightly
* **Semantic duplicates:** multiple records represent the same event from different systems

### Why Duplicates Matter

Duplicates can:

* Overstate totals and event counts
* Inflate conversion and activity metrics
* Create confusion about the latest or authoritative record
* Lead to inconsistent customer views
* Break downstream matching and attribution logic

Deduplication is rarely just a technical cleanup step. It requires decisions about the dataset’s grain, the authoritative source, and the logic for selecting a surviving record.

---

## Inconsistent Definitions

One of the most damaging quality issues is not a malformed value, but a mismatch in meaning.

### What This Looks Like

* “Active customer” means one purchase in 30 days for one team and one login in 90 days for another.
* Revenue includes refunds in one report and excludes them in another.
* A “new user” is defined by signup date in one dashboard and first purchase date in another.

### Why It Happens

* Different teams build metrics independently
* Business rules change over time
* Definitions are embedded in code rather than documented centrally
* Source systems use similar field names with different semantics

### Why It Is Dangerous

Inconsistent definitions produce clean-looking numbers that disagree. This is often worse than obviously broken data because the issue is harder to detect. Stakeholders may assume the discrepancy reflects business reality rather than definitional mismatch.

### Mitigation

* Maintain a metric dictionary or semantic layer
* Standardize business definitions across reporting assets
* Version changes to definitions
* Document the exact logic behind KPIs and derived fields
* Review definitions with stakeholders, not just engineers

---

## Outliers and Anomalies

Outliers and anomalies are values or patterns that differ markedly from expectations. They are not automatically errors.

### Outliers vs Anomalies

* **Outlier:** an extreme value relative to a distribution
* **Anomaly:** a broader irregularity, such as a sudden spike, unexpected sequence, or unusual pattern

Examples:

* An order amount 100 times larger than normal
* Daily traffic dropping to zero
* A user generating thousands of events in seconds
* Negative inventory counts

### Possible Explanations

* Legitimate rare events
* Data entry mistakes
* Unit conversion problems
* System bugs
* Fraud or abuse
* Process changes or one-off campaigns

### Analytical Approach

Do not immediately remove outliers. First determine whether they reflect:

1. genuine business behavior,
2. a known exception,
3. or a data quality problem.

Analysts often compare the suspicious values against:

* historical ranges,
* peer groups,
* business rules,
* external events,
* or raw source records.

Outlier treatment should be documented because it can materially affect averages, forecasts, and model performance.

---

## Data Drift

**Data drift** refers to changes in data patterns over time that can affect analysis, monitoring, and modeling.

### Types of Drift

* **Distribution drift:** the frequency or range of values changes
* **Schema drift:** columns, types, or formats change unexpectedly
* **Definition drift:** a field’s meaning changes over time
* **Behavioral drift:** user or system behavior changes, altering the data-generating process

Examples:

* A categorical field gains new values after a product launch
* Event volumes shift after an app redesign
* A text field once used for free-form notes becomes structured codes
* Customer acquisition sources change mix over time

### Why Drift Matters

Drift can:

* Break dashboards and ETL pipelines
* Make historical comparisons misleading
* Degrade model accuracy
* Create false alerts or hide real issues
* Cause silently wrong interpretations if analysts assume stability

### Monitoring Drift

Analysts and data teams monitor drift using:

* row count and volume checks,
* distribution comparisons,
* null-rate tracking,
* distinct-count tracking,
* schema change detection,
* and alerting thresholds.

Drift is especially important in recurring reports, production pipelines, and machine learning workflows.

---

## Data Quality Assessment Frameworks

A data quality assessment framework provides a structured way to evaluate, prioritize, and manage quality issues.

### 1. Define the Use Case

Quality should be assessed relative to a business purpose:

* executive reporting,
* operational monitoring,
* forecasting,
* experimentation,
* regulatory submission,
* customer-facing applications.

A field that is “good enough” for one purpose may be unacceptable for another.

### 2. Define the Expected Grain and Rules

Clarify:

* what each row represents,
* what the primary key should be,
* which fields are mandatory,
* which value ranges are allowed,
* what reference data should be used,
* and how freshness is measured.

Without this, quality checks become vague and inconsistent.

### 3. Assess the Data Across Key Dimensions

Typical dimensions include:

* accuracy,
* completeness,
* consistency,
* validity,
* uniqueness,
* timeliness.

Assessment may combine automated tests, manual review, reconciliation, and stakeholder feedback.

### 4. Quantify Severity and Impact

Not all issues matter equally. A framework should classify issues by:

* affected records,
* affected metrics,
* business impact,
* frequency,
* detectability,
* and urgency.

A typo in a free-text comment field is not equivalent to duplicate invoice payments.

### 5. Assign Ownership

Every important dataset should have clarity around:

* data producer,
* data steward,
* technical owner,
* and business owner.

Quality problems persist when nobody owns the fix.

### 6. Monitor Continuously

Quality is not a one-time audit. Systems, definitions, and user behavior change. Good frameworks include recurring checks, alerting, issue tracking, and review.

---

## Data Validation Rules

Data validation rules are explicit tests used to detect quality issues. They can be applied at data entry, ingestion, transformation, storage, or reporting time.

### Common Categories of Validation Rules

#### Required Field Rules

Ensure mandatory fields are present.

Examples:

* `customer_id must not be null`
* `order_date is required for all completed orders`

#### Type and Format Rules

Ensure values match expected types and structures.

Examples:

* `invoice_amount must be numeric`
* `email must match expected format`
* `event_timestamp must be a valid datetime`

#### Domain Rules

Restrict values to an allowed set.

Examples:

* `status must be one of: pending, shipped, cancelled, returned`
* `country_code must exist in the approved reference table`

#### Range Rules

Check whether values fall within acceptable bounds.

Examples:

* `discount_percent must be between 0 and 100`
* `age must be between 0 and 120`

#### Uniqueness Rules

Protect the expected grain of the dataset.

Examples:

* `transaction_id must be unique`
* `one active subscription per account`

#### Referential Integrity Rules

Ensure relationships between tables are valid.

Examples:

* every `order.customer_id` must exist in `customers.customer_id`
* every `sales_rep_id` must map to a valid employee record

#### Conditional Rules

Apply logic based on context.

Examples:

* `ship_date must be present if order_status = shipped`
* `termination_date must be null when employee_status = active`

#### Freshness Rules

Verify timely arrival or update.

Examples:

* daily file must arrive by 6:00 AM
* events table must be updated within 15 minutes of source generation

#### Reconciliation Rules

Compare totals across systems or process stages.

Examples:

* order count in warehouse table should match count from source extract within tolerance
* daily revenue in BI layer should reconcile to finance-approved ledger total

### Characteristics of Good Validation Rules

Good rules are:

* specific,
* testable,
* tied to business meaning,
* automated where possible,
* and reviewed when processes change.

A rule that is too vague, too broad, or disconnected from business logic will not provide reliable protection.

---

## Documenting Quality Issues

A quality issue that is found but not documented will usually recur, be rediscovered later, or be misunderstood by downstream users.

### What to Document

For each issue, capture:

* **Issue name:** concise label
* **Description:** what is wrong
* **Affected dataset or table:** where it occurs
* **Affected fields:** columns or metrics impacted
* **Observed symptoms:** null spike, duplicate rows, mismatched totals, etc.
* **Business impact:** how decisions or outputs are affected
* **Severity:** low, medium, high, critical
* **Detection method:** query, validation rule, user complaint, audit, monitoring alert
* **Date discovered:** when it was first observed
* **Owner:** who is responsible for investigation or remediation
* **Root cause:** if known
* **Workaround:** temporary mitigation for analysts or users
* **Resolution status:** open, in progress, resolved, accepted limitation
* **Preventive action:** what will stop recurrence

### Why Documentation Matters

Documentation helps teams:

* avoid repeating the same mistakes,
* communicate caveats clearly,
* prioritize remediation,
* preserve context across team changes,
* and build trust by being transparent.

For analysts, documenting issues is part of responsible communication. It is better to state that a metric is provisional due to a known completeness issue than to present it as fully reliable.

### Example Issue Log Entry

| Field            | Example                                                      |
| ---------------- | ------------------------------------------------------------ |
| Issue name       | Duplicate order records in daily sales table                 |
| Description      | Some orders are loaded twice after ingestion retries         |
| Affected dataset | `sales_daily_fact`                                           |
| Affected fields  | `order_id`, revenue, order count                             |
| Business impact  | Revenue and order totals overstated by 1.8% on affected days |
| Severity         | High                                                         |
| Detection method | Uniqueness validation on `order_id`                          |
| Owner            | Data engineering                                             |
| Workaround       | Deduplicate by latest ingestion timestamp before reporting   |
| Status           | In progress                                                  |

---

## Practical Workflow for Analysts

A practical analyst workflow for data quality often looks like this:

### 1. Understand the Data’s Intended Use

Before checking quality, understand:

* what decision the dataset supports,
* what grain it should have,
* what fields are critical,
* and what level of error is tolerable.

### 2. Profile the Data

Basic profiling includes:

* row counts,
* null rates,
* distinct counts,
* min/max values,
* value distributions,
* duplicate checks,
* and date coverage.

This quickly reveals obvious issues and helps establish a baseline.

### 3. Test Key Assumptions

Examples:

* one row per transaction,
* no negative quantities,
* timestamps within expected range,
* reference IDs exist in parent tables,
* daily volumes within normal range.

### 4. Investigate Exceptions

When a check fails, determine:

* whether the issue is real,
* how widespread it is,
* whether it is new or ongoing,
* and whether it affects the current analysis materially.

### 5. Decide on Treatment

Possible actions:

* exclude affected rows,
* transform or standardize values,
* impute missing fields,
* reconcile against another source,
* flag the limitation and proceed carefully,
* or stop the analysis until the issue is resolved.

### 6. Communicate Clearly

State:

* what was checked,
* what failed,
* what treatment was applied,
* what remains uncertain,
* and how the issue affects interpretation.

---

## Common Trade-offs in Data Quality

Data quality work often involves trade-offs rather than perfect solutions.

### Speed vs Rigor

A fast operational decision may require using imperfect but timely data. A financial close may require slower but highly controlled data.

### Coverage vs Precision

Including more records may increase completeness but also include noisier or less validated data.

### Automation vs Judgment

Automated checks catch many issues, but some problems—especially definitional inconsistency and semantic drift—require human review.

### Correction vs Transparency

Some issues can be corrected algorithmically, but every correction introduces assumptions. When assumptions are strong, transparency is essential.

---

## Good Practices

### Build Quality Checks Early

It is easier to prevent bad data from entering the system than to repair it downstream. Validation at point of entry and ingestion is typically cheaper than late-stage cleanup.

### Tie Checks to Business Meaning

A rule like “field must be non-null” is useful, but “completed orders must have payment confirmation” is more meaningful because it reflects the process being measured.

### Use Reference Data and Standard Definitions

Reference tables, controlled vocabularies, metric dictionaries, and semantic layers reduce inconsistency.

### Monitor Over Time

A dataset that passed checks last month may fail this month. Trend monitoring is necessary for timeliness, drift, and operational stability.

### Treat Documentation as Part of the Analysis

Caveats, assumptions, and known issues should travel with dashboards, notebooks, reports, and metric definitions.

---

## Red Flags Analysts Should Notice

Analysts should be cautious when they see:

* sudden row-count changes,
* unexpected null spikes,
* duplicate IDs,
* unexplained metric jumps,
* new categorical values,
* impossible dates or negative quantities,
* mismatches between sources,
* fields used inconsistently across teams,
* or stale data in supposedly current reports.

These do not always mean the data is unusable, but they do require investigation.

---

## Key Takeaways

* Data quality means fitness for use, not abstract perfection.
* The main quality dimensions include **accuracy, completeness, consistency, validity, uniqueness, and timeliness**.
* Common problems include **missing data, duplicates, inconsistent definitions, outliers, anomalies, and data drift**.
* Quality assessment should be structured, use-case-specific, and ongoing.
* Validation rules should reflect both technical correctness and business logic.
* Quality issues must be documented clearly, including impact, ownership, and remediation status.
* Strong analysis depends not only on technical skill, but on disciplined skepticism about the data itself.

---

## Review Questions

1. Why is data quality relative to use case rather than absolute?
2. How do completeness and accuracy differ?
3. Why are inconsistent definitions often harder to detect than invalid values?
4. When should an analyst keep outliers rather than remove them?
5. How does data drift affect recurring analysis and modeling?
6. What kinds of validation rules would you apply to a transaction table?
7. What information should be included when documenting a quality issue?

---

## Practice Exercise

Choose a dataset and evaluate it using the following checklist:

1. Define the grain of the dataset.
2. Identify the most important fields for the analysis.
3. Check completeness of required fields.
4. Test uniqueness of the expected key.
5. Validate formats, domains, and ranges.
6. Look for inconsistent categories or definitions.
7. Examine outliers and unusual patterns.
8. Assess freshness and time coverage.
9. Record all issues found, their likely impact, and any assumptions used in treatment.

This exercise helps build the habit of treating data quality as a core analytical responsibility rather than a final cleanup step.
