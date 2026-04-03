# Data Fundamentals

Data fundamentals provide the vocabulary and structure needed to work with data correctly. Many analytical errors do not come from advanced statistics or tooling; they come from misunderstanding what the data actually represents. Before cleaning, querying, visualizing, or modeling data, an analyst needs to understand the dataset, its level of detail, its entities, and the meaning of each field.

This chapter introduces the core concepts that sit underneath almost every analytics workflow: datasets, rows and columns, granularity, keys, facts, dimensions, measures, attributes, and metadata. These are foundational ideas for spreadsheets, SQL tables, dashboards, notebooks, data warehouses, and machine learning datasets alike.

---

## What a Dataset Is

A **dataset** is an organized collection of data about one or more entities, events, or processes. It is usually structured so that each item can be stored, retrieved, filtered, and analyzed consistently.

A dataset may exist in many forms:

* a spreadsheet
* a database table
* a CSV or Parquet file
* a JSON export
* a data warehouse model
* the result of a SQL query
* a collection of related tables

In practice, people often use the word dataset broadly. Sometimes it refers to a single table, and sometimes it refers to a whole group of related tables that together represent a domain such as customers, orders, products, and payments.

A dataset is useful only when its structure and meaning are clear. The same values can support very different analyses depending on what each row represents, how each variable is defined, and what level of detail is stored.

### Example

Consider a sales dataset:

| order_id | customer_id | order_date | product_id | quantity | revenue |
| -------- | ----------: | ---------- | ---------: | -------: | ------: |
| O1001    |        C201 | 2026-01-03 |        P10 |        2 |   40.00 |
| O1001    |        C201 | 2026-01-03 |        P11 |        1 |   15.00 |
| O1002    |        C305 | 2026-01-03 |        P10 |        1 |   20.00 |

This looks simple, but even here the analyst must ask:

* Is each row an order or an order line?
* Is revenue gross or net of discounts?
* Is quantity in units, boxes, or kilograms?
* Can the same order appear in multiple rows?

Those questions are not secondary details. They determine what the dataset can validly answer.

---

## Rows, Columns, Records, Variables, and Observations

These terms are often used interchangeably in casual discussion, but they are not always identical. Understanding the distinctions improves precision.

### Rows

A **row** is a horizontal entry in a table. It represents one stored instance in the dataset.

In a spreadsheet, each line is a row. In a database table, each stored tuple is a row. Rows are usually the basic unit of storage and filtering.

### Columns

A **column** is a vertical field in a table. It holds one kind of information across rows.

Examples:

* `customer_id`
* `signup_date`
* `country`
* `revenue`

Columns define the schema or structure of the dataset.

### Records

A **record** is a complete collection of values describing one row-level entity or event. In many practical cases, a record and a row mean the same thing.

For example, one employee record may include:

* employee ID
* name
* department
* hire date
* salary band

### Variables

A **variable** is a characteristic or property that can take different values across observations.

In analytics, a variable usually corresponds to a column, though the term comes more from statistics than from databases.

Examples:

* age
* region
* churn status
* monthly spend

A variable may be numeric, categorical, binary, temporal, or textual.

### Observations

An **observation** is one instance measured or recorded in the data. In tidy tabular datasets, one observation usually corresponds to one row.

For example:

* one customer
* one transaction
* one website session
* one patient visit
* one survey response

### Practical View

In many business datasets:

* **row** describes storage structure
* **record** describes the stored entity/event
* **variable** describes the field being measured
* **observation** describes the analytical unit

These often align, but not always. For instance, in nested JSON or event logs, one logical observation may span multiple rows after transformation.

---

## Data Granularity

**Data granularity** refers to the level of detail represented by each row in a dataset.

This is one of the most important concepts in analytics. If granularity is misunderstood, aggregations, joins, comparisons, and KPIs can all become wrong.

### High Granularity vs Low Granularity

A dataset with **high granularity** contains very detailed records.

Example:

* one row per click
* one row per sensor reading
* one row per order item

A dataset with **low granularity** contains more aggregated records.

Example:

* one row per day
* one row per customer per month
* one row per store per quarter

Neither is inherently better. The correct granularity depends on the decision being supported.

### Examples

#### Transaction-level granularity

| transaction_id | customer_id | transaction_time | amount |
| -------------- | ----------- | ---------------- | -----: |
| T1             | C1          | 2026-01-01 09:15 |  25.00 |
| T2             | C1          | 2026-01-01 14:20 |  18.00 |

Each row is one transaction.

#### Daily summary granularity

| date       | customer_id | total_transactions | total_amount |
| ---------- | ----------- | -----------------: | -----------: |
| 2026-01-01 | C1          |                  2 |        43.00 |

Each row is one customer-day summary.

