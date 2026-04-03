# Databases and Data Storage Basics

Data storage is the foundation of analytics. Analysts rarely work with raw numbers in isolation; they work with data stored in files, systems, and platforms designed for collection, retrieval, transformation, and analysis. Understanding the basic storage landscape helps analysts choose the right source, ask better questions about data quality, and work more effectively with engineers, administrators, and stakeholders.

This chapter introduces the main storage patterns analysts encounter: flat files, spreadsheets, operational databases, data warehouses, data lakes, and cloud data platforms. It also explains core relational concepts such as tables, schemas, indexes, and joins, along with the distinction between OLTP and OLAP systems.

---

## Why storage basics matter for analysts

An analyst does not need to be a database administrator, but they do need to understand where data lives and how the storage system affects:

* query speed
* reliability
* data quality
* update frequency
* historical availability
* modeling choices
* reporting limitations

For example, the same business metric may look different depending on whether it comes from:

* a manually maintained spreadsheet
* a live transactional database
* a cleaned warehouse table
* a raw event lake

A strong analyst knows that storage format is not a technical detail only. It shapes the meaning and usability of the data.

---

## Flat files, spreadsheets, databases, warehouses, and lakes

These storage types often coexist in the same organization.

## Flat files

A **flat file** stores data in a simple tabular or structured text format, usually without enforced relationships between files.

Common examples include:

* CSV
* TSV
* JSON
* XML
* log files
* plain text exports

### Characteristics

* easy to create and share
* often portable across systems
* usually lack built-in constraints and governance
* can become inconsistent when versions multiply
* suitable for small to medium-scale exchange and temporary analysis

### Example

A sales export in `sales_2026_03.csv` might contain:

| order_id | order_date | customer_id | product_id | revenue |
| -------- | ---------- | ----------- | ---------- | ------- |
| 1001     | 2026-03-01 | C301        | P88        | 49.99   |

### Strengths

* simple
* universal
* easy to inspect
* useful for extracts and one-off analysis

### Limitations

* no enforced primary keys or relationships
* easy to corrupt with manual edits
* weak concurrency support
* difficult to manage at scale
* version control is often poor

Flat files are common at the edges of analytics workflows: imports, exports, vendor data, archived snapshots, and ad hoc analysis.

---

## Spreadsheets

A **spreadsheet** is a grid-based application for storing, editing, calculating, and visualizing data.

Common tools include:

* Microsoft Excel
* Google Sheets
* LibreOffice Calc

### Characteristics

* interactive and easy for non-technical users
* useful for quick exploration and business collaboration
* often combines data storage, formulas, formatting, and commentary in one place

### Strengths

* accessible
* flexible
* excellent for lightweight modeling and stakeholder review
* useful for prototyping metrics or validating logic

### Limitations

* error-prone when used as a system of record
* hard to audit at scale
* weak support for large volumes
* formulas can be hidden or inconsistent
* collaboration can create conflicting logic

Spreadsheets are valuable tools, but they become risky when they function as unofficial production databases.

### Practical rule

Use spreadsheets for:

* light analysis
* manual review
* planning
* quick calculations
* stakeholder-friendly models

Do not rely on them as the long-term source of truth for large or critical datasets.

---

## Databases

A **database** is an organized system for storing and retrieving data, usually managed by a database management system (DBMS).

Examples:

* PostgreSQL
* MySQL
* SQL Server
* Oracle
* SQLite

A database provides structure, querying capabilities, constraints, security, and multi-user access.

### Why databases matter

Compared with flat files and spreadsheets, databases provide:

* better consistency
* controlled access
* concurrency management
* efficient querying
* data integrity rules
* support for relationships between tables

Databases are the standard backbone for applications and many analytical workflows.

---

## Data warehouses

A **data warehouse** is a centralized system designed primarily for analytics and reporting rather than day-to-day transaction processing.

Examples:

* Snowflake
* Google BigQuery
* Amazon Redshift
* Azure Synapse Analytics

### Characteristics

* integrates data from multiple source systems
* stores historical data
* optimized for large analytical queries
* often structured around business entities and metrics
* supports reporting, dashboards, and modeling

### Typical warehouse use cases

