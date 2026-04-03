# Numerical Foundations for Analysts

Numerical fluency is a core analytical skill. Most business analysis is not blocked by advanced mathematics; it is blocked by weak handling of basic quantities. Analysts constantly compare values, normalize counts, measure change over time, combine groups, and create interpretable summaries. This chapter reviews the numerical foundations that appear repeatedly in dashboards, business cases, forecasting, experimentation, and decision support.

The goal is not to memorize formulas mechanically. The goal is to understand what each calculation means, when it is appropriate, and where it is often misused.

---

## Why numerical foundations matter

Analysts work with quantities that can easily be misinterpreted:

* Revenue can grow while profit margin shrinks.
* A region can have the highest total sales but the lowest sales per customer.
* An average can mislead when groups differ greatly in size.
* A 50% increase followed by a 50% decrease does not return to the starting point.
* Counts alone may suggest improvement when exposure also changed.

Strong numerical foundations help analysts:

* compare like with like
* normalize raw counts
* detect misleading claims
* explain business changes clearly
* avoid common spreadsheet and dashboard errors

---

## Arithmetic review

Arithmetic remains the base layer of nearly all analysis. Even sophisticated methods often rest on simple operations applied consistently.

### Addition and subtraction

Use addition and subtraction to combine quantities or measure absolute differences.

**Examples**

* Total quarterly revenue = Q1 + Q2 + Q3 + Q4
* Revenue change = Current revenue - Prior revenue
* Budget variance = Actual spend - Planned spend

**Absolute change** tells you how many units something increased or decreased by.

\\[
\text{Absolute Change} = \text{New Value} - \text{Old Value}
\\]

If sales rose from 800 to 950 units:

\\[
950 - 800 = 150
\\]

The business added **150 units**.

### Multiplication and division

Use multiplication when a quantity scales with another quantity.

* Revenue = Price × Quantity
* Total wages = Hours × Hourly rate
* Expected conversions = Traffic × Conversion rate

Use division to normalize one quantity by another.

* Revenue per customer = Revenue / Customers
* Cost per acquisition = Marketing spend / New customers
* Defect rate = Defects / Total items produced

### Order of operations

Analysts frequently work with formulas containing multiple operations. Standard order matters:

1. Parentheses
2. Exponents
3. Multiplication and division
4. Addition and subtraction

For example:

\\[
100 + 20 \times 3 = 160
\\]

not 360.

In spreadsheet work, misplaced parentheses are a common source of silent errors.

### Negative numbers

Negative values often represent:

* losses
* refunds
* debt
* downward variance
* temperature changes
* net outflows

A decline from 50 to 40 gives:

\\[
40 - 50 = -10
\\]

The negative sign indicates direction, not just size.

### Fractions and decimals

Fractions and decimals are different ways of expressing the same relationship.

* \\( \frac{1}{2} = 0.5 = 50% \\)
* \\( \frac{3}{4} = 0.75 = 75% \\)

Analysts often move between all three representations. Clarity matters: report values in the form most useful to the audience.

---

## Ratios, proportions, rates, and percentages

These terms are often used loosely in business settings, but they are not identical.

### Ratios

A **ratio** compares one quantity to another.

\\[
\text{Ratio} = \frac{A}{B}
\\]

Examples:

* Debt-to-equity ratio
* Male-to-female customer ratio
* Inventory-to-sales ratio

If a store has 200 online orders and 50 in-store orders, the online-to-store ratio is:

\\[
\frac{200}{50} = 4
\\]

This can be stated as **4:1**.

Ratios do not always imply that one quantity is part of the other. They simply compare two values.

### Proportions

A **proportion** is a part divided by the whole.

\\[
\text{Proportion} = \frac{\text{Part}}{\text{Whole}}
\\]

If 120 of 300 customers renewed:

\\[
\frac{120}{300} = 0.40
\\]

So the renewal proportion is **0.40**, or **40%**.

Proportions always range from 0 to 1 when correctly defined.

### Rates

A **rate** compares a quantity to another quantity measured in a different base, often involving time, population, or exposure.

Examples:

* 25 orders per hour
* 3 accidents per 10,000 miles
* 18 infections per 100,000 people
* 7 tickets resolved per analyst per day

