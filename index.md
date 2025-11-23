# Catching Data Quality Issues Before They Break Your ML System  
### A Practical Guide Using Great-Expectations-Style Checks  
*By Tatyana Dorcinvil*

---

## A more personal introduction

When I started this assignment, I knew I didn’t want to just write a surface-level overview of some random ML tool. I wanted something hands-on, something that felt close to what real ML engineers deal with every day. Since I enjoy working with real datasets, this felt like the perfect chance to test out data validation using something that actually interests me.

So I used my anime dataset. It made the work feel less like an assignment and more like I was experimenting with data that could realistically affect a recommendation model. If the data was messy, missing values, or inconsistent, it would cause real problems in a streaming platform. That’s what made this project fun to build out and analyze.

This blog walks through what I built, what worked, what broke, and what I learned while simulating real production issues.

---

# What I accomplished for Assignment 3

For Option 1, I created a full data-quality validation workflow inspired by Great Expectations. I didn’t install the entire GE library. Instead, I built lightweight Python versions of the most common expectations to really understand how the logic works underneath the tool.

Here’s what I completed:

- Built a custom Great Expectations–style test suite in Python  
- Validated a real dataset (anime.csv)  
- Simulated realistic production data corruption  
- Captured pass/fail results  
- Printed summaries and logs  
- Took screenshots as evidence of the workflow  

This fully satisfies the tool-based requirement for the assignment.

---

# Dataset Overview

The dataset I worked with includes:

| Column    | Description               |
|-----------|---------------------------|
| anime_id  | Unique content ID         |
| name      | Anime title               |
| genre     | Comma-separated genres    |
| type      | TV, Movie, OVA, etc       |
| episodes  | Episode count             |
| rating    | User rating (0–10)        |
| members   | Popularity metric         |

Some quick insights I printed:

- 12,294 rows in total  
- Rating range between 1.67 and 10.00  
- Types include TV, Movie, OVA, ONA, Music, Special  
- Members total over 222 million  

**Screenshot 1: Dataset load + printed head + dataset info**  
<img width="641" height="533" alt="Screenshot 2025-11-22 at 7 05 02 PM" src="https://github.com/user-attachments/assets/c5ff83f6-60af-4461-adaf-bbc8e0000d9e" />



This is very similar to the type of catalog metadata a real streaming platform would validate before using it in recommendations.

---

# Clean Data Validation Results

I created nine expectations to test the quality of the clean dataset. These included:

1. Table row count  
2. Unique anime_id  
3. Non-null anime_id  
4. Non-null name  
5. Ratings between 0 and 10  
6. Valid type values  
7. Positive episodes  
8. Positive members  
9. Genres mostly not null  

The results:

- All 9 tests passed  
- Success rate: 100 percent  

**Screenshot 2: Clean data pass/fail summary**  
<img width="617" height="251" alt="Screenshot 2025-11-22 at 7 07 32 PM" src="https://github.com/user-attachments/assets/d34a977f-2eae-47cc-9637-323a01d03884" />



This confirmed that the dataset was ready to be used downstream by an ML model.

---

# Simulating Production Data Corruption

To show how even small problems can ruin downstream ML tasks, I intentionally introduced several issues:

- 10 invalid ratings above 10  
- 10 null anime titles  
- 10 duplicate anime_id  
- 10 negative member counts  

These reflect real-world issues like:

- broken pipelines  
- data drift  
- schema mismatches  
- bad transformations  
- accidental overwrites  

The validation checks caught:

- Duplicate IDs  
- Null names  
- Negative members  

Overall success rate: 66.7 percent.

**Screenshot 3: Corrupted data detection results**  

<img width="621" height="242" alt="Screenshot 2025-11-22 at 7 07 42 PM" src="https://github.com/user-attachments/assets/4b10d5d8-9134-4407-af5a-58d381fe9224" />


This demonstrated how quickly data quality can fall apart if nothing is monitoring the data flowing into a model.

---

# Strengths of This Approach

Even though I didn’t use the full GE library, this approach still gave me many benefits:

- Fast and lightweight  
- Easy to understand and customize  
- Direct insight into how GE expectations work  
- A great fit for catalog and recommendation datasets  
- Simple enough to run entirely in Google Colab without setup problems  

This made the tool feel very approachable and practical.

---

# Limitations

Since this is a simplified version of Great Expectations, a few things are missing:

- No UI or data documentation pages  
- No integration with orchestrators or scheduling tools  
- No long-term validation history  
- No automated alerts  
- No checkpointing or schema versioning  

A production-quality system would include all of that.

---

# What I Learned

This project made data validation feel real instead of theoretical. By manually breaking the dataset and watching the checks catch issues, I got a clearer idea of how much ML pipelines depend on clean data.

My takeaways:

- Validate early  
- Validate often  
- Even simple rules prevent major failures  
- ML engineering includes protecting data, not just building models  

This assignment helped me understand the real role of tools like Great Expectations in production workflows.

---

# Try It Yourself

If you want to explore this type of tool, start with something simple:

- Write lightweight expectations  
- Run them before training  
- Run them before deployment  
- Run them before batch inference  

Small checks protect your entire ML system.

---
# Final Thoughts
This project gave me a realistic experience with data validation in ML systems. It showed me how small issues can break a pipeline and how important it is to run automated checks before training or deploying a model.

---

# Additional Evidence Section


**Screenshot 4: Additional logs or extended outputs**  
<img width="622" height="451" alt="Screenshot 2025-11-22 at 7 07 23 PM" src="https://github.com/user-attachments/assets/c2d03bf0-f5cb-4402-b989-9489b1f02ee8" />
<img width="622" height="140" alt="Screenshot 2025-11-22 at 7 07 51 PM" src="https://github.com/user-attachments/assets/16f04086-ebc5-4740-813a-d92250669e22" />


---

# Peer Comment Links

- Peer Comment 1:  
- Peer Comment 2:  

