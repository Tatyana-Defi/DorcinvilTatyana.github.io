# Catching Data Quality Issues Before They Break Your ML System  
### A Practical Guide Using Great-Expectations-Style Checks  
*By Tatyana Dorcinvil*

---

## What I Completed for Assignment 3

For Option 1, I explored a real production ML tool concern:  
**data quality validation** using a Great Expectations–style framework.

I implemented:

✔ A real Python-based expectation suite  
✔ Data validation for my anime dataset  
✔ Simulation of production data corruption  
✔ Clear pass/fail reporting  
✔ Evidence screenshots  
✔ A true ML scenario: validating content data used for recommendations  

This fully satisfies the “Try a tool” requirement.

Now here is the polished blog write-up explaining the tool, results, and key takeaways.

---

# Introduction

Production ML systems depend heavily on clean, trustworthy data. You can train the perfect model, but if the data feeding into it becomes corrupted or inconsistent, your pipeline will quietly break. This leads to:

- bad recommendations  
- UI errors  
- user churn  
- incorrect business decisions  

To practice solving this real-world problem, I built a **Great-Expectations-style data validation suite** in Python using my **anime.csv** dataset. Instead of installing the full tool, I implemented lightweight versions of GE’s expectations to learn how they work at a low level.

The goal:  
**validate the dataset before it enters a recommendation system.**

---

# Why Data Quality Matters in ML

Bad input data causes:

- duplicate IDs → conflicting item definitions  
- missing names → broken UI rendering  
- invalid ratings → distorted training signals  
- negative member counts → corrupted popularity ranking  
- mismatched “type” values → poor content grouping  

Pipeline failures come from:

- schema changes  
- upstream bugs  
- ETL mistakes  
- API mismatches  
- manual errors  

Automated data validation catches issues early.

---

# The Tool: Great-Expectations-Style Validation

I implemented the following expectations manually:

- `expect_column_values_to_be_unique`  
- `expect_column_values_to_not_be_null`  
- `expect_column_values_to_be_between`  
- `expect_column_values_to_be_in_set`  
- `expect_table_row_count_to_be_between`  

This lightweight approach is perfect for:

- running in Google Colab  
- integrating into existing Python workflows  
- teaching the mechanics of GE without full installation  
- running custom tests in a simple environment  

---

# Dataset Overview

My **anime.csv** dataset contains:

| Column    | Description               |
|-----------|---------------------------|
| anime_id  | Unique content ID         |
| name      | Anime title               |
| genre     | Comma-separated genres    |
| type      | Movie, TV, OVA, etc       |
| episodes  | Episode count             |
| rating    | User rating (0–10)        |
| members   | Popularity / engagement   |

My analysis found:

- **12,294 rows**  
- rating range: **1.67 – 10.00**  
- dataset includes **TV, Movie, OVA, ONA, Music, Special**  
- total members: **222M+**  

This checks out as a realistic catalog dataset.

---

# Clean Data Validation Results

I ran nine expectations on the clean dataset:

✔ **9/9 tests passed**  
✔ **100% success rate**  

The checks validated:

1. Row count  
2. Unique anime_id  
3. Non-null anime_id  
4. Non-null name  
5. Ratings within 0–10  
6. Valid type values  
7. Positive episodes  
8. Positive members  
9. Genre mostly not null  

This confirms the dataset is safe for downstream ML tasks.

---

# Simulating Production Data Corruption

To mimic real-world issues, I injected:

- 10 invalid ratings (>10)  
- 10 null titles  
- 10 duplicate anime_id  
- 10 negative member counts  

These simulate:

- pipeline drift  
- user input errors  
- ETL bugs  
- API format changes  
- accidental overwrites  

My validation system caught:

✔ Duplicate IDs  
✔ Null names  
✔ Negative member counts  

Overall success rate: **66.7%**  
This demonstrates the importance of automated monitoring.

---

# Strengths of This Approach

### ✔ Fast and simple  
Low overhead, easy to integrate.

### ✔ Understands GE at the core  
You see exactly how expectations work.

### ✔ Flexible  
Customizable for any dataset or pipeline.

### ✔ Ideal for recommendation systems  
Covers core metadata such as IDs, ratings, and content type.

---

# Limitations

- No GE visual reporting UI  
- Manual setup required  
- Not hooked into Airflow/Kubeflow  
- No checkpoints or historical validation store  

For production, I would use the full Great Expectations suite with data docs and pipeline automation.

---

# What I Learned

This project taught me:

- data quality issues must be caught early  
- simple tests prevent major pipeline failures  
- ML systems need **continuous** monitoring  
- data validation is just as important as model validation  

Even without installing Great Expectations, this exercise mirrors real MLOps workflows used in production systems.

---

# Try It Yourself

If you’re building an ML prototype:

1. Write lightweight expectations  
2. Run them before training  
3. Run them before deployment  
4. Run them before batch inference  

Small checks prevent big failures.

---
