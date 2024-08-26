
<h1 align="center">Ed-Tech Platform: Analyzing Student Performance and Engagement</h1>


### Introduction 
Ed-Tech platforms have transformed the educational landscape by offering interactive and personalized learning experiences. Analyzing student performance on these platforms focuses on evaluating student performance based on various metrics such as accuracy, speed, consistency, and confidence levels. By examining detailed question-by-question responses and overall topic proficiency, this study aims to provide insights into student learning patterns, identify key areas for improvement, and suggest targeted strategies to enhance educational outcomes.  

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



















----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Results/ Findings
**Demographic Insights:**
- Survey Participation: The Codex survey included 10,000 respondents from 10 cities, with a higher number of male participants compared to female. This demographic trend may reflect gender imbalances in certain sectors of the food and beverage industry or interests.  

- City-Specific Engagement:
Bangalore: Highest number of respondents, likely due to its diverse culinary scene and tech-savvy population engaged in health and nutrition trends.  
Hyderabad and Mumbai: Both cities have rich food cultures and a high concentration of food and beverage professionals, contributing to their high engagement.  
Chennai and Pune: Chennai’s traditional South Indian cuisine and Pune’s innovative food scene reflect strong local interest in food and beverage trends.  
Kolkata and Ahmedabad: Participation from these cities indicates interest in traditional foods and global food trends.  
Delhi: Lower respondent rate could suggest market saturation or the need for targeted engagement strategies.  
Jaipur and Lucknow: Strong culinary traditions but lower engagement, potentially due to lesser focus on international food standards.  
Tier 1 vs. Tier 2 Cities: Tier 1 cities generally show higher awareness and engagement with global food and beverage trends, including Codex standards, compared to Tier 2 cities.  

**Consumer Preferences:**  
- Consumption Frequency: Beverages are most commonly consumed 2-3 times a week, indicating they are a regular but not daily part of consumers' lives, often enjoyed socially or with meals.  
- Marketing Channels: Online ads are the most effective marketing channel, reaching consumers through digital platforms. This highlights the importance of targeted digital advertising in engaging with specific audience segments.  
- Consumption Situations:  
Sports/Exercise: High consumption of beverages during sports or exercise indicates a demand for hydration and energy products.  
Studying/Working: Beverages consumed during studying or working are chosen for their ability to enhance focus and productivity, highlighting the need for drinks that provide energy and concentration support.  
Energy and Focus: There is significant consumer interest in beverages that offer increased energy and focus, driven by busy lifestyles and the need for convenient solutions to boost cognitive performance.  

**Brand Penetration:**  
- Brand Reputation: Coca-Cola's strong reputation is a key factor in its popularity, reflecting consumer trust and the brand’s effective marketing and quality consistency.  
- Price Range Preference: The favored price range of ₹50-₹99 reflects a balance between affordability and perceived value, making products in this range appealing to consumers.  

**Reasons for Not Trying New Beverages:**
- Health Concerns: Health-related concerns, including sugar content and artificial ingredients, prevent consumers from trying new beverages.
- Availability: Limited local availability is a barrier to trying new products.
- Caffeine Sensitivity: Some consumers avoid energy drinks due to their caffeine content, preferring beverages without stimulants.
- Brand Perception and Desired Improvements:
- Neutral Perception: Most brands are perceived neutrally, indicating a lack of strong emotional connection or differentiation.

**Desired Improvements:**
- Reduce Sugar Content: There is a strong consumer demand for healthier options with less sugar.
- More Natural Ingredients: A preference for natural ingredients reflects a trend towards clean labeling and transparency.
- Wider Range of Flavors: Consumers desire more flavor variety to cater to diverse tastes.
- Interest in Natural or Organic Products: 50% of respondents are interested in natural or organic products, indicating a significant market segment that values health and sustainability in their beverage choices.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Recommendation  
To improve Codex's sales based on the survey findings, the marketing team can implement the following recommendations:  
 
**1. Enhance Brand Perception**  
Strengthen Brand Identity: Develop a clear and compelling brand narrative that differentiates Codex from competitors. Emphasize unique selling points and the benefits of Codex products.  
Promote Transparency: Highlight the use of natural ingredients and any health benefits prominently in marketing materials. Build trust by being transparent about product formulations and sourcing.  


**2. Address Health Concerns**  
Reduce Sugar Content: Reformulate products to lower sugar content and market these changes as a commitment to healthier options.
Highlight Natural Ingredients: Emphasize natural ingredients and health benefits in product descriptions and advertising campaigns. Use clean labeling to appeal to health-conscious consumers.  


**3. Expand Product Range**  
Introduce New Flavors: Develop and launch a wider range of flavors to cater to diverse consumer preferences. Conduct market research to identify popular and emerging flavor trends.  
Offer Caffeine-Free Options: Provide alternatives to energy drinks with lower caffeine or caffeine-free options to appeal to consumers sensitive to stimulants.  


**4. Optimize Pricing and Distribution**  
Price Positioning: Ensure that pricing aligns with consumer expectations and perceived value. Consider offering promotions or discounts within the ₹50-₹99 price range to attract price-sensitive consumers.  
Improve Availability: Expand distribution channels to ensure products are available locally. Partner with retailers and explore online sales to increase accessibility.  


**5. Leverage Effective Marketing Channels**  
Digital Advertising: Continue to invest in online ads, focusing on targeted campaigns to reach specific consumer segments. Utilize social media, search engines, and websites for precise targeting.  
Content Marketing: Create engaging content that educates consumers about the benefits of Codex products, such as blog posts, videos, and social media updates.  


**6. Increase Engagement with Key Demographics**  
Targeted Campaigns for Tier 1 Cities: Focus marketing efforts on Tier 1 cities where there is higher awareness and engagement. Tailor messages to align with local trends and preferences.  
Educational Campaigns for Tier 2 Cities: Develop educational campaigns to raise awareness and interest in Codex standards and products in Tier 2 cities.  


**7. Enhance Customer Experience**   
Feedback Mechanisms: Implement channels for customers to provide feedback and suggestions. Use this information to continuously improve products and services.  
Loyalty Programs: Develop loyalty programs to reward repeat customers and encourage brand advocacy.  


**8. Focus on Key Consumption Situations**  
Sports and Exercise: Promote products that cater to sports and exercise needs, such as hydration and energy drinks, through partnerships with fitness influencers and events.  
Studying and Working: Market beverages that enhance focus and productivity to students and professionals, highlighting their benefits for improving cognitive performance.
By implementing these recommendations, Codex can better align its marketing strategies with consumer preferences, address key concerns, and enhance its overall market presence.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Dashboard 
- Check the dashboard here: https://mavenanalytics.io/project/18390
 


















