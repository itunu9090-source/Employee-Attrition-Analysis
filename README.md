# Employee-Attrition-Analysis
## Table of contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tool](#tool)
- [Data Cleaning/Preparation](#data-cleaning-preparation)
- [Explanatory Data Analysis](#explanatory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results-findings)
- [Limitation](#limitation)
- [Reference](#reference)

### Project Overview:
This data analysis aims to provide insights into the employee attrition. By analyzing various aspects of the attrition data, we seek to identify causes for attrition, make a data-driven recomendations, and acquire in depth knowledge of the attrition.
<img width="1206" height="699" alt="Screenshot (99)" src="https://github.com/user-attachments/assets/e7a9b00e-1c4b-4291-aaa2-abb56bd6b53d" />

### Data Source:
The primary dataset used forthis analysis is the "https://drive.google.com/file/d/1IMjJomyMETjFBJDybdzn7DObH4hxxmvq/view?usp=drive_link" containing detailed information about each employee attrition.

### Tool:
 - SQL: For data cleaning,transformation, and data analysis.

### Data Cleaning/ Preparation:
From the on set data preparation, i performed the following;
 1. Data loading
 2. Data type convertion

### Explanatory Data Analysis:
The Employee attrition data to answer the following questions, such as;
•	What is the overall attrition rate?
•	Which departments have the highest attrition?
•	Which job roles are most affected by attrition?
•	Does attrition vary by gender or marital status?
•	Are employees with low satisfaction more likely to leave?
•	What is the average tenure of employees who leave vs stay?
•	Does salary level influence attrition?
•	Are employees with more projects more likely to leave (burnout risk)?
•	Performance Vs Satisfaction
•	How does salary vary across departments and job roles?
•	Is there a gender pay gap?
•	Do higher salary grades correlate with lower attrition?
•	Are high-performing employees being paid competitively?
•	Training vs Attrition
•	Is compensation aligned with tenure and promotions?
•	Do employees with more projects perform better or worse?
•	Is there a link between working hours and performance?
•	Are promoted employees actually high performers?
•	Does training completion reduce attrition?
•	How many employees receive promotions?
•	promotion vs attrition
•	Age distribution vs attrition (using date_of_birth)
•	What are the top 5 drivers of attrition?

### Data Analysis:
``` SQL

SELECT 
        COUNT(*) AS Total_Employees,
        SUM ( CASE WHEN attrition = 1 THEN 1 ELSE 0 END) AS Employee_Left,
        ROUND(
        CAST(SUM(CASE WHEN attrition = 1 THEN 1 ELSE 0 END) AS FLOAT) / COUNT(*) * 100, 2) AS Attrition_Rate
FROM attrition
```
``` SQL
SELECT TOP 3
        department,
        COUNT(*) AS Total,
        SUM (CASE WHEN attrition = 1 THEN 1 ELSE 0 END) AS Employee_Count, --- The total employees were 200, Left_Employee were 27, and Attrition rate was 13.5.
        ROUND(
        CAST (SUM ( CASE WHEN attrition = 1 THEN 1 ELSE 0 END) AS FLOAT) / COUNT(*) * 100, 2) AS Attrition_Rate

FROM attrition
GROUP BY  department
ORDER BY Attrition_Rate DESC
```
``` SQL
SELECT 
        gender,
        COUNT(*) AS Total,
        SUM( CASE WHEN attrition = 1 THEN 1 ELSE 0 END) AS Left_Count
FROM attrition
GROUP BY gender
ORDER BY Left_Count DESC
```
``` SQL
SELECT
        attrition,
        ROUND (
        AVG(satisfaction_level) , 2) AS Avg_Satisfaction
FROM Attrition
GROUP BY attrition
ORDER BY Avg_Satisfaction
```
``` SQL
SELECT
       attrition,
       ROUND(
       AVG( CAST( salary_grade AS FLOAT)), 2) AS Avg_level
FROM Attrition
GROUP BY  attrition
ORDER BY Avg_level
```
``` SQL
SELECT
        last_performance_score,
        ROUND ( AVG(satisfaction_level), 2) AS Avg_Sat
FROM attrition
GROUP BY last_performance_score
ORDER BY  Avg_Sat DESC
```
``` SQL
SELECT 
        attrition,
        AVG(CAST (salary_grade AS INT)) AS Avg_Salarygrade 
FROM attrition
GROUP BY attrition
ORDER BY Avg_Salarygrade DESC
```
``` SQL
      num_projects,
     ROUND( AVG(last_performance_score), 2) Performance_Level
FROM Attrition
GROUP BY num_projects
ORDER BY num_projects DESC
```
``` SQL
SELECT
     has_training_completed,
     SUM(CASE WHEN attrition = 1 THEN 1 ELSE 0 END) AS attrition 
FROM attrition
GROUP BY has_training_completed
ORDER BY attrition  DESC
```
``` SQL
Select 
      department,
      num_promotions,
      has_training_completed,
      salary,
     ROUND( AVG(satisfaction_level),1) AS Satistaction,
     SUM( CASE WHEN attrition = 1 THEN 1 ELSE 0 END )AS Left_Count
from attrition
group by  department, num_promotions, has_training_completed, salary
ORDER BY Left_Count DESC
```
### Results/ Findings:
The analysis outcomes are summarized as following 
•	The total employees were 200, Left_Employee were 27, and Attrition rate was 13.5
•	Logisitics Department have the hightest numbers of Attrition, Followed by Administration,and Quality.
•	Warehouse,logistics are most affected
•	Attrition vary by gender cos Male attrition more than female, and male divorcee left the most.
•	Employees with low satisfaction are more likely to leave.
•	Employees who leave have a shorter tenure on average than those who stay.
•	Employees with lower salary grades are more likely to leave than those with higher salary grades.
•	No, they aint likely to leave i.e number of project does not increase attrition.
•	Number of Performance and Satisfaction have a positive relationship.
•	Director of engineering and Marketing have the highest avg salary.
•	there is a gender pay gap because people who makes their gender confidential earns more.
•	High-performing employees being paid competitively.
•	People that have Completed training had more attrition.
•	Employees with more projects perform better. And
   Top 5 drivers of attrition are: Department, Num_Promotions, Training_completed, salary.
### Recomendations:
### Limitation:
### Reference:
 1. Sql analysis by Baara
