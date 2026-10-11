# Correlating AI Errors with Retrieval Using Pandas

## Project Overview

This project investigates the relationship between retrieval failures and factual errors in an AI support chatbot using Python and Pandas.

The objective is to determine whether factual inaccuracies occur more frequently when the retrieval component fails to find relevant information.

## Objectives

- Filter a dataset to isolate a specific user-intent segment.
- Create a contingency table using `pd.crosstab()`.
- Analyze retrieval status against error categories.
- Calculate error distributions using normalized percentages.
- Use data-driven evidence to support root cause analysis.

## Dataset

The notebook uses `synthetic_log_file.csv`, which contains 5,000 rows and 5 columns.

The relevant columns are:

- `user_id`: Identifier for the user.
- `user_intent`: The user's intent, such as `complaint`, `inquiry`, or `ask_refund_policy`.
- `timestamp`: When the interaction occurred.
- `retrieval_status`: Whether retrieval succeeded or resulted in a miss.
- `error_category`: The recorded outcome category, such as `factual_inaccuracy` or `no_error`.

**Note:** The dataset is synthetic, so the findings demonstrate an analysis technique rather than prove a real production chatbot's behavior.

## Methodology

### 1. Load and Inspect the Dataset

Import Pandas, load the CSV file, and inspect the first few rows.

### 2. Filter Refund Policy Interactions

Select records where `user_intent == 'ask_refund_policy'`.

This produces **976 interactions** for focused analysis.

### 3. Validate the Filter

Check the dataset shape, available user intents, and number of matching interactions.

### 4. Create a Contingency Table

Use `pd.crosstab()` to count combinations of `retrieval_status` and `error_category`.

Rows represent retrieval status, while columns represent error categories. The values are raw counts.

### 5. Calculate Error Distribution

Normalize the table by row to calculate the percentage distribution of error categories within each retrieval-status group.

## Results

The analysis produced the following percentage distribution:

| Retrieval status | Attribution error | Factual inaccuracy | Irrelevant response | No error |
|---|---:|---:|---:|---:|
| Miss | 0.0% | 56.4% | 31.4% | 12.2% |
| Success | 1.1% | 0.9% | 2.2% | 95.9% |

### Interpretation

- When retrieval results in a **miss**, 56.4% of the selected interactions are labeled as factual inaccuracies.
- When retrieval is successful, 0.9% are labeled as factual inaccuracies.
- The difference suggests a strong association between retrieval misses and factual inaccuracies in this selected dataset.

These percentages are calculated within each retrieval-status group, not across the entire dataset.

## Tools and Technologies

- Python
- Pandas
- Jupyter Notebook / Google Colab
- Exploratory Data Analysis (EDA)
- Contingency Tables
- Error Analysis and Root Cause Investigation

## Key Takeaway

A crosstab helps engineers identify patterns between retrieval outcomes and AI error categories. This can help prioritize investigation of the retrieval pipeline before assuming that the language model itself needs retraining.

**Limitation:** The analysis demonstrates an association, not proof of causation. Further investigation and controlled testing would be needed to establish the root cause.

## How to Run

1. Clone or download this repository.
2. Install the required dependencies.
3. Make the CSV dataset available at the path expected by the notebook.
4. Open the notebook in Jupyter or Google Colab.
5. Run the cells in order.

