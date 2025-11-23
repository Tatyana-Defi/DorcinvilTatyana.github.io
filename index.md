# Catching Data Quality Issues Before They Break Your ML System  
### A Practical Guide Using Great-Expectations-Style Checks  
*By Tatyana Dorcinvil*

---

## A more personal introduction

When I started this assignment, I knew I wanted to choose something hands-on. I didn’t want to just write about a tool; I wanted to actually try something that feels close to what real ML engineers do every day. Since I love working with real datasets, I figured this was the perfect chance to experiment with data quality checks.

I used my anime dataset, which honestly made the whole project more fun. Instead of another dry academic dataset, I got to validate information on shows, genres, ratings, members, and everything else that would normally feed into a recommendation system. If anything was messy or broken, it would immediately impact a model’s performance, which made the project feel realistic.

This blog walks through what I built, what worked, and what I learned while simulating real production issues.

---

# What I completed for Assignment 3

For Option 1, I built a full data-quality validation workflow inspired by Great Expectations. Instead of installing the entire GE suite, I created lightweight Python versions of the most useful expectations. This let me understand exactly how data validation works behind the scenes.

Here’s what I accomplished:

- Created a custom Great Expectations–style test suite in Python  
- Validated a real dataset (anime.csv)  
- Simulated realistic production data corruption  
- Collected pass/fail results  
- Added printed logs and summaries  
- Took screenshots showing all validation steps  

This fully meets the “Try a tool” requirement.

---

# Dataset Overview

The dataset I used contains:

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

- 12,294 total rows  
- Rating range between 1.67 and 10.00  
- Types include TV, Movie, OVA, ONA, Music, Special  
- Members total over 222 million  

**[INSERT SCREENSHOT 1: Your dataset load + printed <img width="641" height="533" alt="Screenshot 2025-11-22 at 7 05 02 PM" src="https://github.com/user-attachments/assets/4dc77e23-08b5-4198-999e-6c11efe497c5" />
head + dataset info]**

![Uploading Screenshot 2025-11-22 at 7.05.02 PM.png…]()


This gives a very realistic starting point, because streaming platforms usually deal with catalog data that varies a lot in quality.

---

# Clean Data Validation

I created nine expectations to test the dataset before any ML pipeline would use it. These covered:

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

- 9 out of 9 tests passed  
- Success rate: 100 percent  

**[INSERT SCREENSHOT 2: Clean data pass/fail v<img width="633" height="451" alt="Screenshot 2025-11-22 at 7 07 23 PM" src="https://github.com/user-attachments/assets/213478f2-0b0f-41d7-8bf6-451bb823b980" />
alidation summary]**

This confirmed the dataset was ready to be used in a recommendation system.

---

# Simulating Production Data Corruption

To make things more realistic and show why data validation matters, I intentionally introduced several issues:

- 10 invalid ratings above 10  
- 10 null names  
- 10 duplicate anime_id  
- 10 negative member counts  

These represent the kinds of things that happen when pipelines break, schemas change, or bad data flows in from upstream systems.

The validation checks caught:

- Duplicate IDs  
- Null names  
- Negative members  

Success rate: 66.7 percent

**[INSERT SCREENSHOT 3: Corrupted <img width="621" height="242" alt="Screenshot 2025-11-22 at 7 07 42 PM" src="https://github.com/user-attachments/assets/5788ca80-a57f-450c-a158-d70e0cfa7337" />
data detection printout]**

This showed that even simple checks can catch major problems before they damage a production ML workflow.

---

# Strengths of This Approach

Even though I didn’t install the full Great Expectations library, this project still gave me:

- Fast, lightweight checks  
- Clear insight into how expectations work  
- Flexibility to modify tests however I want  
- A great fit for recommendation system workflows  
- A deeper understanding of MLOps-style data validation  

This approach was especially helpful because I could run everything inside Google Colab without heavy setup.

---

# Limitations

Since this was a simplified version of the real tool, a few things are missing:

- No Great Expectations UI or data docs  
- No pipeline integration  
- No checkpoints  
- No long-term validation history  
- No automated alerts  

If this were a real production system, I would hook these tests into an orchestrator like Airflow or Prefect and add automated reporting.

---

# What I Learned

This project made data validation feel much more real. Instead of reading about pipeline failures, I actually created them and watched the validation suite catch them. I learned that:

- Data should be validated as early as possible  
- Even small tests can stop major issues  
- ML isn’t just about modeling — it’s also about protecting data pipelines  
- Ongoing monitoring is essential  

This assignment gave me a clearer picture of what production-level ML engineering looks like.

---

# Try It Yourself

If you want to explore this the same way I did, start by:

- Writing simple expectations  
- Running them before model training  
- Running them before deployment  
- Running them before batch jobs  

Protecting your data protects your entire ML system.

---

**[INSERT SCREENSHOT 4: Any additional logs or plots]**
