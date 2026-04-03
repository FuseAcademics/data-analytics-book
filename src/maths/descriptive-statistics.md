# Descriptive Statistics

Descriptive statistics summarize data so an analyst can quickly understand its center, spread, shape, and unusual features. They do not explain *why* patterns exist or whether one variable causes another. Their role is to describe what the data looks like and provide a compact foundation for deeper analysis.

Good descriptive statistics help answer questions such as:

* What is typical in this dataset?
* How much do values vary?
* Is the distribution symmetric or skewed?
* Are there outliers?
* How should the data be summarized for decision-makers?

In practice, descriptive statistics are usually the first formal step after cleaning and validating data.

---

## Why Descriptive Statistics Matter

Raw data is often too large or too detailed to inspect directly. A table with thousands of rows may hide simple truths:

* Most values may cluster around a narrow range.
* A few extreme values may distort averages.
* The data may be highly skewed.
* Different groups may have very different distributions.

Descriptive statistics reduce complexity while preserving the main signals needed for interpretation.

They are essential for:

* exploratory data analysis
* quality checks
* comparing groups
* validating assumptions before modeling
* communicating findings clearly

---

## Measures of Central Tendency

Measures of central tendency describe the “center” or typical value of a dataset.

### Mean

The **mean** is the arithmetic average.

\\[
\text{Mean} = \frac{\sum x_i}{n}
\\]

Where:

* \\(x_i\\) = each observed value
* \\(n\\) = number of observations

#### Example

For values: 10, 12, 13, 15, 50

\\[
\text{Mean} = \frac{10+12+13+15+50}{5} = 20
\\]

#### Interpretation

The mean uses all observations, so it is informative when data is relatively symmetric and free from extreme outliers.

#### Strengths

* simple and widely understood
* uses every value
* useful in further analysis and modeling

#### Limitations

* highly sensitive to outliers
* may be misleading for skewed data

In the example above, the mean is 20, but most values are much lower. The value 50 pulls the average upward.

---

### Median

The **median** is the middle value when data is sorted.

* If the number of observations is odd, the median is the middle value.
* If even, it is the average of the two middle values.

#### Example

Sorted values: 10, 12, 13, 15, 50

Median = 13

#### Interpretation

The median represents the midpoint of the data: half the observations are below it and half are above it.

#### Strengths

* resistant to outliers
* more representative than the mean for skewed data
* useful for income, prices, response times, and similar variables

#### Limitations

* ignores the exact magnitude of most observations
* less mathematically convenient than the mean for some analyses

---

### Mode

The **mode** is the most frequently occurring value.

#### Example

Values: 2, 3, 3, 4, 4, 4, 5

Mode = 4

A dataset may be:

* **unimodal**: one mode
* **bimodal**: two modes
* **multimodal**: more than two modes
* **without a mode**: no repeated value

#### Interpretation

The mode is especially useful for:

* categorical variables
* common choices or preferences
* identifying peaks in discrete data

#### Example Use Cases

* most common product category
* most frequent survey answer
* most common defect type

#### Limitations

* may not be unique
* can be unstable in small datasets
* less useful for continuous numerical data unless values are grouped into bins

---

## Comparing Mean, Median, and Mode

| Measure | Best Use                      | Sensitive to Outliers | Works for Categorical Data |
| ------- | ----------------------------- | --------------------: | -------------------------: |
| Mean    | symmetric numerical data      |                   Yes |                         No |
| Median  | skewed numerical data         |                    No |                         No |
| Mode    | most common value or category |                    No |                        Yes |

### Practical Rule

* Use the **mean** when the distribution is roughly symmetric.
* Use the **median** when the distribution is skewed or contains outliers.
* Use the **mode** for categories or when frequency itself matters.

---

## Measures of Spread

Measures of spread describe how dispersed the data is. Two datasets can have the same center but very different variability.

### Range

The **range** is the difference between the maximum and minimum values.

\\[
\text{Range} = \text{Max} - \text{Min}
\\]

#### Example

Values: 10, 12, 13, 15, 50

Range = 50 - 10 = 40

#### Interpretation

The range gives a quick sense of total spread.

#### Limitation

It depends only on two values and is therefore highly sensitive to outliers.

---

### Variance

The **variance** measures the average squared distance from the mean.