Rates are especially useful when simple counts are unfair because the amount of opportunity differs.

For example, 20 defects in Factory A and 30 defects in Factory B does not necessarily mean B performs worse. If A produced 1,000 units and B produced 10,000 units, the defect rates are:

\\[
\text{A defect rate} = \frac{20}{1000} = 2%
\\]

\\[
\text{B defect rate} = \frac{30}{10000} = 0.3%
\\]

B has more defects in total, but a much lower defect rate.

### Percentages

A **percentage** is a proportion multiplied by 100.

\\[
\text{Percentage} = \text{Proportion} \times 100
\\]

If 18 out of 24 customers were satisfied:

\\[
\frac{18}{24} = 0.75 = 75%
\\]

Percentages are easy to communicate, but analysts should remember that the underlying denominator matters.

### Percentage points vs percent change

This is one of the most common mistakes in reporting.

If conversion rate rises from 4% to 6%:

* the increase is **2 percentage points**
* the relative increase is **50%**

Why?

\\[
6% - 4% = 2 \text{ percentage points}
\\]

\\[
\frac{6% - 4%}{4%} = 50%
\\]

Use **percentage points** for absolute differences between percentages. Use **percent change** for relative change.

### Common pitfalls

* Comparing percentages without checking denominators
* Reporting raw counts when exposure differs
* Confusing ratio with proportion
* Using percentages where counts are too small to be meaningful
* Mixing percent change and percentage point change

---

## Growth rates

Growth rates measure how much something changes relative to its starting value.

### Basic growth rate formula

\\[
\text{Growth Rate} = \frac{\text{New Value} - \text{Old Value}}{\text{Old Value}}
\\]

This is often expressed as a percentage.

If revenue rises from 200,000 to 250,000:

\\[
\frac{250000 - 200000}{200000} = 0.25 = 25%
\\]

Revenue grew by **25%**.

### Decline rates

If website traffic falls from 80,000 to 60,000:

\\[
\frac{60000 - 80000}{80000} = -0.25 = -25%
\\]

Traffic declined by **25%**.

### Interpreting growth correctly

Growth rates are relative. A gain of 100 customers means something different depending on the starting base.

* From 100 to 200 customers = 100% growth
* From 10,000 to 10,100 customers = 1% growth

Absolute change and growth rate should often be reported together.

### Period-over-period growth

Common comparisons include:

* day over day
* week over week
* month over month
* quarter over quarter
* year over year

Each serves a different purpose.

**Month-over-month** is useful for short-term trend monitoring.
**Year-over-year** is often better when seasonality is strong.

If December sales are compared with November sales, holiday season may distort the result. Comparing December this year with December last year often gives a fairer view.

### Average growth across periods

A common mistake is to average periodic growth rates using a simple arithmetic mean when compounding is involved. For multi-period change, geometric treatment is often more appropriate.

Suppose sales grow:

* 10% in Year 1
* 20% in Year 2

Starting from 100:

\\[
100 \times 1.10 \times 1.20 = 132
\\]

Total two-year growth is:

\\[
\frac{132 - 100}{100} = 32%
\\]

The average annual growth is not simply 15% unless you are using a rough approximation. The more correct compound annual rate is:

\\[
\left(\frac{132}{100}\right)^{1/2} - 1 \approx 14.89%
\\]

---

## Compound growth

Compound growth occurs when each period’s growth builds on the previous period’s new level.

### Core formula

If a value starts at (V_0), grows at rate (r) each period, for (n) periods:

\\[
V_n = V_0 (1+r)^n
\\]

If an investment starts at 1,000 and grows 8% annually for 3 years:

\\[
1000(1.08)^3 = 1259.71
\\]

### Why compounding matters

Compounding means growth is not linear. Each period adds growth on top of prior growth.

A 10% increase for three years is not:

\\[
100% + 10% + 10% + 10% = 130%
\\]

It is:

\\[
100 \times (1.10)^3 = 133.1
\\]

So the final value is **133.1**, not 130.

### Compound annual growth rate (CAGR)

CAGR summarizes the average annual growth rate over multiple periods, assuming smooth compounding.