These datasets can answer different questions. The first supports sequence analysis, basket analysis, and time-between-purchases. The second supports daily trend analysis but cannot recover the original transaction timing.

### Why Granularity Matters

Granularity affects:

* what questions can be answered
* how data should be aggregated
* whether joins will duplicate values
* whether counts are distinct or raw
* how KPIs should be defined
* whether metrics are additive across dimensions

A common mistake is joining a lower-granularity table to a higher-granularity table without accounting for duplication. For example, joining customer-level data to transaction-level data and then summing customer-level revenue targets can inflate totals.

### Always Ask

When working with a dataset, ask:

* What does one row represent?
* Is this event-level, entity-level, or aggregated data?
* Can an entity appear multiple times?
* Over what time period is each row defined?
* What granularity do I need for the analysis?

---

## Units of Analysis

The **unit of analysis** is the main entity or event being studied in an analysis.

It answers the question:

> What exactly am I analyzing?

The unit of analysis may or may not match the storage format directly, but it should always be explicit.

### Examples

| Business Question                                     | Unit of Analysis              |
| ----------------------------------------------------- | ----------------------------- |
| Which customers are likely to churn?                  | Customer                      |
| What products have the highest return rate?           | Product or product order line |
| How has daily revenue changed?                        | Day                           |
| Which marketing campaigns drive the most conversions? | Campaign or campaign-day      |
| How long do support tickets remain open?              | Ticket                        |

### Unit of Analysis vs Dataset Row

Sometimes they are identical.

* one row per customer, analyzing customers

Sometimes they differ.

* one row per transaction, but analysis is at customer level
* one row per page view, but analysis is at session level
* one row per order line, but analysis is at order level

In such cases, analysts must aggregate or transform the data first.

### Why It Matters

A mismatch between the business question and the unit of analysis creates misleading results.

For example, if one analyst calculates average order value using order-line rows rather than order rows, the result may be distorted because orders with more items receive more weight.

A disciplined analyst states the unit of analysis early and ensures the dataset is aligned to it.

---

## Primary Keys and Foreign Keys

Relational data relies on keys to uniquely identify records and connect tables correctly.

### Primary Keys

A **primary key** is a column, or combination of columns, that uniquely identifies each row in a table.

Examples:

* `customer_id` in a customer table
* `order_id` in an orders table
* `product_id` in a products table
* `(order_id, line_number)` in an order items table

A good primary key should be:

* unique
* non-null
* stable over time
* specific to the entity represented by the table

### Foreign Keys

A **foreign key** is a column in one table that refers to the primary key of another table.

Examples:

* `customer_id` in `orders` refers to `customer_id` in `customers`
* `product_id` in `order_items` refers to `product_id` in `products`

Foreign keys create relationships between tables.

### Example Schema

#### Customers

| customer_id | customer_name | region |
| ----------- | ------------- | ------ |
| C1          | Asha          | East   |
| C2          | Ravi          | West   |

#### Orders

| order_id | customer_id | order_date |
| -------- | ----------- | ---------- |
| O1       | C1          | 2026-01-03 |
| O2       | C2          | 2026-01-04 |

Here:

* `customer_id` is the **primary key** in `customers`
* `order_id` is the **primary key** in `orders`
* `customer_id` in `orders` is a **foreign key** referencing `customers`

### Composite Keys

Sometimes a single column is not enough to uniquely identify a row. In those cases, a **composite key** uses multiple columns.

Example:

| order_id | line_number | product_id | quantity |
| -------- | ----------: | ---------- | -------: |
| O1       |           1 | P10        |        2 |
| O1       |           2 | P11        |        1 |

Here, `(order_id, line_number)` may be the primary key.

### Why Keys Matter

Keys support:

* deduplication
* accurate joins
* integrity checks
* entity tracking over time
* building dimensional models

Poor key design leads to duplicated rows, orphaned records, and invalid analysis.

### Common Problems

#### Non-unique supposed keys

A field is assumed to identify rows uniquely, but duplicates exist.

#### Natural key instability

Email addresses or product names may change over time and may not be reliable primary keys.

#### Missing foreign key matches

Orders may reference customers that do not exist in the customer table due to data quality issues.

#### Many-to-many joins

Two tables may both contain repeated values for the join key, producing unintended row multiplication.

Analysts should test key assumptions rather than trust them blindly.

---

## Facts and Dimensions

In analytical data modeling, especially in data warehousing, tables are often divided into **fact tables** and **dimension tables**.

### Fact Tables

A **fact table** stores measurable events or business processes. It usually contains numeric values and foreign keys to related dimensions.

Examples of facts:

* sales transactions
* website visits
* shipments
* claims
* support calls

A fact table is often large and grows over time.

#### Example fact table: `sales_fact`