For a population:

\\[
\sigma^2 = \frac{\sum (x_i - \mu)^2}{N}
\\]

For a sample:

\\[
s^2 = \frac{\sum (x_i - \bar{x})^2}{n-1}
\\]

#### Interpretation

A larger variance means observations are more spread out from the mean.

#### Why Squared Distances?

Squaring ensures:

* all deviations become positive
* larger deviations are weighted more heavily
* the measure supports many mathematical procedures

#### Limitation

Variance is expressed in squared units, which can be hard to interpret directly.

For example, if a variable is in dollars, variance is in dollars squared.

---

### Standard Deviation

The **standard deviation** is the square root of the variance.

\\[
\sigma = \sqrt{\sigma^2}, \quad s = \sqrt{s^2}
\\]

#### Interpretation

Standard deviation measures typical distance from the mean in the original units of the data.

#### Example

If average daily sales are 500 units with a standard deviation of 50, then daily sales typically vary by about 50 units around the mean.

#### Why It Matters

Standard deviation is often more interpretable than variance because it uses the same units as the underlying variable.

#### Caution

Like the mean, standard deviation is sensitive to outliers. If the data is heavily skewed, it may overstate typical spread.

---

## Quartiles, Percentiles, and Interquartile Range

These measures describe the position of values within the sorted data.

### Quartiles

Quartiles divide data into four equal parts.

* **Q1**: 25th percentile
* **Q2**: 50th percentile, which is the median
* **Q3**: 75th percentile

#### Interpretation

* 25% of values are below Q1
* 50% are below Q2
* 75% are below Q3

Quartiles are useful for understanding how data is distributed beyond just the center.

---

### Percentiles

A **percentile** indicates the value below which a given percentage of observations fall.

#### Examples

* 90th percentile: 90% of observations are below this value
* 95th percentile response time: 95% of requests are faster than this threshold

#### Common Business Uses

* customer income distribution
* exam scores
* delivery times
* system latency metrics
* compensation benchmarking

Percentiles are often more informative than averages when users care about tails rather than typical cases.

---

### Interquartile Range (IQR)

The **interquartile range** is the distance between Q3 and Q1.

\\[
IQR = Q3 - Q1
\\]

#### Interpretation

The IQR captures the spread of the middle 50% of the data.

#### Why It Matters

Because it ignores the most extreme 25% on each side, the IQR is more robust to outliers than the full range or standard deviation.

#### Outlier Detection Rule

A common rule defines outliers as values:

* below \\(Q1 - 1.5 \times IQR \\)
* above \\(Q3 + 1.5 \times IQR \\)

This rule is commonly used in box plots.

---

## Distribution Shape

Descriptive statistics should not only summarize center and spread. They should also describe the **shape** of the distribution.

Shape affects interpretation, choice of summary metrics, and downstream analysis.

### Symmetric Distribution

A symmetric distribution has roughly equal shape on both sides of the center.

Characteristics:

* mean and median are often similar
* outliers are less likely to distort the picture dramatically
* standard deviation is often a reasonable summary of spread

The normal distribution is the classic example.

---

### Skewed Distribution

A distribution is **skewed** when one tail is longer than the other.

#### Right-Skewed (Positive Skew)

* long tail on the right
* a few large values pull the mean upward
* mean > median is common

Examples:

* income
* transaction value
* website session duration
* delivery delays

#### Left-Skewed (Negative Skew)

* long tail on the left
* a few very small values pull the mean downward
* mean < median is common

Examples:

* very easy test scores
* satisfaction ratings clustered at the high end

#### Why Skew Matters

When data is skewed:

* the mean may not represent a typical observation
* the median may be a better measure of center
* percentiles may be more informative than standard deviation

---

### Modality

A distribution’s **modality** refers to the number of peaks.

* **unimodal**: one peak
* **bimodal**: two peaks
* **multimodal**: multiple peaks

#### Interpretation

Multiple peaks often suggest that the data contains different subgroups.

Example:

If employee salaries show two peaks, the organization may have two main job bands or role families.

This is a warning that one overall average may hide important structure.

---

## Skewness and Kurtosis

These are formal numerical summaries of distribution shape.

### Skewness

**Skewness** measures asymmetry.