\\[
\text{CAGR} = \left(\frac{\text{Ending Value}}{\text{Beginning Value}}\right)^{1/n} - 1
\\]

If customers grow from 5,000 to 8,000 over 4 years:

\\[
\left(\frac{8000}{5000}\right)^{1/4} - 1 \approx 12.47%
\\]

This means the customer base grew at an average compounded rate of about **12.47% per year**.

### Compound decline

Compounding also applies to declines.

If a subscriber base falls 5% each month for 6 months:

\\[
V_6 = V_0(0.95)^6
\\]

Repeated declines reduce the base multiplicatively, not additively.

### Rule of 72

A useful approximation for doubling time:

\\[
\text{Doubling Time} \approx \frac{72}{\text{Growth Rate in Percent}}
\\]

At 8% annual growth:

\\[
\frac{72}{8} = 9
\\]

The quantity doubles in about **9 years**.

This is approximate, but useful in quick business discussions.

### Common pitfalls

* Adding growth rates instead of compounding them
* Averaging multi-period growth arithmetically when CAGR is needed
* Ignoring the effect of changing base size
* Comparing growth across periods of different lengths without normalization

---

## Weighted averages

A weighted average is used when different values contribute unequally.

### Why simple averages fail

Suppose two stores have average order values:

* Store A: $100 from 10 orders
* Store B: $50 from 1,000 orders

A simple average of store averages gives:

\\[
\frac{100 + 50}{2} = 75
\\]

But that treats both stores as equally important, despite very different order volumes.

### Weighted average formula

\\[
\text{Weighted Average} = \frac{\sum (x_i w_i)}{\sum w_i}
\\]

where:

* (x_i) = value
* (w_i) = weight

Using the order counts as weights:

\\[
\frac{100 \times 10 + 50 \times 1000}{10 + 1000}
================================================

\frac{1000 + 50000}{1010}
\approx 50.50
\\]

The true combined average order value is about **$50.50**, not $75.

### Common uses of weighted averages

#### Average price

If 100 units sell at $5 and 300 units sell at $8:

\\[
\frac{100 \times 5 + 300 \times 8}{400} = 7.25
\\]

Average selling price is **$7.25**.

#### Portfolio return

If 60% of assets return 4% and 40% return 10%:

\\[
0.6 \times 4% + 0.4 \times 10% = 6.4%
\\]

#### Course grades

If homework is 30% and the exam is 70%, the overall score is a weighted average, not a simple mean.

### Weighted vs unweighted metrics

Analysts should be explicit about whether a metric is:

* customer-weighted
* revenue-weighted
* store-weighted
* population-weighted

These can produce very different answers.

### Simpson’s paradox warning

A pattern visible in separate groups can disappear or reverse when data is combined. One cause is unequal group weights. Weighted reasoning is essential when aggregating across segments.

### Common pitfalls

* Averaging averages without weights
* Using the wrong weight variable
* Forgetting to divide by total weight
* Treating segment summaries as if they represent equal populations

---

## Logarithms and scaling

Logarithms help analysts work with data that spans large ranges, grows multiplicatively, or changes by constant percentages rather than constant absolute amounts.

### What is a logarithm?

A logarithm answers this question:

**To what power must a base be raised to produce a number?**

If:

\\[
10^3 = 1000
\\]

then:

\\[
\log_{10}(1000) = 3
\\]

Common bases:

* base 10: common logarithm
* base (e): natural logarithm, written (\ln)

### Why analysts use logarithms

#### 1. Compressing large ranges

Suppose one company has revenue of 10,000 and another has 10,000,000. On a regular scale, the smaller company may look nearly invisible.

A log scale compresses the range so both can be shown meaningfully.

#### 2. Interpreting multiplicative growth

Equal distances on a log scale correspond to equal multiplicative changes.

For example:

* 10 to 100 is a 10× increase
* 100 to 1,000 is also a 10× increase

On a log scale, those moves are equally spaced.

#### 3. Linearizing exponential patterns

If a quantity grows exponentially, plotting the logarithm can turn a curved pattern into a straight line. This helps with interpretation and modeling.

### Log differences and approximate percentage change

For small to moderate changes:

\\[
\ln(\text{New}) - \ln(\text{Old})
\\]

