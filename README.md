# MTH1203: PROBABILITY AND STATISTICS

## Practical Test — Python & Jupyter Notebook Study Guide

**Programme:** Bachelor of Science in Information Technology (BSIT)
**Year:** 1
**Semester:** 2
**Course Code:** MTH1203
**Course:** Probability and Statistics

---

# 1. ABOUT THE PRACTICAL TEST

This practical test is done using **Python in a Jupyter Notebook**.

There are **two questions**, and each question carries **20 marks**.

The important instructions are:

* Attempt all questions.
* Use Python to perform the analysis.
* Put the answers in a new Jupyter Notebook.
* Every question must have written explanations in **Markdown cells**.
* Do not rely only on comments inside Python code for explanations.
* Submit a zipped folder containing the Jupyter Notebook and any other required exported files.

The examination lasts **1 hour**.

---

# 2. WHAT IS A JUPYTER NOTEBOOK?

A Jupyter Notebook allows us to combine:

1. Python code
2. Results/output
3. Written explanations

There are two important types of cells.

## Code Cell

A Code Cell is where we write Python code.

Example:

```python
import pandas as pd
```

When we run the cell, Python executes the code and gives us a result.

## Markdown Cell

A Markdown Cell is where we explain what we are doing and what the results mean.

Example:

> The DataFrame contains 12 rows and 8 columns. There are no missing values in the dataset.

The lecturer specifically requires written interpretations in Markdown cells.

---

# 3. IMPORTANT PYTHON LIBRARY — PANDAS

We are using the **pandas** library to work with tables and data.

Import it using:

```python
import pandas as pd
```

`pd` is simply a short name for pandas.

---

# 4. WHAT IS A DATAFRAME?

A **DataFrame** is basically a table inside Python.

You can think of it like an Excel spreadsheet.

For example:

| Name   | Score |
| ------ | ----: |
| Faith  |    80 |
| Kevin  |    47 |
| Miriam |    89 |

In Python, this table can be stored in a DataFrame.

---

# 5. QUESTION 1 — TRAINEE DATA

Question 1 gives us information about **12 first-year IT trainees**.

The table contains 8 columns:

1. Trainee
2. Track
3. Sex
4. LabHours
5. Attendance
6. Score
7. Result
8. Certified

Because the table contains 12 trainees and 8 variables, the expected DataFrame shape is:

```text
(12, 8)
```

This means:

* 12 rows
* 8 columns

---

# 6. CREATING THE DATAFRAME

We create the DataFrame using pandas.

The DataFrame is called:

```python
trainees_df
```

The general structure is:

```python
data = {
    "Trainee": [...],
    "Track": [...],
    "Sex": [...],
    "LabHours": [...],
    "Attendance": [...],
    "Score": [...],
    "Result": [...],
    "Certified": [...]
}

trainees_df = pd.DataFrame(data)
```

The `pd.DataFrame()` function converts the data into a pandas table.

---

# 7. CHECKING THE SIZE OF THE DATAFRAME

Use:

```python
trainees_df.shape
```

The expected result is:

```text
(12, 8)
```

Remember:

```text
(rows, columns)
```

Therefore:

```text
12 = number of trainees
8 = number of variables
```

---

# 8. CHECKING INFORMATION ABOUT THE DATAFRAME

Use:

```python
trainees_df.info()
```

`.info()` gives information such as:

* column names
* number of rows
* data types
* number of non-null values

It helps us understand the structure of our DataFrame.

---

# 9. CHECKING FOR MISSING VALUES

Use:

```python
trainees_df.isnull().sum()
```

The expected result is:

```text
Trainee       0
Track         0
Sex           0
LabHours      0
Attendance    0
Score         0
Result        0
Certified     0
```

The `0` means that the column contains **no missing values**.

## What does `isnull()` mean?

`isnull()` checks whether individual cells are empty/missing.

For example:

```python
trainees_df.isnull()
```

may show:

```text
False
False
False
False
```

`False` means:

> This particular cell is not missing.

When we add `.sum()`:

```python
trainees_df.isnull().sum()
```

pandas counts the missing values in each column.

Therefore:

```text
0
```

means there are no missing values.

---

# 10. CATEGORICAL COLUMNS

Categorical data represents groups or categories.

In Question 1, the categorical columns are:

* Trainee
* Track
* Sex
* Result
* Certified

Examples:

`Sex` contains:

```text
F
M
```

`Result` contains:

```text
Pass
Fail
```

These are categories rather than measurements.

The numerical columns are:

* LabHours
* Attendance
* Score

---

# 11. MEAN

The **mean** is the average.

Formula:

```text
Mean = Sum of all values / Number of values
```

Example:

```text
10, 20, 30
```

Mean:

```text
(10 + 20 + 30) / 3 = 20
```

In pandas:

```python
trainees_df["Score"].mean()
```

This gives the average Score.

For several numerical columns:

```python
trainees_df[["LabHours", "Attendance", "Score"]].mean()
```

---

# 12. MEDIAN

The **median** is the middle value when the values are arranged from smallest to largest.

Example:

```text
10, 20, 30, 40, 50
```

The middle value is:

```text
30
```

Therefore, the median is 30.

In Python:

```python
trainees_df["Score"].median()
```

For several columns:

```python
trainees_df[["LabHours", "Attendance", "Score"]].median()
```

---

# 13. STANDARD DEVIATION

Standard deviation tells us how **spread out** the values are.

Simple way to remember:

### Small standard deviation

Values are relatively close together.

### Large standard deviation

Values are more spread out.

Python:

```python
trainees_df["Score"].std()
```

For several columns:

```python
trainees_df[["LabHours", "Attendance", "Score"]].std()
```

---

# 14. FINDING THE HIGHEST SCORE

There are two important commands:

## `.max()`

`.max()` tells us the **highest value itself**.

Example:

```python
trainees_df["Score"].max()
```

The highest Score is:

```text
93
```

So:

```text
max() = What is the highest value?
```

---

# 15. `.idxmax()`

`.idxmax()` tells us the **index/row position where the highest value occurs**.

Example:

```python
trainees_df["Score"].idxmax()
```

This gives:

```text
8
```

because the highest score, 93, is on row/index 8.

Therefore:

```text
idxmax() = Where is the highest value?
```

---

# 16. `.loc`

`.loc` is used to **locate/select a row or rows**.

Example:

```python
trainees_df.loc[8]
```

This means:

> Locate row 8 and show its information.

We can combine `.loc` with `.idxmax()`:

```python
trainees_df.loc[trainees_df["Score"].idxmax()]
```

This means:

> Find where the highest Score is located, then show the entire row.

The result identifies the trainee with the highest score.

In this dataset, that is:

**Diana — Score 93**

---

# 17. WHY THIS DOES NOT WORK

Do NOT confuse:

```python
trainees_df["Score"].max()
```

with:

```python
trainees_df["Score"].idxmax()
```

If you write:

```python
trainees_df.loc[trainees_df["Score"].max()]
```

Python first finds:

```text
93
```

Then it tries to do:

```python
trainees_df.loc[93]
```

But our DataFrame has indexes:

```text
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11
```

There is no index 93.

Therefore, this can produce a `KeyError`.

The correct code is:

```python
trainees_df.loc[trainees_df["Score"].idxmax()]
```

---

# 18. FINDING THE LOWEST SCORE

For the lowest value, use:

```python
trainees_df["Score"].min()
```

This gives the lowest Score itself.

To find where the lowest score occurs:

```python
trainees_df["Score"].idxmin()
```

To display the entire trainee record:

```python
trainees_df.loc[trainees_df["Score"].idxmin()]
```

In this dataset:

**Tonny has the lowest score — 41.**

---

# 19. QUICK MEMORY TABLE