* monthly revenue trends
* customer retention analysis
* finance reporting
* executive dashboards
* cross-functional KPI tracking

### Key idea

Operational systems answer questions like:

> “What is the status of this order right now?”

Warehouses answer questions like:

> “How have orders, revenue, returns, and customer behavior changed over the past 24 months?”

---

## Data lakes

A **data lake** is a large-scale storage system that holds raw or semi-processed data in its native format.

Examples of stored content:

* CSV files
* JSON events
* application logs
* clickstream data
* images
* audio
* parquet files
* machine-generated telemetry

### Characteristics

* flexible ingestion
* can store structured, semi-structured, and unstructured data
* often cheaper storage than traditional warehouse patterns
* useful for raw history and large-scale processing

### Benefits

* preserves detailed raw data
* supports future use cases not anticipated upfront
* works well for data science, machine learning, and event pipelines
* enables schema-on-read approaches

### Risks

Without governance, a lake can become a **data swamp**:

* unclear ownership
* inconsistent naming
* poor documentation
* duplicate files
* uncertain quality
* difficult discovery

A lake is powerful, but it needs metadata, conventions, and controls to remain useful.

---

## How these fit together

A simplified analytics landscape might look like this:

1. operational systems generate data
2. exports, events, and logs land in storage
3. raw data is stored in a lake or staging area
4. cleaned and modeled data is loaded into a warehouse
5. analysts query warehouse tables for reporting and analysis
6. selected outputs are pushed into dashboards, spreadsheets, or presentations

This layered design separates **data capture** from **analytical consumption**.

---

# Relational databases

A **relational database** stores data in tables made of rows and columns, with relationships between tables defined through keys.

Relational systems are based on the relational model, which emphasizes structured data, consistency, and logical relationships.

## Why relational systems are central to analytics

Most business data is naturally relational. For example:

* customers place orders
* orders contain products
* employees belong to departments
* subscriptions generate invoices
* website sessions contain events

These are not independent facts. They are connected entities.

Relational databases let us represent those connections cleanly and query them with SQL.

---

## Tables

A **table** is a collection of records about one entity or event type.

Examples:

* `customers`
* `orders`
* `products`
* `payments`

Each table has:

* **rows**: individual records
* **columns**: fields or attributes

### Example

`customers`

| customer_id | customer_name | signup_date | country |
| ----------- | ------------- | ----------- | ------- |
| C301        | Asha Rai      | 2025-11-04  | Nepal   |
| C302        | R. Gupta      | 2025-12-20  | India   |

`orders`

| order_id | customer_id | order_date | amount |
| -------- | ----------- | ---------- | ------ |
| O1001    | C301        | 2026-03-01 | 49.99  |
| O1002    | C301        | 2026-03-14 | 19.99  |

The `customer_id` column connects orders to customers.

---

## Schemas

A **schema** is the structural definition or organizational grouping of database objects.

The term is used in two closely related ways:

### 1. Schema as structure

It describes:

* table names
* columns
* data types
* constraints
* relationships

Example:

* `order_id` is integer
* `order_date` is date
* `amount` is numeric

### 2. Schema as namespace

In many database systems, a schema is also a logical container inside a database.

Example:

* `raw.orders`
* `analytics.orders`
* `finance.invoices`

This helps organize objects by purpose, team, or data maturity.

### Why analysts care

Schemas help signal intent:

* `raw` may contain uncleaned source data
* `staging` may contain transformed intermediate tables
* `analytics` may contain business-ready tables
* `sandbox` may contain temporary analyst work

Understanding schema organization reduces confusion and prevents analysts from building reports on the wrong tables.

---

## Indexes

An **index** is a data structure that improves the speed of data retrieval for certain queries.

It works somewhat like an index in a book: instead of scanning every page, the system can jump more directly to the relevant entries.

### Example

If a database frequently searches for orders by `customer_id`, an index on `customer_id` can make those lookups much faster.

### Benefits

* faster filtering
* faster joins
* faster sorting in some cases

### Trade-offs

* indexes use storage
* indexes can slow inserts and updates
* not every query benefits equally
* too many indexes can hurt performance

### Analyst perspective

