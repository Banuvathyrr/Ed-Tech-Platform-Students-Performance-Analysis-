
<h1 align="center">Ed-Tech Platform: Analyzing Student Performance and Engagement</h1>


### Introduction 
In the ever-evolving landscape of education, institutions and training centers must leverage data to optimize their outreach and enrollment strategies. This project, titled "Enhancing Student Enrollment Using Power BI," aims to utilize data analysis to improve student enrollment rates by understanding patterns in inquiries and identifying key factors that influence conversion.

Through this project, we have analyzed a dataset containing 74 inquiries over a period of 141 days, focusing on various aspects such as weekly, monthly, and daily trends, age group preferences, course popularity, and the impact of prior coding experience on course interest. By leveraging Power BI, we have visualized these insights to create a comprehensive understanding of the data, enabling us to develop targeted strategies to enhance student engagement and increase enrollment.

The findings from this analysis will provide actionable recommendations for improving follow-up processes, optimizing communication channels, addressing concerns about fees, tailoring course content to specific age groups, and enhancing overall course presentation. By applying these strategies, educational institutions can better meet the needs of prospective students and boost their enrollment rates.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Project Overview  
This dashboard is designed to analyze a candidate's performance in multiple-choice questions across various topics. Key metrics and insights are provided to evaluate their overall and topic-specific performance, identify strengths and weaknesses, and suggest targeted learning paths.  

**Key Areas of Analysis:**  
**Overall Performance Metrics:** Evaluate total score, percentage correct, accuracy rate, and time spent on questions.  
**Topic-Specific Performance:** Analyze scores, accuracy, and topic mastery levels to identify strengths and weaknesses.  
**Comparative Analysis:** Compare the candidate's performance against peers, percentile ranks, and trends over time.  
**Response Patterns and Behavioral Insights:** Examine consistency, guessing patterns, and time management to understand behavioral tendencies.  
**Skill Gap Identification:** Highlight unaddressed areas and critical skills that require improvement.  
**Learning Path Suggestions:** Recommend topics for review and study materials to enhance learning outcomes.  

By addressing these key areas, the dashboard provides a comprehensive view of the candidate's talents and areas for improvement, helping to guide effective study strategies and skill development.  

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Data Sources
The dataset contains 1 csv file:
1. sample_student_perfomance.csv
   
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Tools
- PowerBI -Data Cleaning, Data Visualization and creating dashboards

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Data Cleaning/Preparation
- Column names checked.  
- Checked datatype of each column .  
- Checked for rows having errors and empty values.


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### DASHBOARD

**1. OVERALL PERFORMANCE METRICS**   

**a) Total Score: What is the candidate's total score across all topics?**    
The Score calculated column now directly converts the Boolean value into a numeric score, reducing complexity.  
```Score = IF('Student performance'[Is Correct] = TRUE(), 1,  IF('Student performance'[Is Correct] = FALSE(), 0, BLANK()))```  

The Total Score measure uses the SUM function to aggregate scores, ensuring accurate total score computation for any candidate.  
```Total Score = SUM('Student performance'[Score])```    