* positive skewness indicates a longer right tail
* negative skewness indicates a longer left tail
* skewness near zero suggests approximate symmetry

#### Interpretation

Skewness helps quantify what is often seen visually in a histogram or density plot.

#### Caution

Skewness can be unstable in small samples and sensitive to outliers. It should be interpreted together with plots and robust summaries.

---

### Kurtosis

**Kurtosis** describes tail heaviness and the tendency to produce extreme values.

A distribution with high kurtosis tends to have:

* heavier tails
* more extreme observations
* a sharper central peak in some cases

A distribution with low kurtosis tends to have:

* lighter tails
* fewer extreme values

#### Practical Interpretation

Kurtosis is often used to assess whether a dataset produces more unusually large or small observations than expected under a normal distribution.

#### Caution

Kurtosis is often misunderstood. In applied analytics, it is usually more useful as a signal of tail behavior than as a standalone business metric.

---

## Robust Statistics

**Robust statistics** are measures that remain informative even when data contains outliers, skewness, or non-normal behavior.

These are often preferred in messy real-world data.

### Common Robust Measures

#### Median

A robust measure of center.

#### Interquartile Range

A robust measure of spread.

#### Median Absolute Deviation (MAD)

MAD summarizes variability using deviations from the median rather than the mean.

[
MAD = \text{median}(|x_i - \text{median}(x)|)
]

This is useful when outliers make standard deviation misleading.

#### Trimmed Mean

A **trimmed mean** removes a small percentage of the lowest and highest values before calculating the mean.

Example:

* a 10% trimmed mean removes the lowest 10% and highest 10% of observations

This gives a compromise between:

* the mean, which uses many values
* the median, which is highly resistant but uses less detail

---

### Why Robust Statistics Matter

Real-world data is often messy because of:

* data entry errors
* unusual transactions
* fraud
* operational incidents
* natural business heterogeneity

In such cases, robust statistics provide summaries that better reflect typical behavior.

#### Example

Consider delivery times:

* Most deliveries take 2 to 4 days
* A few take 20 days due to weather or system failures

The mean may overstate typical delivery time, while the median and IQR provide a more realistic summary.

---

## Summary Tables

A summary table condenses descriptive statistics into a structured format.

### Common Elements in a Summary Table

For a numerical variable, analysts often include:

* count
* mean
* median
* standard deviation
* minimum
* Q1
* Q3
* maximum
* IQR
* selected percentiles such as p10, p90, p95

For a categorical variable, analysts often include:

* count
* number of unique categories
* most frequent category
* frequency of the mode
* percentages by category

---

### Example Numerical Summary Table

| Statistic          | Value |
| ------------------ | ----: |
| Count              | 1,000 |
| Mean               |  52.4 |
| Median             |  49.8 |
| Standard Deviation |  12.1 |
| Minimum            |  18.0 |
| Q1                 |  44.2 |
| Q3                 |  58.9 |
| Maximum            | 121.0 |
| IQR                |  14.7 |
| 90th Percentile    |  68.3 |

### Interpretation

This table suggests:

* the typical value is around 50
* the mean is slightly higher than the median, indicating possible right skew
* the maximum is far above Q3, suggesting possible outliers
* the middle 50% of observations span 14.7 units

---

### Example Categorical Summary Table

| Category | Count | Percent |
| -------- | ----: | ------: |
| Email    |   420 |   42.0% |
| Search   |   310 |   31.0% |
| Direct   |   180 |   18.0% |
| Referral |    90 |    9.0% |

### Interpretation

This shows the dominant categories and their relative contribution. Here, Email is the largest source, but Search is also substantial.

---

## How to Interpret Descriptive Statistics Together

No single statistic is enough. Good interpretation requires combining multiple measures.

### Example 1: Mean Much Higher Than Median

This usually suggests:

* right-skewed data
* a small number of large values

Possible conclusion: use the median as the primary summary of a typical case.

---

### Example 2: Large Standard Deviation

This may indicate:

* genuine variability
* multiple subgroups
* measurement inconsistencies
* outliers

Possible next step: inspect the distribution visually and segment by relevant categories.

---

### Example 3: Small IQR but Large Range

This often means:

* most observations are tightly clustered
* a few extreme values stretch the total spread