approximates proportional change.

This is used frequently in economics, finance, and time-series analysis.

More precisely:

\\[
\ln\left(\frac{\text{New}}{\text{Old}}\right)
\\]

captures continuous growth.

### Example

If revenue rises from 100 to 110:

\\[
\ln(110) - \ln(100) = \ln(1.10) \approx 0.0953
\\]

This is close to a 9.53% continuously compounded increase, while ordinary percent growth is 10%.

### Doubling and halving on a log scale

A doubling represents the same multiplicative jump no matter the starting point:

* 50 to 100
* 500 to 1,000
* 5 million to 10 million

This makes logs useful in growth analysis.

### When not to use logs casually

* When the audience is unfamiliar and interpretability matters more
* When values can be zero or negative, since logarithms of non-positive numbers are undefined in standard form
* When the data generating process is additive rather than multiplicative

### Practical caution with zeros

Many business datasets contain zeros, such as zero sales days or zero claims. Since (\log(0)) is undefined, analysts sometimes use transformations like:

\\[
\log(x+1)
\\]

This can be useful, but it changes interpretation. It should never be applied mechanically without explanation.

---

## Index numbers

Index numbers express values relative to a chosen base period or base value. They are widely used to show change over time in a normalized way.

### Basic idea

An index sets a reference point, often 100, and scales other values relative to it.

\\[
\text{Index}_t = \frac{\text{Value}*t}{\text{Value}*{\text{base}}} \times 100
\\]

If the base year sales are 500 and current sales are 650:

\\[
\frac{650}{500} \times 100 = 130
\\]

The current index is **130**, meaning sales are **30% above the base period**.

### Why use index numbers

Index numbers are useful when:

* comparing different series with different units
* showing relative movement over time
* simplifying communication for executives
* benchmarking performance against a base period

### Example: comparing two products

Suppose:

* Product A sales go from 50 to 75
* Product B sales go from 1,000 to 1,200

Raw increases are:

* A: +25
* B: +200

But indexed to 100 at baseline:

* A index = \\(75/50 \times 100 = 150\\)
* B index = (\\1200/1000 \times 100 = 120\\)

A grew faster relative to its own base.

### Price indices

A common analytical use is price tracking. For example, consumer price indices track how a basket of goods changes in price over time.

If the basket cost $200 in the base year and $230 now:

\\[
\frac{230}{200} \times 100 = 115
\\]

The index is **115**, indicating a **15% price increase** since the base year.

### Re-basing an index

Sometimes the base period changes. Re-basing resets the reference point to 100 in a new period.

If an old series has:

* 2022 = 120
* 2023 = 150

and you want 2022 as the new base:

\\[
\text{New 2023 Index} = \frac{150}{120} \times 100 = 125
\\]

Now 2022 = 100 and 2023 = 125.

### Composite indices

Some index numbers combine multiple components, often using weights. For example, a market index may weight firms by market value.

Construction choices matter:

* which components are included
* how they are weighted
* what base period is chosen
* how often weights are updated

### Common pitfalls

* Forgetting that an index is relative, not absolute
* Comparing indices with different base periods without adjustment
* Ignoring weighting methodology in composite indices
* Treating an indexed difference as an absolute unit difference

---

## Bringing the concepts together

These numerical tools are often used together in one analysis.

### Example: e-commerce performance

Suppose an online business reports:

* Orders increased from 8,000 to 9,200
* Website visits increased from 200,000 to 250,000
* Revenue increased from $400,000 to $460,000

You can analyze performance from several angles:

#### Absolute change

* Orders: +1,200
* Visits: +50,000
* Revenue: +$60,000

#### Growth rates

* Orders growth: (1200/8000 = 15%)
* Visits growth: (50000/200000 = 25%)
* Revenue growth: (60000/400000 = 15%)

#### Conversion rate

Old conversion rate:

\\[
\frac{8000}{200000} = 4%
\\]

New conversion rate:

\\[
\frac{9200}{250000} = 3.68%
\\]

Orders grew, but conversion rate fell.

#### Revenue per visit

Old:

\\[
\frac{400000}{200000} = 2.00
\\]

New:

\\[
\frac{460000}{250000} = 1.84
\\]

