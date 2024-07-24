## A pdf of the analysis presentation can be found here - [https://bit.ly/Amoo-pariti](url)

The file vetting_df contains information on the result of automated vetting for each application. The columns provide basic information on the jobs of a candidate ['candidate_titles'], the cosine similarity score given by an LLM model ['cos_sim_score'] and the percentile the candidate is mapped to ['percentiles'].
What you need to know on the automated vetting process is that it uses an LLM to encode the experience of a candidate and the experience requested in a vacancy, then provides a cosine similarity score on the similarity between the two inputs.

The file application_df provides information on the hiring stage of each application, where the data model order of an application is the following: 
1. referred
2. contacted
3. screening
4. shortlisted
5. interviewing
6. later rounds
7. offered
8. started
9. probation passed
10. hired

An application can be closed at any of the steps above.