Analysts do not always create indexes, but they should know why a query may be slow:

* no index on filter column
* join keys not indexed in transactional systems
* full-table scan required
* query hitting a huge raw table

In analytical warehouses, indexing may work differently or be abstracted away, but the principle remains: physical design affects query performance.

---

## Joins

A **join** combines rows from two or more tables based on a related column.

Joins are essential because business data is often normalized across multiple tables.

### Example

You may need customer names from `customers` and order amounts from `orders`. A join connects them through `customer_id`.

### Common join types

#### Inner join

Returns only rows with matches in both tables.

Use when you want records that exist in both places.

#### Left join

Returns all rows from the left table and matching rows from the right table.

Use when you want to preserve all records from the primary table even if related data is missing.

#### Right join

Returns all rows from the right table and matching rows from the left table.

Less commonly used in practice because the same logic can often be written as a left join with reversed table order.

#### Full outer join

Returns all matched and unmatched rows from both tables.

Useful for reconciliation tasks.

### Join risks analysts should watch for

#### Duplicates from one-to-many relationships

If one customer has many orders, joining customers to orders multiplies the customer row.

#### Many-to-many joins

These can create explosive row growth and incorrect aggregations if not modeled carefully.

#### Missing keys

If keys are null, inconsistent, or differently formatted, joins may silently drop or fail to match records.

#### Wrong grain

Joining a daily summary table to row-level events can distort results if the level of detail is mismatched.

### Rule of thumb

Before joining, ask:

* What is the grain of each table?
* Which key connects them?
* Is the relationship one-to-one, one-to-many, or many-to-many?
* What rows will be excluded or duplicated?

---

# OLTP vs OLAP

One of the most important distinctions in analytics infrastructure is the difference between **OLTP** and **OLAP**.

## OLTP: Online Transaction Processing

OLTP systems are designed to support operational business processes in real time.

Examples:

* placing orders
* processing payments
* updating account balances
* booking appointments
* managing inventory transactions

### Characteristics

* many small, fast read/write transactions
* high concurrency
* strict consistency requirements
* optimized for inserting and updating current records
* typically highly normalized

### Example questions answered by OLTP systems

* Did this payment succeed?
* What is the current shipping address for this customer?
* Is this item in stock right now?

Operational databases power applications.

---

## OLAP: Online Analytical Processing

OLAP systems are designed for analysis over large amounts of data.

Examples:

* trend analysis
* dashboards
* cohort retention
* regional sales comparisons
* profitability analysis

### Characteristics

* fewer but much heavier queries
* scans across large datasets
* aggregations across many rows
* historical analysis
* often denormalized or modeled for reporting efficiency

### Example questions answered by OLAP systems

* What were quarterly sales by channel over the last three years?
* Which customer segments have the highest lifetime value?
* How did conversion rates change after the pricing update?

Analytical systems power insight generation.

---

## OLTP vs OLAP comparison

| Aspect             | OLTP                           | OLAP                                |
| ------------------ | ------------------------------ | ----------------------------------- |
| Primary purpose    | Run business operations        | Analyze business performance        |
| Query style        | Short, transactional           | Long, aggregate-heavy               |
| Data freshness     | Current operational state      | Historical and integrated           |
| Users              | Applications, operations staff | Analysts, BI tools, executives      |
| Write activity     | Frequent inserts/updates       | Less frequent bulk loads/transforms |
| Data model         | Normalized                     | Often denormalized or dimensional   |
| Performance target | Fast individual transactions   | Fast large-scale analysis           |

### Why analysts must know this distinction

Analysts sometimes query production OLTP systems directly, especially in smaller organizations. This can be risky because:

* analytical queries may slow the application
* the schema may be optimized for transactions, not insight
* historical data may be limited
* business definitions may not be standardized

In mature environments, analytics should usually run on OLAP-oriented systems such as warehouses or marts.

---

# Data marts

A **data mart** is a focused subset of analytical data designed for a specific business area, team, or use case.

Examples:

* finance mart
* marketing mart
* sales mart
* customer support mart

## Purpose

A mart simplifies access to relevant data by organizing it around a particular function rather than exposing the full complexity of enterprise-wide data.