Revenue per visit also declined.

A superficial reading says performance improved because revenue increased. A stronger numerical reading shows traffic rose faster than monetization efficiency.

---

## Choosing the right numerical summary

A recurring analytical question is not merely *how to calculate*, but *what should be calculated*.

### Use raw counts when

* scale itself matters
* resource planning depends on totals
* the audience needs absolute magnitude

Examples:

* total units sold
* total claims filed
* total support tickets

### Use ratios, proportions, or rates when

* groups differ in size
* exposure differs
* fairness requires normalization

Examples:

* conversion rate
* defects per 1,000 units
* sales per employee

### Use growth rates when

* change relative to baseline matters
* comparing entities with different starting sizes
* trend evaluation is central

### Use weighted averages when

* subgroup sizes differ
* combining summaries across segments
* averages must reflect true contribution

### Use logarithms when

* data spans many orders of magnitude
* growth is multiplicative
* relative changes matter more than absolute differences

### Use index numbers when

* showing relative movement from a base period
* comparing multiple series on a common scale
* communicating trend without distracting unit differences

---

## Common analyst errors

### Confusing absolute and relative change

Going from 2 to 4 is not the same as going from 200 to 202, even though both increase by 2.

### Comparing unnormalized counts

A larger region, store, or population often has larger totals. That alone says little about performance.

### Averaging percentages improperly

An average of group percentages is often wrong unless weighted by the relevant denominator.

### Ignoring denominator changes

A drop in incidents may simply reflect reduced volume, not better performance.

### Misreporting percentage points

Moving from 30% to 40% is a 10 percentage point increase, not a 10% increase.

### Treating growth as additive

Repeated percentage changes compound.

### Presenting logs or indices without explanation

These tools are useful but can be opaque. The analyst must explain what the transformed scale means.

---

## Practical checklist for analysts

Before presenting a number, ask:

1. What exactly is the numerator?
2. What exactly is the denominator?
3. Am I showing an absolute change or a relative change?
4. Should this be weighted?
5. Is the comparison fair across groups or time periods?
6. Would an indexed or log-scaled view reveal the pattern more clearly?
7. Will the audience understand the unit and interpretation?

If any of these are unclear, the calculation is not ready for decision-making.

---

## Summary

Numerical foundations are not minor technical details. They shape how analysts frame evidence and how stakeholders interpret reality.

A capable analyst should be comfortable with:

* arithmetic for combining and comparing values
* ratios, proportions, rates, and percentages for normalization
* growth rates for relative change
* compound growth for multi-period change
* weighted averages for correct aggregation
* logarithms for multiplicative patterns and large ranges
* index numbers for base-relative comparison

These tools recur across nearly every domain of analytics. Mastering them makes later topics such as statistics, forecasting, experimentation, and performance analysis much easier and much more reliable.

---

## Key terms

**Absolute change**
The arithmetic difference between a new value and an old value.

**Ratio**
A comparison of one quantity to another.

**Proportion**
A part divided by a whole.

**Rate**
A quantity measured relative to another base, often time, population, or exposure.

**Percentage**
A proportion expressed out of 100.

**Growth rate**
Relative change from an initial value to a later value.

**Compound growth**
Growth where each period builds on the prior period’s updated level.

**Weighted average**
An average that accounts for unequal importance or frequency.

**Logarithm**
A transformation expressing the exponent needed to produce a value from a chosen base.

**Index number**
A relative measure scaled to a base period, often set to 100.

---

## Review questions

1. What is the difference between a ratio and a proportion?
2. Why is percentage point change different from percent change?
3. When should a rate be used instead of a raw count?
4. Why can a simple average of averages be misleading?
5. What does CAGR measure that a simple average growth rate does not?
6. Why are logarithms useful for data that spans a very large range?
7. What does an index value of 140 mean if the base period is 100?

---

## Practice prompts

* Compute the absolute change and percent change in monthly active users from 24,000 to 30,000.
* Compare two stores using revenue per customer rather than total revenue.
* Calculate a weighted average price from multiple product tiers.
* Convert a sales series into an index with the first month as base 100.
* Explain to a stakeholder why a rise from 12% to 15% should be described as a 3 percentage point increase.
