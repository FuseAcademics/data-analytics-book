# Data Collection and Data Generation

Data analysis begins long before a dashboard, query, or model. It begins where data is created, captured, and stored. Analysts who understand how data is collected make better decisions about data quality, interpretation, bias, and fitness for use.

This chapter explains the major ways data is generated in modern organizations, the limitations of different collection methods, and the practical risks that appear before analysis even starts.

---

## Why Data Collection Matters

Collected data is not a neutral mirror of reality. It is shaped by:

* the system that records it
* the people or devices producing it
* the business process around it
* the definitions used at the time of capture
* incentives, errors, and missing context

Two datasets may appear similar while representing very different underlying processes. For example, a “customer” table might include only paying users in one system but all registered accounts in another. A “click” event might represent a real interaction in one product and an auto-generated tracking event in another.

Analysts should therefore ask not only **what the data says**, but also:

* How was it created?
* Who or what generated it?
* Under what conditions?
* What is missing?
* What kinds of errors are likely?

---

## Operational Systems

Operational systems are the systems that run day-to-day business processes. They are often the original source of data used for analytics.

Common examples include:

* transaction processing systems
* customer relationship management systems
* enterprise resource planning systems
* ecommerce platforms
* billing systems
* support ticketing systems
* human resources systems

These systems are usually built for running the business, not for analysis.

### Characteristics of Operational Data

Operational data is often:

* highly structured
* updated frequently
* tied to specific business processes
* optimized for speed and accuracy of transactions
* subject to rules, permissions, and workflow constraints

For example:

* a retail system records orders, refunds, and shipments
* a banking system records deposits, withdrawals, and balances
* a hospital system records appointments, diagnoses, and billing events

### Analytical Implications

Operational systems are valuable because they often reflect real business activity at a detailed level. However, they can be difficult to analyze directly because:

* schemas are designed for application logic, not analytical convenience
* fields may use system-specific codes
* important historical changes may be overwritten
* multiple systems may represent the same entity differently
* business logic may live in the application rather than the database

### Example

An order management system may contain:

* one table for orders
* another for line items
* another for payments
* another for fulfillment status
* another for returns

A simple question such as “What was net revenue last month?” may require joining several tables and understanding business rules around taxes, cancellations, and refunds.

### Analyst Guidance

When working with operational data:

* learn the business process behind the system
* identify system-of-record sources
* understand update timing and latency
* confirm definitions of key fields
* check whether records are current-state or historical-state

---

## Surveys and Forms

Surveys and forms collect data directly from people through structured questions and responses. They are common in market research, employee feedback, customer satisfaction programs, lead capture, applications, and internal workflows.

### Common Sources

* online surveys
* registration forms
* feedback forms
* assessment questionnaires
* onboarding forms
* polls and interviews with structured responses

### Strengths

Surveys are useful because they can capture information not available in operational systems, such as:

* opinions
* preferences
* expectations
* self-reported behaviors
* demographic information
* satisfaction or sentiment

A transaction database can show what a customer bought. A survey may show why they bought it, whether they were satisfied, and what they intended to do next.

### Weaknesses

Survey data has important limitations:

* respondents may misunderstand questions
* respondents may skip questions
* answers may be inaccurate or biased
* question wording can influence results
* response rates may be low
* certain groups may be overrepresented or underrepresented

### Common Survey Biases

#### Response Bias

People may answer in ways they think are socially acceptable, strategically beneficial, or expected.

#### Nonresponse Bias

Those who choose not to respond may differ systematically from those who do respond.

#### Recall Bias

People may not accurately remember past events or behaviors.

#### Question Framing Effects

Small wording changes can change how people interpret and answer questions.

### Form Design Considerations

Good form design improves data quality. Important considerations include:

* clear wording
* mutually exclusive response options
* consistent units and scales
* validation rules
* required vs optional fields
* logic for conditional questions
* minimal ambiguity

### Analyst Guidance

Before analyzing survey data, check:

* who was invited to respond
* who actually responded
* response rate by segment
* missingness patterns
* question wording and answer choices
* whether the survey was anonymous or identifiable

---

## Logs and Event Streams

Logs and event streams record actions, states, or system messages over time. They are central to product analytics, software monitoring, security analysis, and digital behavior tracking.

### What They Capture

Common logged events include:

* page views
* button clicks
* searches
* purchases
* login attempts
* API requests
* errors and exceptions
* device or session activity

### Logs vs Event Streams

The terms are related but not identical.

* **Logs** often describe system-generated records used for debugging, monitoring, or auditing.
* **Event streams** more often refer to structured sequences of business or product events that occur over time and may be processed continuously.

