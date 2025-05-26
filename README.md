## LLM-Driven Hiring System Analysis

This project analyzes data from an LLM-driven automated vetting system for job applications. The goal is to understand the system's effectiveness by examining the relationship between LLM-generated cosine similarity scores, candidate progression through hiring stages, and candidate job titles.

A PDF of the analysis presentation can be found here - <a href="https://bit.ly/Amoo-pariti">🔗Report LINK</a>

### Data Source

The analysis utilizes two main datasets:

*   `vetting_df`: Contains information on the result of automated vetting for each application. Key columns include `candidate_titles` (job titles of the candidate), `cos_sim_score` (LLM-generated cosine similarity score), and `percentiles` (percentile mapping of the candidate). The automated vetting process uses an LLM to encode candidate experience and vacancy requirements, then calculates a cosine similarity score between them.
*   `application_df`: Provides information on the hiring stage of each application. The hiring stages follow a defined order from `referred` to `hired`.

An application can be closed at any of the defined hiring stages.

### Methodology

The analysis was conducted using Python with the Pandas library in a Jupyter Notebook (`Amoo_assignment.ipynb`). The key steps involved:

1.  **Data Loading and Initial Exploration:**
    *   Loaded `vetting_assignment.csv` and `application_assignment.csv` into Pandas DataFrames.

2.  **Data Cleaning and Preprocessing:**
    *   **`vetting_df`:**
        *   Handled missing values by removing rows with NaNs.
        *   Extracted `candidate_country` from the `filtered_candidate_briefs` column (e.g., 'NG', 'US', 'ZA').
    *   **`application_df`:**
        *   Cleaned the `status` column by removing the prefix `ADMIN_APPLICATION_STATUS_`.
        *   Cleaned the `application_stage` column by removing the prefix `NEXT_APPLICATION_STAGE_`.
    *   **Merging:** Combined the cleaned `vetting_df` and `application_df` into a single DataFrame (`merged_df`) using `application_id` as the key.
    *   Ensured `job_id` was of integer type.
    *   Removed any remaining rows with NaN values from the merged DataFrame.

3.  **Exploratory Data Analysis (EDA):**
    *   Calculated descriptive statistics, including the total number of valid applications.
    *   Determined the distribution of applications across different `job_id`s.
    *   Analyzed the count of applications in each `application_stage` grouped by `percentiles`.
    *   Calculated the minimum, maximum, and mean `cos_sim_score` grouped by `percentiles` and `job_id`.
    *   Identified the top countries by applicant volume (Kenya, South Africa, Nigeria, USA, India).

4.  **Analysis of Key Questions:**
    The following questions were addressed through targeted data filtering and aggregation:

    *   What is the most common `application_stage` for applications with a `cos_sim_score` higher than 0.7?
    *   What is the most common `application_stage` for applications with a `cos_sim_score` lower than 0.3?
    *   Is there a correlation between a higher `cos_sim_score` and the number of job titles listed in `candidate_titles`?

### Key Findings & Insights

1.  **Applications with `cos_sim_score > 0.7`:**
    *   The most common `application_stage` for these high-similarity candidates is **SCREENING**.
    *   **Insight:** Even candidates identified as strong matches by the LLM (only 8 such applications in the dataset, with 3 in SCREENING) predominantly undergo the initial screening phase. This suggests that while the LLM is effective in identifying potentially good fits, human review or further automated checks are still a critical part of the early-stage process. It may indicate a robust initial filtering mechanism that doesn't solely rely on the LLM score for progression.

2.  **Applications with `cos_sim_score < 0.3`:**
    *   The most common `application_stage` for these low-similarity candidates is also **SCREENING**.
    *   **Insight:** This finding reinforces the role of the screening stage in filtering out candidates. Applicants with low LLM scores are largely identified and potentially rejected at this early point, highlighting the screening process's efficiency in managing less suitable applications.

3.  **Correlation between `cos_sim_score` and Number of Candidate Titles:**
    *   A **weak positive correlation of approximately 0.096** was found.
    *   **Insight:** The number of job titles a candidate has listed does not have a significant linear relationship with their cosine similarity score. This implies that the LLM's scoring is more nuanced than simply counting past roles and likely focuses on the relevance of those roles to the specific job requirements. The diversity or quantity of job titles alone is not a strong predictor of a high match score from the LLM.

### Technical Skills Demonstrated

*   **Data Analysis:** Python, Pandas
*   **Data Cleaning & Preprocessing:** Handling missing values, string manipulation, data type conversion, merging DataFrames.
*   **Exploratory Data Analysis (EDA):** Descriptive statistics, grouping and aggregation, value counts.
*   **Problem Solving:** Interpreting data and drawing actionable insights from analysis.
*   **Reporting:** Summarizing findings from a Jupyter Notebook.

### Further Analysis & Recommendations

To further enhance the automated vetting process, the following was suggested:

*   **Deeper Dive into `candidate_titles`:**
    *   Analyze the distribution of the number of job titles per candidate.
    *   Investigate if specific job titles are more prevalent or correlate with higher/lower `cos_sim_score`.
*   **Industry Correlation:**
    *   **Recommendation:** Conduct a detailed analysis to explore the correlation between the industry of a candidate's previous job titles, the industry of the job they applied for, and the resulting `cos_sim_score`. This could reveal if the LLM (MPNet v2) inherently favors candidates with direct same-industry experience and help refine the model or evaluation criteria for better cross-industry talent identification.

---
*This README was updated based on the analysis performed in `Amoo_assignment.ipynb`.*