### Benefits

* easier for business users to understand
* faster access to common metrics
* reduced complexity
* better governance for a domain
* can improve performance for repeated reporting use cases

### Example

A finance mart may include:

* revenue by month
* invoice facts
* expense categories
* budget dimensions
* customer billing history

A marketing analyst may not need raw warehouse tables if a well-designed marketing mart already provides campaign, channel, attribution, and lead metrics.

## Trade-off

Data marts are useful when they align with consistent business logic. They become a problem when many disconnected marts create conflicting definitions.

For example:

* one mart defines “active customer” as a purchase in 90 days
* another uses 180 days

A good data architecture balances local usability with shared enterprise definitions.

---

# Cloud data platforms

Modern analytics increasingly runs on **cloud data platforms**, which provide scalable storage, computation, and managed services over the internet.

These platforms reduce the need for organizations to manage physical infrastructure directly.

## What cloud platforms usually provide

* managed storage
* elastic compute
* SQL query engines
* pipeline and orchestration tools
* security and access controls
* backup and recovery options
* integration with BI and machine learning tools

## Common platform patterns

### Cloud data warehouses

Managed systems optimized for analytics.

Examples include platforms built for:

* massive SQL workloads
* scalable storage and compute
* separation of compute from storage in some architectures
* concurrent access by many users and tools

### Cloud object storage

Low-cost storage for files and raw data.

Typical uses:

* landing raw source data
* archiving snapshots
* storing logs and events
* supporting lake architectures

### Lakehouse-style platforms

These combine some characteristics of data lakes and warehouses:

* file-based scalable storage
* table-like semantics
* analytical SQL access
* support for structured and semi-structured data
* improved governance over lake data

## Why analysts should care

Even when analysts do not manage infrastructure, cloud platforms affect daily work:

* query cost may depend on data scanned
* performance may depend on table partitioning or clustering
* permissions may vary by environment
* compute resources may need to be selected or scheduled
* data may be separated across dev, test, and prod environments

### Practical implication

In cloud systems, writing an inefficient query is not just slow. It may also be expensive.

---

# Basic storage architecture for analysts

Analysts benefit from understanding the typical flow of data through an organization.

## A simple analytical storage architecture

### 1. Source systems

These are where data originates.

Examples:

* CRM
* ERP
* e-commerce application
* payment platform
* product event tracking
* support ticketing tool

These systems are optimized for operational needs, not necessarily analysis.

### 2. Ingestion layer

Data is extracted from source systems and moved into central storage.

Common methods:

* batch loads
* API pulls
* change data capture
* event streaming
* file drops

### 3. Raw storage or staging

Data is landed with minimal transformation.

Characteristics:

* close to source format
* useful for traceability and reprocessing
* may contain duplicates, nulls, or source-specific quirks

### 4. Transformation layer

Data is cleaned, standardized, joined, and modeled.

Typical tasks:

* type correction
* deduplication
* key normalization
* metric definition
* dimensional modeling
* business rule application

### 5. Curated analytical layer

This is where analysts ideally work most of the time.

Characteristics:

* documented tables
* trusted definitions
* stable joins
* business-friendly naming
* ready for dashboards and ad hoc analysis

### 6. Consumption layer

Outputs are delivered through:

* dashboards
* notebooks
* reports
* extracts
* reverse ETL workflows
* data applications

---

## A common layered model

Many teams use a layered structure such as:

| Layer           | Purpose                                  |
| --------------- | ---------------------------------------- |
| Raw             | Ingested source data with minimal change |
| Staging         | Basic cleanup and standardization        |
| Intermediate    | Reusable transformation logic            |
| Mart / Semantic | Business-ready analytical tables         |
| Presentation    | Dashboards, reports, APIs                |

This layered approach improves:

* transparency
* reproducibility
* trust
* maintainability

---

## What analysts should know about storage architecture

An analyst should be able to answer these questions:

### Where did this data come from?

Know the original source system or upstream table.

### What transformation steps occurred?

Understand whether the data is raw, cleaned, enriched, or aggregated.

### What is the grain?

Know whether the table is at the level of:

* event
* order
* order item
* day
* customer-month
* account-quarter