### Characteristics

Event data is usually:

* high volume
* time-stamped
* append-oriented
* granular
* sometimes semi-structured

An event record might include:

* event name
* timestamp
* user ID
* session ID
* device type
* page or screen
* attributes specific to the action

### Advantages

Logs and event streams can provide:

* fine-grained behavioral data
* near real-time visibility
* sequence and timing information
* data for funnels, retention, journeys, and anomaly detection

### Challenges

Event data often contains quality issues such as:

* duplicate events
* missing events
* inconsistent naming
* schema drift over time
* client-side tracking failures
* bot or automated traffic
* out-of-order timestamps
* differences between frontend and backend events

### Example

A product team may want to analyze checkout conversion. That depends on whether events such as `view_cart`, `begin_checkout`, `enter_payment`, and `purchase_complete` are consistently defined and reliably tracked. If one step is under-instrumented, the funnel can appear worse than reality.

### Analyst Guidance

For event data, verify:

* event taxonomy and naming standards
* instrumentation coverage
* timestamp source and timezone
* identity resolution across devices or sessions
* deduplication logic
* changes in tracking implementations over time

---

## APIs and Third-Party Data

Organizations often consume data from external systems through APIs, flat-file deliveries, purchased datasets, partner integrations, or public data portals.

### Examples

* payment provider APIs
* ad platform data
* social media metrics
* weather data
* mapping data
* financial market data
* demographic or geographic datasets
* vendor enrichment data

### API-Based Collection

An API allows one system to request data from another in a structured way. API data collection may be:

* real-time
* scheduled in batches
* triggered by specific events

### Benefits

Third-party data can:

* fill gaps in internal data
* enrich existing records
* provide broader market context
* enable benchmarking
* support forecasting or segmentation

### Risks and Limitations

External data introduces dependencies and interpretation risks:

* data definitions may differ from internal definitions
* coverage may be incomplete
* access may be rate-limited or delayed
* providers may change schemas or endpoints
* historical backfills may be unavailable
* licensing or usage restrictions may apply
* quality control may be outside your organization’s control

### Matching and Integration Problems

Joining third-party data to internal data can be difficult. Common issues include:

* inconsistent identifiers
* partial address or name matching
* duplicates
* stale enrichment attributes
* mismatched time periods
* missing metadata about collection methods

### Analyst Guidance

When using external data, document:

* source provider
* extraction date and frequency
* terms of use
* field definitions
* known coverage limitations
* matching methodology
* assumptions made during integration

---

## Sensors and IoT

Sensors and Internet of Things devices generate machine-produced data from physical environments. These sources are common in manufacturing, logistics, smart buildings, healthcare, transportation, agriculture, and energy systems.

### Examples

* temperature sensors
* GPS trackers
* motion detectors
* wearables
* smart meters
* production line sensors
* vehicle telemetry
* environmental monitors

### Characteristics

Sensor data is often:

* continuous or high-frequency
* time-series in nature
* device-generated rather than human-entered
* subject to calibration and hardware conditions
* noisy and sometimes incomplete

### Advantages

Sensor data enables measurement of physical processes with a level of precision and frequency that would be difficult through manual observation.

Examples include:

* monitoring machine performance in real time
* tracking delivery routes and delays
* measuring patient vital signs
* detecting environmental anomalies

### Common Problems

Sensor and IoT data can suffer from:

* device failure
* calibration drift
* intermittent connectivity
* power loss
* missing intervals
* measurement noise
* inconsistent firmware behavior
* unit inconsistencies across devices

### Example

A temperature reading of 85 may be valid, suspicious, or meaningless depending on whether the unit is Celsius or Fahrenheit, whether the sensor is indoors or outdoors, and whether the device was recently recalibrated.

### Analyst Guidance

For sensor data, confirm:

* measurement units
* sampling frequency
* device identifiers
* calibration procedures
* timezone handling
* expected operating ranges
* maintenance events that may affect readings

---

## Experimental Data

Experimental data is produced when conditions are deliberately varied to measure causal effects. This type of data is common in scientific research, product experimentation, marketing testing, operations improvement, and policy evaluation.

### Examples

* A/B tests
* randomized controlled trials
* pricing experiments
* email subject-line tests
* process improvement trials
* clinical experiments

### Key Feature

The defining feature of experimental data is that the researcher or organization actively assigns treatments, conditions, or interventions rather than merely observing what happens naturally.

### Why It Matters

Experiments help answer causal questions such as:

* Did the new onboarding flow improve activation?
* Did the promotion increase sales?
* Did the training program improve performance?

This is different from observational analysis, which often identifies associations but cannot as easily isolate cause and effect.