| order_id | product_id | customer_id | date_id  | quantity | revenue |
| -------- | ---------- | ----------- | -------- | -------: | ------: |
| O1       | P10        | C1          | 20260103 |        2 |   40.00 |

This row records a business event and includes measurements such as quantity and revenue.

### Dimension Tables

A **dimension table** stores descriptive context used to categorize, filter, and group facts.

Examples of dimensions:

* customer
* product
* calendar date
* region
* channel
* salesperson

#### Example dimension table: `product_dim`

| product_id | product_name   | category    | brand |
| ---------- | -------------- | ----------- | ----- |
| P10        | Wireless Mouse | Accessories | Apex  |

This table describes products rather than recording transactions.

### Why This Distinction Exists

Fact/dimension modeling makes analysis easier by separating:

* **what happened** from
* **the descriptive context around what happened**

This supports efficient reporting, slicing metrics by categories, and consistent KPI definitions.

### Fact Table Characteristics

Fact tables usually have:

* many rows
* foreign keys to dimensions
* numeric measures
* business-event granularity

### Dimension Table Characteristics

Dimension tables usually have:

* fewer rows than facts
* descriptive fields
* one row per entity version or entity instance
* fields used for grouping, labeling, and filtering

### Example Questions

Using a sales fact table and product/customer/date dimensions, an analyst can answer:

* Revenue by month
* Units sold by product category
* Orders by customer segment
* Average order value by region

The fact table holds the measures. The dimensions provide the grouping logic.

---

## Measures and Attributes

Measures and attributes are related to facts and dimensions, but they refer more specifically to field roles within a dataset.

### Measures

A **measure** is a quantitative value that can usually be aggregated for analysis.

Examples:

* revenue
* cost
* quantity
* profit
* number of sessions
* call duration

Common aggregations include:

* sum
* average
* minimum
* maximum
* count
* median

Not every numeric field is a good measure. Some numbers are identifiers, codes, or rankings and should not be summed.

For example:

* `customer_id` is numeric in some systems, but it is not a measure
* `zip_code` may contain digits, but it is categorical

### Attributes

An **attribute** is a descriptive property used to characterize an entity or event.

Examples:

* customer region
* product category
* payment method
* subscription plan
* device type

Attributes help analysts segment, filter, and label data.

### Example

| order_id | region | category    | quantity | revenue |
| -------- | ------ | ----------- | -------: | ------: |
| O1       | East   | Electronics |        2 |     300 |

Here:

* `quantity` and `revenue` are **measures**
* `region` and `category` are **attributes**
* `order_id` is an **identifier**

### Additive, Semi-additive, and Non-additive Measures

Measures differ in how they should be aggregated.

#### Additive measures

Can be summed across all dimensions.

Examples:

* revenue
* units sold
* cost

#### Semi-additive measures

Can be summed across some dimensions but not all.

Example:

* account balance can be summed across customers, but not across time in the same way revenue can

#### Non-additive measures

Cannot be meaningfully summed.

Examples:

* percentages
* ratios
* averages

For instance, conversion rate should not usually be summed across groups. It should be recomputed from underlying counts.

### Analytical Importance

Clear separation between measures and attributes improves:

* dashboard design
* semantic layer modeling
* BI tool behavior
* metric definition
* aggregation correctness

A frequent reporting mistake is treating a precomputed rate as a raw measure and aggregating it incorrectly.

---

## Metadata and Data Dictionaries

Data is only useful when people know what it means. That supporting information is provided by **metadata** and **data dictionaries**.

### Metadata

**Metadata** is data about data. It describes the structure, origin, meaning, lineage, format, and usage of a dataset.

Examples of metadata:

* table name
* column names
* data types
* source system
* refresh schedule
* owner
* creation date
* last updated time
* allowed values
* business definitions
* nullability
* sensitivity classification

Metadata can be technical, business-oriented, or operational.

#### Technical metadata

Describes how data is stored.

Examples:

* data type
* schema
* partitioning
* file format
* index

#### Business metadata

Describes what data means in business terms.

Examples:

* definition of active customer
* meaning of revenue field
* distinction between booked and recognized revenue

#### Operational metadata

Describes how data is produced and maintained.

Examples:

* refresh cadence
* pipeline status
* upstream source
* owner team

### Data Dictionaries

A **data dictionary** is a structured reference document that defines the fields in a dataset.

It typically includes:

* column name
* business meaning
* data type
* allowed values
* example values
* null rules
* calculation logic
* units of measure
* notes on caveats

### Example Data Dictionary

| Field Name    | Type    | Definition                           | Example    | Notes                     |
| ------------- | ------- | ------------------------------------ | ---------- | ------------------------- |
| `customer_id` | string  | Unique identifier for a customer     | C1023      | Stable across systems     |
| `signup_date` | date    | Date the customer created an account | 2025-07-14 | UTC date                  |
| `plan_type`   | string  | Current subscription plan            | Pro        | One of Free, Basic, Pro   |
| `mrr`         | decimal | Monthly recurring revenue in USD     | 49.00      | Excludes one-time charges |

