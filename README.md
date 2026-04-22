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
 - What is the overall attrition rate?
 - Which departments have the highest attrition?
 - Which job roles are most affected by attrition?
 - Does attrition vary by gender or marital status?
 - Are employees with low satisfaction more likely to leave?
 - What is the average tenure of employees who leave vs stay?
 -	Does salary level influence attrition?
 -	Are employees with more projects more likely to leave (burnout risk)?
 -	Performance Vs Satisfaction
 -	How does salary vary across departments and job roles?
 -	Is there a gender pay gap?
 -	Do higher salary grades correlate with lower attrition?
 -	Are high-performing employees being paid competitively?
 -	Training vs AttritioN
 -	Is compensation aligned with tenure and promotions?
 -	Do employees with more projects perform better or worse?
 -	Is there a link between working hours and performance?
 -	Are promoted employees actually high performers?
 -	Does training completion reduce attrition?
 -	How many employees receive promotions?
 -	promotion vs attrition
 -	Age distribution vs attrition (using date_of_birth)
 -	What are the top 5 drivers of attrition?

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
 - The total employees were 200, Left_Employee were 27, and Attrition rate was 13.5
 - Logisitics Department have the hightest numbers of Attrition, Followed by Administration,and Quality.
 - Warehouse,logistics are most affected
 - Attrition vary by gender cos Male attrition more than female, and male divorcee left the most.
 - Employees with low satisfaction are more likely to leave.
 - Employees who leave have a shorter tenure on average than those who stay.
	- Employees with lower salary grades are more likely to leave than those with higher salary grades.
	- No, they aint likely to leave i.e number of project does not increase attrition.
	- Number of Performance and Satisfaction have a positive relationship.
	- Director of engineering and Marketing have the highest avg salary.
	- There is a gender pay gap because people who makes their gender confidential earns more.
	- High-performing employees being paid competitively.
	- People that have Completed training had more attrition.
 - Employees with more projects perform better. And
 - Top 5 drivers of attrition are: Department, Num_Promotions, Training_completed, salary.

### Recomendations:
 1. Compensation Strategy Optimization
 Look first at what people earn now. Where gaps show up - especially roles tough to fill - adjust wages so folks stay. Extra money now and then keeps important workers around. Fairness between male and female pay matters a lot. Unequal treatment fades when balances are set right. Trust grows quietly when fairness leads. Legal trouble often avoids teams that act early.

2. Workload Balancing Burnout Control
Most days do not need top speed. Slowing down opens space for regular progress instead of collapse. Structure shapes what happens next, especially when pressure builds. Even splits across tasks keep thinking clear much later than sprints ever could. Notice how calm patterns outlast frantic bursts nearly every time.

3. Higher Engagement and Satisfaction
Somebody has to take responsibility when teams lose spark. When leaders speak plainly, trust grows - just like it does during tough moments when they stay close instead of vanishing. Cash alone won’t fix silence; better options appear through clear next steps, recognition that fits the effort, room to grow sideways into unfamiliar work.

4. Promotion and Career Growth Strategy
Parked at the start, each role maps what comes after. Workers spot their follow-up move before they need it. Progress stays visible - no secrets, just clarity. If interest shifts, paths unfold within rather than outside. Shifting roles feels routine, almost natural. Just because you stay, does not mean you stop moving. Moving between teams brings new energy. Learning changes shape when roles change too. Different work wakes up curiosity once more. Progress twists like a river, yet always keeps going.

5. Performance Management Adjustment
What if progress looked different? Pay attention to what tasks actually do, instead of counting hours spent. When changes lead somewhere meaningful, people notice. Effort finds purpose once it connects to impact. Value sticks around when it comes from something real.

6. Integrated Retention Actions
Now comes the moment when fairer pay must walk hand in hand with roles reshaped around their real needs. Progress shows up clearer when learning unfolds step by step, woven together with moments that spark belonging. Speed counts - waiting too long risks quiet exits. Action taken early shapes what happens next. Before balance tips, presence makes the difference.

### Limitations:
1. Data Quality Dependency

2. How good a manager is makes a difference. The mood of the office space adds its own weight. Hiring patterns beyond the company walls pull things one way or another

3. Simplified Metrics

Most days, moods, performance, even effort - these often collapse into a solitary figure. But real behavior weaves through countless shades, far too tangled for any lone score to capture.

4. Potential Misclassification

Out of work? Reasons differ, but true cause rarely fits a box. Upward moves become mere digits - equal on paper, unequal in life. Appearances shift when you look close. Hidden layers sit beneath what seems obvious.

### Conclusion

Heavy workloads hit harder when wages seem small. When promotions stop coming, morale takes a drop. As bonuses get smaller, so does motivation. Without knowing what comes next, effort grinds down.

Right from week one, set a steady pace so everyone finds their footing. Pay well - yet balance workloads to keep energy steady. Progress becomes real when steps ahead are visible, not just mentioned. The lasting things take root at the beginning, then grow stronger with regular care.

Most of what makes sense today comes from looking back; predictions may help clarify next steps. Today tells the story so far, yet tomorrow holds clues about direction. Patterns often appear before they explode - catching them early allows faster changes. Not merely checking results, but noticing shifts ahead alters how ideas take shape. Knowing adjusts responses; expecting steers design.

### Reference:
 1. Sql analysis by Baara