### Components of Experimental Data

Experimental datasets often include:

* subject or unit ID
* treatment assignment
* control condition
* outcome measures
* pre-treatment variables
* timestamps
* exposure indicators
* eligibility criteria

### Common Risks

Even experiments can fail or mislead when there is:

* poor randomization
* sample imbalance
* contamination between groups
* noncompliance
* attrition
* small sample size
* measurement errors
* premature stopping

### Analyst Guidance

When analyzing experimental data, verify:

* unit of randomization
* assignment method
* treatment and control definitions
* exposure logging
* exclusion rules
* experiment start and stop dates
* whether outcomes were predefined

---

## Manual Data Entry Issues

Not all data is captured automatically. Many important datasets still depend on humans typing values into forms, spreadsheets, or operational systems.

### Common Contexts

* customer service notes
* CRM updates
* reimbursement forms
* inventory adjustments
* medical coding
* compliance records
* spreadsheet-based reporting
* case management systems

### Frequent Errors

Manual entry introduces predictable problems:

* typos
* inconsistent spelling
* missing values
* incorrect dates
* wrong units
* duplicated records
* free-text variation
* copy-paste mistakes
* default values left unchanged

### Standardization Problems

One user may enter “United States,” another “USA,” and another “US.” One may enter phone numbers with country codes and another without. Dates may appear in multiple formats. Product names may be abbreviated inconsistently.

These inconsistencies complicate grouping, joining, and reporting.

### Incentive and Process Effects

Manual entry errors are not just individual mistakes. They often reflect process design:

* fields may be unclear
* users may be rushed
* validation rules may be weak
* training may be inconsistent
* certain fields may not be important to the person entering the data

If a salesperson sees a field as bureaucratic rather than useful, completion quality may be poor even if the field is technically required.

### Analyst Guidance

When working with manually entered data:

* profile categorical values for inconsistencies
* examine null rates by field and team
* look for out-of-range values
* standardize formats before analysis
* identify which fields are system-enforced versus optional
* understand who enters the data and why

---

## Sampling and Observational Limitations

Not all data represents the full population of interest. Many datasets are samples, partial records, or observational traces shaped by who or what was measured.

Understanding sampling and observational limitations is essential for drawing valid conclusions.

---

## Sampling

Sampling means analyzing a subset of a larger population.

### Why Sampling Happens

Organizations use samples because collecting all possible data may be:

* too expensive
* too slow
* technically impossible
* unnecessary for the decision at hand

### Common Sampling Approaches

#### Random Sampling

Each unit has a known chance of selection. This is often preferred because it reduces selection bias.

#### Stratified Sampling

The population is divided into groups, and samples are taken within each group to improve representation.

#### Convenience Sampling

Data is collected from what is easiest to access. This is common but often biased.

#### Systematic Sampling

Every nth item is selected after a starting point.

### Sampling Risks

Poor sampling can produce misleading results when:

* certain groups are excluded
* sample sizes are too small
* response patterns differ across segments
* weights are ignored
* the sampling frame does not match the true population

### Example

A customer survey sent only to active app users cannot represent all customers if many customers use the website only or have become inactive.

---

## Observational Data

Observational data records what happened without experimental control. Much of business analytics uses observational data.

### Examples

* sales transactions
* website activity
* medical records
* public policy outcomes
* customer behavior in production systems

### Key Limitation

With observational data, groups often differ for many reasons at once. This makes causal claims difficult.

For example, customers who saw a premium offer may differ systematically from those who did not. If premium users are targeted differently, observed differences in outcomes may reflect selection effects rather than treatment effects.

### Common Observational Problems

#### Selection Bias

The observed sample differs systematically from the target population.

#### Survivorship Bias

Only entities that remain visible are included, while failures or dropouts disappear from view.

#### Confounding

A third factor influences both the explanatory variable and the outcome.

#### Measurement Bias

The way data is captured systematically distorts the observed value.

#### Missing Data

Missingness may not be random. For example, higher-risk cases may be less likely to have complete information.

### Analyst Guidance

When using sampled or observational data:

* define the target population clearly
* identify how records entered the dataset
* ask who is missing and why
* avoid making causal claims without proper design
* distinguish between correlation and causation
* document known representational limits

---

## Comparing Data Collection Methods