### Is this source trusted for production reporting?

Some tables are exploratory only; others are certified.

### How fresh is it?

A dashboard based on hourly refresh differs from one based on end-of-month snapshots.

### Who owns it?

Ownership matters when definitions break or anomalies appear.

---

# Analytical implications of storage choices

Storage design affects analysis quality.

## Granularity and aggregation

Raw event data supports flexibility, but summarized tables are faster and simpler. Analysts must know which one they are using.

## History retention

Operational tables may overwrite values. Warehouses often preserve historical snapshots or slowly changing dimensions.

## Data quality controls

Databases and curated warehouse tables usually have more validation than ad hoc files.

## Performance

Joins, filters, aggregations, and time windows behave differently depending on storage engine and physical design.

## Access and governance

Some data may be restricted by role, region, or compliance requirements.

---

# Common pitfalls for analysts

## Treating spreadsheets as authoritative databases

Convenient does not mean reliable.

## Querying OLTP systems for heavy reporting

This can hurt operational performance and still produce poor analytical structures.

## Ignoring grain before joining

Many bad metrics come from valid SQL over mismatched levels of detail.

## Confusing raw tables with curated tables

Raw does not mean ready.

## Assuming all tables with similar names mean the same thing

Different schemas and layers often represent different stages of transformation.

## Overlooking cost in cloud environments

A query that scans huge raw tables repeatedly may be financially wasteful.

---

# Practical mental model

A useful way to think about storage systems is this:

* **flat files** move or archive data
* **spreadsheets** help humans inspect and manipulate small datasets
* **databases** run applications and store structured records
* **warehouses** support analytics across integrated historical data
* **lakes** store raw and varied data at scale
* **marts** organize analytical data for specific business domains
* **cloud platforms** provide scalable infrastructure for all of the above

An analyst does not need to build every layer, but they should understand how each layer shapes the data they use.

---

# Summary

Databases and storage systems are not interchangeable containers. Each exists for a reason.

* **Flat files** are simple and portable but weakly governed.
* **Spreadsheets** are flexible and accessible but risky as systems of record.
* **Databases** provide structure, integrity, and operational access.
* **Relational databases** organize data into related tables queried through SQL.
* **Tables, schemas, indexes, and joins** are core concepts for working with structured data efficiently and correctly.
* **OLTP systems** support day-to-day transactions.
* **OLAP systems** support large-scale analysis.
* **Data marts** provide domain-focused analytical views.
* **Cloud data platforms** make large-scale storage and analytics more scalable and managed.
* **Basic storage architecture** helps analysts trace data from source to insight.

The better an analyst understands storage, the better they can diagnose issues, choose the right data source, write efficient queries, and produce trustworthy analysis.

---

## Key terms

**Flat file**
A simple file-based data format, often tabular, with little or no enforced relational structure.

**Spreadsheet**
A grid-based application for storing, calculating, and reviewing data interactively.

**Database**
An organized system for storing and retrieving data through a database management system.

**Relational database**
A database that stores structured data in related tables.

**Table**
A collection of rows and columns representing one entity or event type.

**Schema**
The structural definition of database objects or a logical namespace containing them.

**Index**
A structure that improves lookup and query performance on selected columns.

**Join**
An operation that combines related rows from multiple tables.

**OLTP**
Online Transaction Processing; systems optimized for operational transactions.

**OLAP**
Online Analytical Processing; systems optimized for large analytical queries.

**Data warehouse**
A centralized analytical database for integrated, historical, query-ready data.

**Data lake**
A storage system for raw, large-scale, multi-format data.

**Data mart**
A subject-area-focused subset of analytical data.

**Cloud data platform**
A managed cloud-based environment for storing, processing, and analyzing data.

---

## Review questions

1. What are the main differences between a flat file, a spreadsheet, a database, and a data warehouse?
2. Why are relational databases especially useful for analytics?
3. What role do schemas, indexes, and joins play in database work?
4. How do OLTP and OLAP systems differ in purpose and design?
5. What problem does a data mart solve?
6. Why is understanding storage architecture important for analysts?
7. What risks arise when analysts ignore data grain or source maturity?