**b) Percentage Correct: What percentage of questions did the candidate answer correctly overall?**  
The Correct Answers measure counts the number of rows where the score is 1, indicating that the candidate answered correctly.  
![image](https://github.com/user-attachments/assets/e21bc6d3-85be-40da-87de-d3db41a30a07)  

The Percentage Correct measure calculates the percentage of questions answered correctly.  
![image](https://github.com/user-attachments/assets/def88133-b022-4fbf-81f8-fb353605b372)  


**c) Accuracy Rate: What is the candidate's accuracy rate (correct answers vs. total attempts)?**  
The "Accuracy rate" measure calculates the percentage of correct answers relative to the total number of questions. 
If the total number of questions is zero (to avoid division by zero error), the measure returns 0.  
![image](https://github.com/user-attachments/assets/5afabab0-c30d-432c-9a11-015205c2b186)  


**d) Time Spent: How much time did the candidate spend on each section or question?**   
The "Total Time Taken (in seconds)" measure calculates the sum of all the time taken by the candidate across all questions. This measure gives the total duration, in seconds, that the candidate spent answering questions.
```Total Time Taken (in seconds) = SUM('Student performance'[Time Taken (Seconds)])```    

   

**2. TOPIC SPECIFIC PERFORMANCE**    
**a) Strengths and Weaknesses: Which topics did the candidate perform best in, and which did they struggle with?**  
The "Strengths" measure identifies the topics where a candidate's score is 50% or higher. It concatenates the names of these topics into a single string, separated by commas. This measure helps to quickly identify and display the candidate's stronger areas based on their performance in different topics.  
![image](https://github.com/user-attachments/assets/60c0421b-fc9f-4ca0-8d86-469c6650e604)  

![image](https://github.com/user-attachments/assets/6d4bde53-1218-4c1d-a083-4779dc911cfa)  

**b) Topic Mastery Level: How well does the candidate understand each topic? (e.g., Beginner, Intermediate, Advanced)**  
The first DAX formula calculates the percentage of correct answers by dividing the number of correct answers by the total questions and multiplying by 100. The second DAX formula categorizes the mastery level based on this percentage, classifying it as "Advanced" for 80% or more, "Intermediate" for greater than 50% but less than 80%, and "Beginner" for 50% or less.  
![image](https://github.com/user-attachments/assets/91fa2070-ebab-46e0-9a90-5e53e8bcfbde)  

![image](https://github.com/user-attachments/assets/cb2b6dec-2849-4dc9-9d6d-93e1951d4c20)


**4) COMPARATIVE ANALYSIS**
**Comparison to Peers: How does the candidate's performance compare to the average performance of their peers?**  
The first DAX formula computes the candidate’s average score by dividing their total score by the total number of questions.    
![image](https://github.com/user-attachments/assets/2e8ed584-cdfa-40a1-9779-1933d3ae59f8)    
The second DAX formula calculates the average score of other candidates by excluding the current candidate’s scores from the average calculation.  
![image](https://github.com/user-attachments/assets/badd5066-ee7a-41c5-a519-7576cdc04f12)  
This allows for comparison of a candidate’s performance against the average score of their peers.  

**5) SKILL GAP IDENTIFICATION**  
**a) Unaddressed Areas: Are there any topics that the candidate did not cover or answered very few questions on?**    
The DAX measure Low Question Topics Measure identifies topics in the 'Student performance' table with fewer than 3 questions. It first counts the number of questions per topic, filters those with less than 3 questions, and then concatenates the names of these topics into a comma-separated string.   
![image](https://github.com/user-attachments/assets/7630effe-ab6a-4511-bbe4-a4670052f562)  

**b) Critical Skills Lacking: Which key skills or knowledge areas are most lacking based on incorrect answers?**  
The DAX calculated column KeySkills assigns specific key skills to different topics in the 'Student performance' table. The SkillsforReview measure then creates a comma-separated list of these key skills for topics where the percentage of incorrect answers is 50% or more, helping to highlight areas needing review.

![image](https://github.com/user-attachments/assets/c1e50ce9-d8bc-4eda-88f2-069bcd1b96fe)  
![image](https://github.com/user-attachments/assets/f3de29b0-16ac-4490-9ad1-b6273caa4202)  

**6. LEARNING PATH SUGGESTIONS**  
The DAX measure Topics For Review identifies topics from the 'Student Performance' table where the average score is less than 50%. It calculates the average score for each topic by dividing the sum of scores by the count of question IDs, filters for topics with an average below 50%, and concatenates these topics into a comma-separated list for review.  
![image](https://github.com/user-attachments/assets/bba11549-2bc5-47c6-a916-9db453fbe2a9)  
The DAX calculated column Incorrect Answers counts the number of rows in the 'Student performance' table where the score is zero.   
![image](https://github.com/user-attachments/assets/548b1952-a028-4c0c-be03-fd4252822d23)  
The measure Percent Incorrect calculates the percentage of incorrect answers by dividing the number of incorrect answers by the total number of questions and multiplying by 100.  
![image](https://github.com/user-attachments/assets/25438e99-3b0a-43fb-bda7-a2b661ecbcdf)  
The calculated column Study Material assigns recommended study resources based on the topic, such as maps for Geography or storybooks for History  
![image](https://github.com/user-attachments/assets/4d2cabfe-23ca-4400-98f3-808b06302edf)    
The measure Study Materials to Refer generates a comma-separated list of study materials for topics where the percentage of incorrect answers is 50% or higher, aiding in targeted study efforts.  
![image](https://github.com/user-attachments/assets/71264f7d-86aa-4505-8d28-423ff9b9ce5a)


**6) DETAILED QUESTION ANALYSIS (Optional)**  
**Question-by-Question Breakdown: How did the candidate answer each question? (e.g., correct, incorrect, time taken, confidence level)** 
The DAX calculated column Time split categorizes the time taken to answer questions in the 'Student performance' table into three groups based on the time in seconds. If the time taken is 30 seconds or less, it is labeled as "Quick (<30s)". If it is between 31 and 59 seconds, it is labeled as "Moderate (30s-60s)". For times of 60 seconds or more, it is labeled as "Long (>60s)". This helps in analyzing the time efficiency of students in answering questions.    
![image](https://github.com/user-attachments/assets/7c87629b-08cc-4ea4-affc-14ab676ad55f)    

The DAX calculated column ConfidenceLevel determines a student's confidence based on their correctness and the time taken to answer. It assigns a "High" confidence level if the answer is correct and answered quickly ("Quick (<30s)"). A "Medium" confidence level is assigned for correct answers with moderate ("Moderate (30s-60s)") or long ("Long (>60s)") times. For incorrect answers, regardless of the time taken, it assigns a "Low" confidence level. This column helps assess student confidence levels based on their performance and response time.  
![image](https://github.com/user-attachments/assets/517047a6-4adc-446d-b5ac-bb6a2ed9d6e2)























### Dashboard 
- Check the dashboard here: https://mavenanalytics.io/project/18839
 


