Possible conclusion: the dataset is mostly stable, but outliers deserve investigation.

---

### Example 4: Bimodal Distribution

This suggests:

* two populations may be combined
* averages may hide important differences

Possible next step: split the analysis by segment, product line, geography, or customer type.

---

## Descriptive Statistics and Visualization

Descriptive statistics are strongest when paired with visuals.

Useful companion charts include:

* **histogram** for shape and skew
* **box plot** for median, IQR, and outliers
* **bar chart** for categorical frequencies
* **density plot** for smooth distribution comparison
* **violin plot** for shape and spread across groups

A table may show a median of 20 and a mean of 35, but a histogram can reveal whether this comes from mild skew, a few large outliers, or multiple clusters.

---

## Common Mistakes

### Reporting Only the Mean

This can mislead when data is skewed or contains outliers.

### Ignoring Sample Size

A mean from 10 observations is less reliable than one from 10,000. Always report count.

### Treating Standard Deviation as Enough

Standard deviation alone does not reveal skewness, multimodality, or outliers.

### Using the Wrong Summary for the Variable Type

* mean for categories: invalid
* mode only for continuous data: often unhelpful
* percentages without counts: incomplete

### Interpreting Statistics Without Context

A standard deviation of 5 may be small or large depending on the unit and domain. Descriptive statistics need business context.

---

## Practical Workflow for Analysts

A reliable descriptive statistics workflow often looks like this:

1. verify the variable type
2. check count and missingness
3. compute center and spread
4. inspect quartiles and percentiles
5. assess skewness, tails, and outliers
6. compare overall summary with subgroup summaries
7. pair numeric summaries with visualizations
8. document interpretation in plain language

This process reduces the risk of drawing conclusions from incomplete or distorted summaries.

---

## Worked Example

Suppose a dataset contains monthly spending by 8 customers:

25, 30, 35, 40, 45, 50, 55, 200

### Basic Summaries

* Mean = 60
* Median = 42.5
* Min = 25
* Max = 200
* Range = 175

### Interpretation

* The mean is much higher than the median because one customer spends far more than the others.
* The range is very large, but that is driven mostly by one extreme value.
* The median gives a more realistic summary of a typical customer.
* A box plot or percentile summary would make the outlier immediately visible.

This is a classic example of why descriptive statistics must be interpreted together, not one at a time.

---

## Choosing the Right Summary

| Situation                        | Preferred Center        | Preferred Spread       |
| -------------------------------- | ----------------------- | ---------------------- |
| Symmetric data with few outliers | Mean                    | Standard deviation     |
| Skewed data                      | Median                  | IQR                    |
| Heavy outliers                   | Median or trimmed mean  | IQR or MAD             |
| Categorical variable             | Mode                    | Frequency / proportion |
| Operational tail metrics matter  | Median plus percentiles | Percentiles            |

---

## Key Takeaways

* Descriptive statistics summarize the main features of a dataset.
* Measures of center include mean, median, and mode.
* Measures of spread include range, variance, standard deviation, and IQR.
* Quartiles and percentiles show relative position in the distribution.
* Distribution shape matters: symmetry, skew, tails, and modality affect interpretation.
* Skewness and kurtosis quantify aspects of shape but should not replace visual inspection.
* Robust statistics such as the median, IQR, MAD, and trimmed mean are valuable for messy real-world data.
* Summary tables are useful only when interpreted in context.
* No single metric is sufficient; analysts should combine numerical summaries, visualizations, and domain knowledge.

---

## Checklist

Before presenting descriptive statistics, confirm that you have:

* reported the sample size
* chosen summaries appropriate to the variable type
* checked for skew and outliers
* included robust measures when needed
* compared mean and median where relevant
* used percentiles when tail behavior matters
* paired important summaries with a visual
* translated the statistics into plain-language interpretation

---

## Suggested Practice Questions

1. When would the median be more useful than the mean?
2. Why is standard deviation less reliable for heavily skewed data?
3. What does a large gap between Q3 and the maximum suggest?
4. Why can two datasets with the same mean require very different business responses?
5. When is a percentile more informative than an average?

---

## In One Sentence

Descriptive statistics turn raw data into interpretable summaries of center, spread, position, and shape, allowing analysts to understand what the data says before trying to explain why it looks that way.