### Why Metadata Matters

Without metadata, analysts waste time and make preventable mistakes.

Common failures include:

* misunderstanding whether revenue is gross or net
* assuming timestamps are in local time when they are UTC
* treating nulls as zeros
* confusing status codes
* using deprecated fields
* joining on fields with different definitions across systems

A mature analytics environment treats documentation as part of the data product, not as optional overhead.

### Good Data Documentation Should Answer

* What does this dataset represent?
* What does one row represent?
* What is the grain?
* What does each field mean?
* How is it calculated?
* What values are valid?
* Where did it come from?
* How fresh is it?
* Who owns it?
* What are the known caveats?

---

## Putting the Concepts Together

Consider a simple retail model:

### Orders Fact

| order_id | customer_id | product_id | order_date | quantity | revenue |
| -------- | ----------- | ---------- | ---------- | -------: | ------: |
| O1       | C1          | P10        | 2026-01-03 |        2 |   40.00 |

### Customer Dimension

| customer_id | customer_name | region | segment |
| ----------- | ------------- | ------ | ------- |
| C1          | Asha          | East   | Premium |

### Product Dimension

| product_id | product_name | category    |
| ---------- | ------------ | ----------- |
| P10        | Mouse        | Accessories |

Now identify the concepts:

* The **dataset** includes related tables about sales.
* In `Orders Fact`, each **row** is one order line.
* `quantity` and `revenue` are **measures**.
* `region`, `segment`, and `category` are **attributes**.
* The **granularity** of the fact table is order-line level.
* The **unit of analysis** might be order lines, orders, customers, or days depending on the question.
* `order_id` may not be unique in the fact table if an order contains multiple products.
* `customer_id` and `product_id` are **foreign keys** in the fact table.
* The customer and product tables are **dimensions**.
* A **data dictionary** should define what `revenue` means, which currency it uses, and whether it includes tax or discounts.

This is why fundamentals matter: they tell you what you can trust, what you can aggregate, and how to interpret the outputs.

---

## Common Mistakes in Data Fundamentals

### Confusing identifiers with measures

Numeric IDs are often mistakenly summarized like real quantities.

### Ignoring granularity

Analysts aggregate or join data without first defining what one row represents.

### Using the wrong unit of analysis

A business question about customers is answered using transaction-level logic without proper aggregation.

### Assuming keys are unique

A supposed primary key may contain duplicates, causing broken joins and overcounting.

### Treating all numeric fields as additive

Percentages, balances, and averages often require careful recalculation.

### Working without documentation

Analysts infer column meanings instead of verifying them through metadata or domain knowledge.

### Mixing descriptive and transactional data carelessly

Dimension values may change over time, and facts may need historical context to remain interpretable.

---

## Practical Checklist for Analysts

When you first receive a dataset, verify the following:

1. What does the dataset contain?
2. What does one row represent?
3. What is the granularity?
4. What is the intended unit of analysis?
5. Which columns are identifiers?
6. Which columns are keys?
7. Which fields are measures?
8. Which fields are attributes?
9. Which tables are facts and which are dimensions?
10. Is there metadata or a data dictionary?
11. Are there known caveats, missing values, or definition changes?
12. Can the data support the question being asked?

This checklist prevents a large class of downstream errors.

---

## Summary

Data fundamentals are not introductory in the sense of being trivial. They are introductory in the sense of being foundational. Strong analysts revisit them constantly.

The core ideas are:

* A **dataset** is an organized collection of data.
* **Rows** store instances; **columns** store fields.
* **Records** and **observations** represent row-level entities or events.
* **Variables** describe characteristics that vary across observations.
* **Granularity** defines the level of detail in each row.
* The **unit of analysis** defines what is actually being studied.
* **Primary keys** uniquely identify rows; **foreign keys** link tables.
* **Fact tables** store measurable events; **dimension tables** store descriptive context.
* **Measures** are quantitative values for aggregation; **attributes** are descriptive fields for grouping and filtering.
* **Metadata** and **data dictionaries** explain what the data means and how it should be used.

An analyst who understands these concepts can read unfamiliar data structures faster, ask better questions earlier, and avoid costly analytical mistakes later.

---

## Key Takeaways

* Always define what one row represents before analyzing a dataset.
* Granularity and unit of analysis should be explicit, not assumed.
* Keys are central to data integrity and correct joins.
* Facts, dimensions, measures, and attributes help structure analytical thinking.
* Metadata is part of the dataset’s usability, not optional documentation.
* Many analytics errors are really data fundamentals errors in disguise.