| Source Type               | Typical Strengths                                              | Common Weaknesses                                            |
| ------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------ |
| Operational systems       | Detailed business records, process-linked, often authoritative | Designed for operations, not analysis; may overwrite history |
| Surveys and forms         | Captures attitudes, intent, demographics, feedback             | Subject to response bias, wording effects, nonresponse       |
| Logs and event streams    | High-volume behavioral detail, near real-time                  | Duplicates, missing events, instrumentation issues           |
| APIs and third-party data | Enrichment, broader context, external coverage                 | Limited control, schema changes, coverage gaps               |
| Sensors and IoT           | Continuous physical measurement, high frequency                | Noise, calibration issues, missing intervals                 |
| Experimental data         | Best support for causal inference                              | Requires careful design and execution                        |
| Manual data entry         | Flexible, often necessary for business processes               | Human error, inconsistency, missingness                      |

---

## Questions Analysts Should Always Ask

Before trusting a dataset, ask:

1. **What process created this data?**
2. **Who or what generated each record?**
3. **What event causes a record to appear?**
4. **What definitions were used at collection time?**
5. **What fields are optional, derived, or system-generated?**
6. **What kinds of errors are most likely?**
7. **Who is missing from this dataset?**
8. **How often is the data updated or corrected?**
9. **What changed over time in the collection process?**
10. **Is this data suitable for the decision I need to support?**

These questions often matter more than advanced statistical techniques.

---

## Practical Example: Same Metric, Different Origins

Consider the metric **daily active users**.

It may be generated from:

* login records in an operational authentication system
* frontend event streams tracking app opens
* backend API request logs
* survey responses asking whether users used the product today

Each source may produce a different number because each captures a different definition of “active.” Without understanding the data generation process, the metric can be misinterpreted or argued over endlessly.

---

## Best Practices for Working with Collected Data

### Trace Data Back to Its Source

Whenever possible, identify the original system or collection mechanism rather than relying only on downstream tables or dashboards.

### Learn the Process, Not Just the Schema

A column name rarely tells the full story. Business workflow and operational behavior matter.

### Document Definitions

Keep notes on field meanings, event definitions, survey wording, and collection rules.

### Expect Data Quality Problems

Assume every source has failure modes. Your job is to discover and quantify them.

### Separate Measurement from Interpretation

A recorded value is not automatically the same as the real-world concept you care about.

### Reassess Over Time

Data collection methods change. New app versions, revised forms, new vendors, and updated business rules can all affect comparability.

---

## Common Mistakes

Analysts often make avoidable errors at the collection stage by:

* assuming system data is automatically accurate
* treating survey results as representative without checking response patterns
* trusting event counts without validating instrumentation
* ignoring schema or tracking changes over time
* using third-party data without understanding coverage and licensing
* making causal claims from observational data
* overlooking manual entry errors because the dataset “looks clean”

---

## Summary

Data is generated through systems, people, devices, and designed interventions. Each source has its own structure, strengths, and limitations.

A capable analyst understands that:

* operational systems reflect business processes
* surveys capture perceptions but introduce response bias
* logs and event streams reveal behavior but depend on reliable instrumentation
* APIs and third-party data add value but reduce control
* sensors provide continuous measurement but may be noisy or incomplete
* experiments support causal analysis when designed properly
* manual entry often creates inconsistency and error
* samples and observational datasets may not represent the full population or support strong causal conclusions

The quality of analysis depends heavily on understanding where data came from and what it truly represents.

---

## Key Terms

**Operational system**
A system used to run day-to-day business processes and record transactions.

**Survey data**
Data collected from respondents through structured questions.

**Event stream**
A sequence of time-stamped records describing actions or state changes.

**API**
An interface that allows systems to exchange data programmatically.

**IoT**
Internet of Things; connected devices that collect and transmit data.

**Experimental data**
Data produced under controlled conditions where treatments or interventions are assigned.

**Sampling**
Selecting a subset of a population for measurement or analysis.

**Observational data**
Data collected without controlling or assigning treatments.

**Selection bias**
Bias caused by systematic differences in who is included in the data.

**Confounding**
A distortion in the relationship between variables caused by an omitted related factor.

---

## Review Questions

1. Why can operational system data be difficult to analyze directly?
2. What are the main risks in survey-based data collection?
3. How do logs and event streams differ from traditional transactional records?
4. What are common failure modes in sensor-generated data?
5. Why is external API or vendor data often harder to interpret than internal data?
6. What makes experimental data different from observational data?
7. What kinds of errors are common in manual data entry?
8. Why must analysts think carefully about sampling and representativeness?
9. What is the difference between a recorded event and the concept it is meant to measure?
10. Why should analysts document changes in data collection methods over time?

---

## In Practice

When you receive a dataset, do not begin with charts. Begin with source questions:

* Where did this come from?
* What process generated it?
* What could have gone wrong?
* What population does it represent?
* What does it fail to capture?

Those questions are the foundation of sound analysis.