| Python command    | Simple meaning                            |
| ----------------- | ----------------------------------------- |
| `pd.DataFrame()`  | Create a table                            |
| `.shape`          | Show rows and columns                     |
| `.info()`         | Show information about the DataFrame      |
| `.isnull()`       | Check individual cells for missing values |
| `.isnull().sum()` | Count missing values                      |
| `.mean()`         | Calculate average                         |
| `.median()`       | Find middle value                         |
| `.std()`          | Measure spread                            |
| `.max()`          | Find highest value                        |
| `.min()`          | Find lowest value                         |
| `.idxmax()`       | Find location/index of highest value      |
| `.idxmin()`       | Find location/index of lowest value       |
| `.loc[]`          | Locate/select a row                       |

---

# 20. QUESTION 1 — WHAT WE STILL HAVE TO DO

After Q1(a), we continue with:

### Q1(b)

Calculate:

* Mean
* Median
* Standard deviation

for:

* LabHours
* Attendance
* Score

Then identify:

* Highest-scoring trainee
* Lowest-scoring trainee

And explain how spread out the scores are.

### Q1(c)

Calculate:

* Q1
* Q2
* Q3
* IQR
* 90th percentile
* Outlier boundaries
* Score outliers
* `.describe()`

Then determine whether the Score distribution is approximately symmetric or skewed.

### Q1(d)

Separate:

* Pass group
* Fail group

Then calculate:

* Mean LabHours
* Mean Attendance

for each group.

Then compare the gaps.

### Q1(e)

Write a **120–150 word recommendation** based on the results and give one limitation of using only 12 records.

---

# 21. QUESTION 2 — MPG DATASET

Question 2 uses:

```text
mpg.csv
```

The dataset contains records about cars.

Important columns include:

| Column       | Meaning                    |
| ------------ | -------------------------- |
| mpg          | Fuel efficiency            |
| cylinders    | Number of cylinders        |
| displacement | Engine displacement        |
| horsepower   | Engine horsepower          |
| weight       | Vehicle weight             |
| acceleration | 0–60 mph acceleration time |
| model year   | Year of manufacture        |
| origin       | Region of origin           |
| name         | Car model name             |

---

# 22. IMPORTANT STATISTICAL TERMS TO LEARN

## Quartile

Quartiles divide data into four sections.

### Q1

25th percentile.

### Q2

50th percentile / median.

### Q3

75th percentile.

---

# 23. IQR

IQR means:

**Interquartile Range**

Formula:

```text
IQR = Q3 - Q1
```

It represents the spread of the middle 50% of the data.

---

# 24. PERCENTILE

A percentile tells us the position of a value within a dataset.

For example, the 90th percentile means approximately 90% of observations are at or below that value.

Python:

```python
data["weight"].quantile(0.90)
```

---

# 25. OUTLIERS

An outlier is a value that is unusually far from the rest of the data.

The assignment uses the **1.5 × IQR rule**.

Lower boundary:

```text
Q1 - 1.5 × IQR
```

Upper boundary:

```text
Q3 + 1.5 × IQR
```

Values below the lower boundary or above the upper boundary are considered outliers using this rule.

---

# 26. IMPORTANT RULE FOR THIS TEST

Do not just run Python code and leave the numbers.

For every important result, explain what it means.

For example:

### Code

```python
trainees_df["Score"].mean()
```

### Output

```text
65.5
```

### Interpretation

> The mean Score is 65.5, meaning that the average score among the 12 trainees was 65.5.

The explanation belongs in a **Markdown cell**.

---

# 27. THE MAIN IDEA TO REMEMBER

When doing statistics in Python, think of the process as:

```text
DATA
  ↓
CREATE DATAFRAME
  ↓
CHECK DATA
  ↓
CALCULATE STATISTICS
  ↓
LOOK AT RESULTS
  ↓
INTERPRET RESULTS
```

Python performs the calculations.

**You explain what the calculations mean.**

That is what the lecturer is testing.
