# **🎯 OTT Media Pre-Merger Analytics using SQL**



## **1. About Overview**

This project analyzes the performance, subscriber behavior, content consumption, user engagement, subscription changes, and revenue trends of LioCinema and Jotstar between January and November 2024.



The objective is to support merger planning by identifying platform strengths, user behavior patterns, monetization opportunities, and strategic growth areas.

## 

## **2. Project Domain**

Media and Entertainment-OTT Media Analytics | Subscriber Analytics | Revenue Analytics



## **3. Dataset Information**

LioCinema and Jotstar Database: This database contains detailed data on content, subscribers, and content consumption for the both OTT platform, enabling insights into content, user behavior, and platform performance trends.



**1. contents:**

Purpose: This table provides detailed information about the content available on the OTT platform, enabling analysis of content diversity, genre popularity, and runtime patterns.

* content\_id
* content\_type
* language
* genre
* run\_time



**2. subscribers:**

Purpose: This table captures demographic and subscription details for OTT users, enabling insights into subscriber acquisition, upgrades, downgrades, and inactivity patterns.

* user\_id
* age\_group
* city\_tier
* subscription\_date
* subscription\_plan
* last\_active\_date
* plan\_change\_date
* new\_subscription\_plan



**3. content\_consumption:**

Purpose: This table captures user-level content consumption data, enabling analysis of total watch time, device preferences, and engagement trends.

* user\_id
* device\_type
* total\_watch\_time (mins)



## **4. Business Requirements**



The management team requires a detailed analysis of both OTT Platform to support merger planning and strategic decision-making.



### **Key Objectives:**



#### **1. Content Library Analysis**
* Compare the total content available on both platforms.
* Analyze content distribution by language and content type.



#### **2. Subscriber Insights**

* Analyze user growth trends from January–November 2024.
* Study subscriber demographics by age group, city tier, and subscription plan.



#### **3. Inactivity Analysis**

* Measure active vs. inactive user percentages.
* Identify inactivity patterns across age groups, city tiers, and subscription plans.
* Examine the relationship between watch time and user inactivity.



#### **4. Content Consumption Analysis**

* Compare average watch time across platforms
* Analyze viewing behavior by city tier, device type, and demographics.



#### **5. Upgrade Pattern Analysis**

* Identify the most common subscription upgrade paths.
* Compare upgrade behavior between platforms and user segments.



#### **6. Downgrade Pattern Analysis**

* Analyze downgrade trends and their frequency.
* Compare downgrade behavior between LioCinema and Jotstar.



#### **7. Paid User Distribution**

* Evaluate the proportion of paid subscribers across plans.
* Compare premium user adoption across Tier 1, Tier 2, and Tier 3 cities.



#### **8. Revenue Analysis**

* Calculate total revenue generated from subscriptions during January–November 2024.
* Compare revenue contribution by platform and subscription plan.



## **5. Business Metrics**

  1. Total content items
  2. Total users
  3. Paid users
  4. Paid users %
  5. Active users
  6. Inactive users
  7. Inactive Rate (%)
  8. Active Rate (%)
  9. Upgraded users
  10. Upgrade Rate (%)
  11. Downgraded users
  12. Downgrade Rate (%)
  13. Total watch time (hrs)
  14. Average watch time (hrs)
  15. Monthly users Growth Rate (%)
  16. Upgrade/Downgrade Rate (%)



## **6. Analysis Process**



**1. Data Collection:** Import datasets into MySQL

**2. Data Processing:**

   * Data validation
   * Duplicate checks
   * Data profiling
   * Relationship verification
     
**3. Exploratory Data Analysis (EDA)-SQL Analysis:**

   * Joins
   * Aggregations
   * Window Functions
   * CTEs
   * Subqueries
   * Conditional Logic

**4. Business Insight Generation**





## **7. Key Business Questions \& Data-Driven Insights with SQL Script**



### **Q1. Total Users \& Growth Trends-What is the total number of users for LioCinema and Jotstar?**



#### **SQL Script Jotstar:**
##### select COUNT(DISTINCT user\_id)

from jotstar\_db.content\_consumption;


#### **SQL Script LioCinema:**
##### select COUNT(DISTINCT user\_id)

from liocinema\_db.content\_consumption;

#### Data Driven Insights:👥 1. LioCinema Leads in User Acquisition

* User analysis revealed a significant difference in platform scale.
* Key Metrics:
  1. LioCinema Users → 183,446
  2. Jotstar Users → 44,620
* LioCinema acquired over four times more users than Jotstar during the analysis period.

👉 **Business Insight:** LioCinema has built a much larger customer base, creating a strong foundation for future growth and merger expansion.

### 

### **Q2. Content Library Comparison-What is the total number of contents available on LioCinema vs. Jotstar? How do they differ in terms of language and content type?**

#### **SQL Script Jotstar:**
SELECT
&#x20;   COUNT(DISTINCT content\_id) AS unique\_content\_ids,

&#x20;   COUNT(DISTINCT content\_type) AS unique\_content\_types,

&#x20;   COUNT(DISTINCT language) AS unique\_languages
FROM jotstar\_db.contents;

#### **SQL Script LioCinema:**
SELECT

&#x20;   COUNT(DISTINCT content\_id) AS unique\_content\_ids,

&#x20;   COUNT(DISTINCT content\_type) AS unique\_content\_types,

&#x20;   COUNT(DISTINCT language) AS unique\_languages
FROM liocinema\_db.contents;

#### Data Driven Insights: 🎬 2. Jotstar Built a Stronger Content Ecosystem
* Content library analysis revealed that Jotstar offers significantly broader content coverage.
* Key Metrics:
  1. Jotstar Content → 2,360
  2. LioCinema Content → 1,250
* Language Coverage:
  1. Jotstar → 10 Languages
  2. LioCinema → 7 Languages
* Jotstar also supports additional regional languages, increasing market reach.

👉 **Business Insight:** Jotstar contributes content depth and regional diversity, while LioCinema contributes audience scale

### **Q3. User Demographics-What is the distribution of users by age group, city tier, and subscription plan for each platform?**
**(Multiple Experiments while extracting data from available datasets)**

#### 
#### **SQL Script Jotstar:**

##### **1) Work on AGE GROUP:**
SELECT 

&#x20;   age\_group,

&#x20;   COUNT(DISTINCT user\_id) AS total\_user,

&#x20;   ROUND(COUNT(DISTINCT user\_id)\*100/

&#x20;   (SELECT COUNT(DISTINCT user\_id) 

&#x20;   FROM jotstar\_db.subscribers),2) AS age\_group\_user\_percentage
FROM jotstar\_db.subscribers
GROUP BY age\_group;

##### **2)Work on City Tier:**
SELECT 
&#x20;   city\_tier,

&#x20;   COUNT(DISTINCT user\_id) AS total\_user\_city\_tier,

&#x20;   ROUND(COUNT(DISTINCT user\_id)\*100/

&#x20;   (SELECT COUNT(DISTINCT user\_id) 

&#x20;   FROM jotstar\_db.subscribers),2) AS city\_tier\_user\_percentage
FROM jotstar\_db.subscribers
GROUP BY city\_tier;


##### **3)Work Subscription Plan:**
SELECT 
&#x20;   subscription\_plan,
&#x20;   COUNT(DISTINCT user\_id) AS total\_user\_subscription\_plan,
&#x20;   ROUND(COUNT(DISTINCT user\_id)\*100/
&#x20;   (SELECT COUNT(DISTINCT user\_id) 
&#x20;   FROM jotstar\_db.subscribers),2) AS subscription\_plan\_user\_percentage
FROM jotstar\_db.subscribers
GROUP BY subscription\_plan;


#### **SQL Script LioCinema:**
##### **1) Work on AGE GROUP:**

SELECT 
&#x20;   age\_group,
&#x20;   COUNT(DISTINCT user\_id) AS total\_user,
&#x20;   ROUND(COUNT(DISTINCT user\_id)\*100/
&#x20;   (SELECT COUNT(DISTINCT user\_id) 
&#x20;   FROM liocinema\_db.subscribers),2) AS age\_group\_user\_percentage
FROM liocinema\_db.subscribers
GROUP BY age\_group;

##### 

##### **2)Work on City Tier:**

SELECT 
&#x20;   city\_tier,
&#x20;   COUNT(DISTINCT user\_id) AS total\_user\_city\_tier,
&#x20;   ROUND(COUNT(DISTINCT user\_id)\*100/
&#x20;   (SELECT COUNT(DISTINCT user\_id) 
&#x20;   FROM liocinema\_db.subscribers),2) AS city\_tier\_user\_percentage
FROM liocinema\_db.subscribers
GROUP BY city\_tier;

##### 

##### **3)Work Subscription Plan:**

SELECT 
&#x20;   subscription\_plan,
&#x20;   COUNT(DISTINCT user\_id) AS total\_user\_subscription\_plan,
&#x20;   ROUND(COUNT(DISTINCT user\_id)\*100/
&#x20;   (SELECT COUNT(DISTINCT user\_id) 
&#x20;   FROM liocinema\_db.subscribers),2) AS subscription\_plan\_user\_percentage
FROM liocinema\_db.subscribers
GROUP BY subscription\_plan;



### **Data Driven Insights:
👨‍👩‍👧 3. Both Platforms Attract Different Customer Segments.

* Subscriber demographics showed clear differences in audience composition.
* Jotstar: Largest Age Group → 25–34 Years (45%)
* LioCinema: Largest Age Group → 18–24 Years (43.5%)
* Both platforms appeal to different customer segments.

👉 **Business Insight:** The merger creates access to both younger and mature audience groups, improving market coverage.

### 

### **Q4. Active vs. Inactive Users-What %age of LioCinema and Jotstar users are active vs. inactive? How do these rates vary by age group and subscription plan?**

#### **SQL Script Jotstar:**
##### **(1) Active vs. Inactive Users (Overall)**
SELECT
COUNT(DISTINCT user\_id),
COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END) AS active\_users,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END) AS inactive\_users,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END)\*100.0 / COUNT(DISTINCT user\_id), 2) AS active\_pct
FROM jotstar\_db.subscribers;

##### **(2) Rates vary by age group**
SELECT
age\_group,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END) AS active\_users,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END) AS inactive\_users,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END)\*100.0/COUNT(DISTINCT user\_id),2) AS active\_pct,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END)\*100.0/COUNT(DISTINCT user\_id),2) AS inactive\_pct
FROM jotstar\_db.subscribers
GROUP BY age\_group
ORDER BY age\_group;

##### **(3) Rates vary by subscription plan**
SELECT
subscription\_plan,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END) AS active\_users,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END) AS inactive\_users,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END)\*100.0/COUNT(DISTINCT user\_id),2) AS active\_pct,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END)\*100.0 /COUNT(DISTINCT user\_id),2) AS inactive\_pct
FROM jotstar\_db.subscribers
GROUP BY subscription\_plan
ORDER BY subscription\_plan;

#### 
#### **SQL Script LioCinema:**

##### **(1) Active vs. Inactive Users (Overall)**
SELECT
COUNT(DISTINCT user\_id),
COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END) AS active\_users,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END) AS inactive\_users,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id 
END) \* 100.0 / COUNT(DISTINCT user\_id), 2) AS active\_pct
FROM liocinema\_db.subscribers;


##### **(2) Rates vary by age group**
SELECT
age\_group,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END) AS active\_users,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END) AS inactive\_users,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END)\*100.0/COUNT(DISTINCT user\_id),2) AS active\_pct,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END)\* 100.0/COUNT(DISTINCT user\_id),2) AS inactive\_pct
FROM liocinema\_db.subscribers
GROUP BY age\_group
ORDER BY age\_group;



##### **(3) Rates vary by subscription plan:**

SELECT
subscription\_plan,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END) AS active\_users,
COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END) AS inactive\_users,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NULL THEN user\_id END)\*100.0/COUNT(DISTINCT user\_id), 2) AS active\_pct,
ROUND(COUNT(DISTINCT CASE WHEN last\_active\_date IS NOT NULL THEN user\_id END)\* 100.0/COUNT(DISTINCT user\_id), 2)AS inactive\_pct
FROM liocinema\_db.subscribers
GROUP BY subscription\_plan
ORDER BY subscription\_plan;


### **Data Driven Insights:
📈 4. Jotstar Demonstrates Stronger User Engagement

* User activity analysis revealed higher engagement levels on Jotstar.
* Key Metrics:
  1. Jotstar Active Users → \~85%
  2. LioCinema Active Users → \~55%
* Across all age groups and subscription plans, Jotstar consistently maintained higher activity levels.

👉 **Business Insight:** Jotstar users are significantly more engaged and less likely to become inactive.

### **Q5. Watch Time Analysis-What is the average watch time for LioCinema vs. Jotstar during the analysis period? How do these compare by city tier and device type?**

#### 
#### **SQL Script Jotstar:**
##### **(1) Overall Average Watchtime**
SELECT 
ROUND(AVG(total\_watch\_time\_mins),2) AS avg\_watch\_time,
ROUND(AVG(total\_watch\_time\_mins)/60,2) AS avg\_watch\_time\_Hours
FROM jotstar\_db.content\_consumption;

##### **(2)** **Average Watchtime by Device Type**
SELECT 
device\_type,
ROUND(AVG(total\_watch\_time\_mins),2) AS avg\_watch\_time,
ROUND(AVG(total\_watch\_time\_mins)/60,2) AS avg\_watch\_time\_Hours
FROM jotstar\_db.content\_consumption
GROUP BY device\_type;

##### **(3)** **Average Watchtime by City Tier**
SELECT 
s.city\_tier,
ROUND(AVG(total\_watch\_time\_mins),2) AS avg\_watch\_time,
ROUND(AVG(total\_watch\_time\_mins)/60,2) AS avg\_watch\_time\_Hours
FROM jotstar\_db.content\_consumption c
JOIN jotstar\_db.subscribers s
ON s.user\_id=c.user\_id
GROUP BY city\_tier;

#### **SQL Script LioCinema:**
##### **(1) Overall Average Watchtime**
SELECT
ROUND(AVG(total\_watch\_time\_mins),2) AS avg\_watch\_time,
ROUND(AVG(total\_watch\_time\_mins)/60,2) AS avg\_watch\_time\_Hours
FROM liocinema\_db.content\_consumption;

##### **(2)** **Average Watchtime by Device Type**
SELECT
device\_type,
ROUND(AVG(total\_watch\_time\_mins),2) AS avg\_watch\_time,
ROUND(AVG(total\_watch\_time\_mins)/60,2) AS avg\_watch\_time\_Hours
FROM liocinema\_db.content\_consumption
GROUP BY device\_type;

##### **(3)** **Average Watchtime by City Tier**
SELECT
s.city\_tier,
ROUND(AVG(total\_watch\_time\_mins),2) AS avg\_watch\_time,
ROUND(AVG(total\_watch\_time\_mins)/60,2) AS avg\_watch\_time\_Hours
FROM liocinema\_db.content\_consumption c
JOIN liocinema\_db.subscribers s
ON s.user\_id=c.user\_id
GROUP BY city\_tier;


### **Data Driven Insights:
📺 5. Jotstar Users Consume More Content

* Watch time analysis showed substantial differences in content consumption.
* Average Watch Time:
  1. Jotstar → 117.24 Hours
  2. LioCinema → 26.61 Hours
* Across both platforms:
  1. Mobile users recorded the highest watch time.
  2. Tier 1 cities showed the strongest engagement.

👉 **Business Insight:** Jotstar successfully drives deeper content engagement and platform stickiness.

### **Q6. Inactivity Correlation-How do inactivity patterns correlate with total watch time or average watch time? Are less engaged users more likely to become inactive?**

#### **SQL Script Jotstar:**
SELECT 
&#x20;   COUNT(\*) AS total\_users,
&#x20;   ROUND(AVG(total\_watch\_time\_mins) / 60, 2) AS avg\_watch\_time\_hours,
&#x20;   SUM(CASE WHEN last\_active\_date IS NULL THEN 1 ELSE 0 END) AS active\_users,
&#x20;   SUM(CASE WHEN last\_active\_date IS NOT NULL THEN 1 ELSE 0 END) AS inactive\_users
FROM (SELECT s.user\_id,
&#x20;     SUM(c.total\_watch\_time\_mins) AS total\_watch\_time\_mins, s.last\_active\_date
&#x20;   FROM jotstar\_db.content\_consumption c 
&#x20;   JOIN jotstar\_db.subscribers s
&#x20;       ON c.user\_id = s.user\_id
&#x20;   GROUP BY s.user\_id, s.last\_active\_date) t;



###### **(\*)Correlation** 
SELECT
&#x20; ROUND((AVG(total\_watch\_time\_mins \* inactivity\_flag)-AVG(total\_watch\_time\_mins)\*AVG(inactivity\_flag))/
&#x20;     (STDDEV(total\_watch\_time\_mins) \* STDDEV(inactivity\_flag)),2) AS correlation\_value
FROM(SELECT s.user\_id,
&#x20;    SUM(c.total\_watch\_time\_mins) AS total\_watch\_time\_mins,
&#x20;     CASE 
&#x20;         WHEN s.last\_active\_date IS NOT NULL THEN 1 ELSE 0 
&#x20;     END AS inactivity\_flag
&#x20;   FROM jotstar\_db.content\_consumption c 
&#x20;   JOIN jotstar\_db.subscribers s
&#x20;       ON c.user\_id = s.user\_id
&#x20;   GROUP BY s.user\_id, s.last\_active\_date) t;



#### **SQL Script LioCinema:**
SELECT 
&#x20;   COUNT(\*) AS total\_users,
&#x20;   ROUND(AVG(total\_watch\_time\_mins) / 60, 2) AS avg\_watch\_time\_hours,
&#x20;   SUM(CASE WHEN last\_active\_date IS NULL THEN 1 ELSE 0 END) AS active\_users,
&#x20;   SUM(CASE WHEN last\_active\_date IS NOT NULL THEN 1 ELSE 0 END) AS inactive\_users
FROM (SELECT s.user\_id,
&#x20;     SUM(c.total\_watch\_time\_mins) AS total\_watch\_time\_mins, s.last\_active\_date
&#x20;   FROM liocinema\_db.content\_consumption c 
&#x20;   JOIN liocinema\_db.subscribers s
&#x20;   ON c.user\_id = s.user\_id
&#x20;   GROUP BY s.user\_id, s.last\_active\_date) t;



###### **(\*)Correlation**
SELECT 
&#x20; ROUND((AVG(total\_watch\_time\_mins \* inactivity\_flag)-AVG(total\_watch\_time\_mins) \* AVG(inactivity\_flag))/
&#x20; (STDDEV(total\_watch\_time\_mins) \* STDDEV(inactivity\_flag)),2) AS correlation\_value FROM(SELECT s.user\_id,
&#x20;     SUM(c.total\_watch\_time\_mins) AS total\_watch\_time\_mins,
&#x20;     CASE 
&#x20;     WHEN s.last\_active\_date IS NOT NULL THEN 1 ELSE 0 
&#x20;     END AS inactivity\_flag
&#x20;     FROM liocinema\_db.content\_consumption c 
&#x20;     JOIN liocinema\_db.subscribers s
&#x20;     ON c.user\_id = s.user\_id
&#x20;     GROUP BY s.user\_id, s.last\_active\_date) t;

### **Data Driven Insights
:🔄 6. Low Engagement Increases Churn Risk

* Correlation analysis examined the relationship between watch time and inactivity.
* Results:showing a moderate inverse relationship
  1. Jotstar Correlation → -0.39
  2. LioCinema Correlation → -0.45
* The relationship is meaningful but not definitive, indicating other factors also play a role.
* Higher watch time was associated with lower inactivity on both platforms.
* Low engagement is a good indicator of possible churn, but not the only reason, Other factors like content type, genre, and subscription plan also affect inactivity
👉 **Business Insight:** Watch time can serve as an early indicator of potential customer churn.

### 

### **Q7. Downgrade Trends-How do downgrade trends differ between LioCinema and Jotstar? Are downgrades more prevalent on one platform compared to the other?** 

#### **SQL Script Jotstar:**
SELECT
&#x20;   subscription\_plan AS from\_plan,
&#x20;   new\_subscription\_plan AS to\_plan,
&#x20;   COUNT(DISTINCT user\_id) AS downgrade\_users FROM jotstar\_db.subscribers
WHERE plan\_change\_date IS NOT NULL
&#x20;   AND (&#x20(subscription\_plan = 'VIP' AND new\_subscription\_plan IN ('Premium','Free'))
&#x20;       OR (subscription\_plan = 'Premium' AND new\_subscription\_plan = 'Free') &#x20;   )
GROUP BY
&#x20;   subscription\_plan,
&#x20;   new\_subscription\_plan
ORDER BY
&#x20;   downgrade\_users DESC**;**

#### 

#### **SQL Script LioCinema:**
SELECT
&#x20;   subscription\_plan AS from\_plan,
&#x20;   new\_subscription\_plan AS to\_plan,
&#x20;   COUNT(DISTINCT user\_id) AS downgrade\_users
FROM liocinema\_db.subscribers
WHERE plan\_change\_date IS NOT NULL
&#x20;   AND (
&#x20;       (subscription\_plan = 'Premium' AND new\_subscription\_plan = 'Basic')
&#x20;       OR (subscription\_plan = 'Premium' AND new\_subscription\_plan = 'Free')
&#x20;       OR (subscription\_plan = 'Basic' AND new\_subscription\_plan = 'Free')
&#x20;   )
GROUP BY
&#x20;   subscription\_plan,
&#x20;   new\_subscription\_plan
ORDER BY
&#x20;   downgrade\_users DESC;


### **Data Driven Insights:
📉 7. LioCinema Faces Higher Downgrade Pressure

* Subscription analysis revealed significant differences in downgrade behavior.
* LioCinema:
  1. Premium → Free = 7,439 Users
  2. Basic → Free = 10,309 Users
* Jotstar:
  1. VIP → Premium = 2,821 Users
  2. VIP → Free = 2,149 Users

**👉 Business Insight:** LioCinema faces stronger pressure in retaining paid subscribers, indicating potential pricing or value perception challenges.

### 

### **Q8. Upgrade Patterns-What are the most common upgrade transitions (e.g., Free to Basic, Free to VIP, Free to Premium)for LioCinema and Jotstar? How do these differ across platforms?**



#### **SQL Script Jotstar:**
SELECT
&#x20;   subscription\_plan AS from\_plan,
&#x20;   new\_subscription\_plan AS to\_plan,
&#x20;   COUNT(DISTINCT user\_id) AS users\_upgraded,
&#x20;   ROUND(
&#x20;       COUNT(DISTINCT user\_id) \* 100.0 /
&#x20;       SUM(COUNT(DISTINCT user\_id)) OVER (),
&#x20;       2
&#x20;   ) AS upgrade\_percentage
FROM jotstar\_db.subscribers
WHERE plan\_change\_date IS NOT NULL
&#x20;   AND (
&#x20;       (subscription\_plan = 'Free' AND new\_subscription\_plan IN ('VIP','Premium'))
&#x20;       OR
&#x20;       (subscription\_plan = 'VIP' AND new\_subscription\_plan = 'Premium')
&#x20;   )
GROUP BY
&#x20;   subscription\_plan,
&#x20;   new\_subscription\_plan
ORDER BY users\_upgraded DESC;

#### **SQL Script LioCinema:**
SELECT
&#x20;   subscription\_plan AS from\_plan,
&#x20;   new\_subscription\_plan AS to\_plan,
&#x20;   COUNT(DISTINCT user\_id) AS users\_upgraded,
&#x20;   ROUND(
&#x20;       COUNT(DISTINCT user\_id) \* 100.0 /
&#x20;       SUM(COUNT(DISTINCT user\_id)) OVER (),
&#x20;       2
&#x20;   ) AS upgrade\_percentage
FROM liocinema\_db.subscribers
WHERE plan\_change\_date IS NOT NULL
&#x20;   AND (
&#x20;       (subscription\_plan = 'Free' AND new\_subscription\_plan IN ('Basic','Premium'))
&#x20;       OR
&#x20;       (subscription\_plan = 'Basic' AND new\_subscription\_plan = 'Premium')
&#x20;   )
GROUP BY
&#x20;   subscription\_plan,
&#x20;   new\_subscription\_plan
ORDER BY users\_upgraded DESC;

### **Data Driven Insights:📈 
8. Jotstar Shows Strong Premium Adoption**
* Upgrade analysis highlighted differences in customer willingness to pay.
* Jotstar:
  1. Free → VIP = 844 Users
  2. Free → Premium = 683 Users
* LioCinema:
  1. Free → Basic = 2,078 Users
  2. Basic → Premium = 1,362 Users
* Jotstar users are more likely to move directly into premium tiers, while LioCinema users prefer gradual upgrades.

👉 **Business Insight:** Jotstar demonstrates stronger premium value perception among subscribers.

### 

### **Q9. Paid Users Distribution-How does the paid user% age (e.g., Basic, Premium for LioCinema; VIP, Premium for Jotstar) vary across different platforms? Analyse the proportion of premium users in Tier 1, Tier 2, and Tier 3 cities and identify any notable trends or differences.**

#### **SQL Script Jotstar:**
SELECT 
&#x20;   city\_tier,
&#x20;   COUNT(DISTINCT user\_id) AS total\_users,
&#x20;   COUNT(DISTINCT CASE 
&#x20;       WHEN subscription\_plan IN ('VIP','Premium') 
&#x20;       THEN user\_id 
&#x20;   END) AS paid\_users,
&#x20;   COUNT(DISTINCT CASE 
&#x20;       WHEN subscription\_plan = 'VIP' 
&#x20;       THEN user\_id 
&#x20;   END) AS vip\_users,
&#x20;   COUNT(DISTINCT CASE 
&#x20;       WHEN subscription\_plan = 'Premium' 
&#x20;       THEN user\_id 
&#x20;   END) AS premium\_users,
&#x20;   ROUND(
&#x20;       COUNT(DISTINCT CASE 
&#x20;           WHEN subscription\_plan IN ('VIP','Premium') 
&#x20;           THEN user\_id 
&#x20;       END) \* 100.0 / COUNT(DISTINCT user\_id), 2
&#x20;   ) AS paid\_user\_pct,
&#x20;   ROUND(
&#x20;       COUNT(DISTINCT CASE 
&#x20;           WHEN subscription\_plan = 'VIP' 
&#x20;           THEN user\_id 
&#x20;       END) \* 100.0 / COUNT(DISTINCT user\_id), 2
&#x20;   ) AS vip\_pct
FROM jotstar\_db.subscribers
GROUP BY city\_tier
ORDER BY city\_tier;


#### **SQL Script LioCinema:**

SELECT 
&#x20;   city\_tier,
&#x20;   COUNT(DISTINCT user\_id) AS total\_users,
&#x20;   COUNT(DISTINCT CASE 
&#x20;       WHEN subscription\_plan IN ('Basic','Premium') 
&#x20;       THEN user\_id 
&#x20;   END) AS paid\_users,
&#x20;   COUNT(DISTINCT CASE 
&#x20;       WHEN subscription\_plan = 'Premium' 
&#x20;       THEN user\_id 
&#x20;   END) AS premium\_users,
&#x20;   COUNT(DISTINCT CASE 
&#x20;       WHEN subscription\_plan = 'Basic' 
&#x20;       THEN user\_id 
&#x20;   END) AS basic\_users,
&#x20;   ROUND(
&#x20;       COUNT(DISTINCT CASE 
&#x20;           WHEN subscription\_plan IN ('Basic','Premium') 
&#x20;           THEN user\_id 
&#x20;       END) \* 100.0 / COUNT(DISTINCT user\_id), 2
&#x20;   ) AS paid\_user\_pct,
&#x20;   ROUND(
&#x20;       COUNT(DISTINCT CASE 
&#x20;           WHEN subscription\_plan = 'Premium' 
&#x20;           THEN user\_id 
&#x20;       END) \* 100.0 / COUNT(DISTINCT user\_id), 2
&#x20;   ) AS premium\_pct
FROM liocinema\_db.subscribers
GROUP BY city\_tier
ORDER BY city\_tier;

#### 
### **Data Driven Insights:
* 💳9. Jotstar Achieved Better Monetization
* Paid user analysis revealed stronger conversion performance for Jotstar.
* Paid User Percentage:
  1. Jotstar → 72.9%
  2. LioCinema → 42.8%
* Tier 1 cities consistently delivered the highest paid user penetration across both platforms.

👉 **Business Insight:** Jotstar converts free users into paying subscribers far more effectively.

### 

### **Q10. Revenue Analysis-Assume the following monthly subscription prices, calculate the total revenue generated by both platforms**

#### **SQL Script Jotstar:**
**-- STEP 1: Prepare base subscriber data and define effective end date***
WITH base\_data AS (
&#x20;   SELECT
&#x20;       user\_id,
&#x20;       subscription\_plan,
&#x20;       new\_subscription\_plan,
&#x20;       subscription\_date,
&#x20;       plan\_change\_date,
&#x20;       last\_active\_date,
&#x20;       CASE 
&#x20;           WHEN last\_active\_date IS NULL THEN '2024-11-30'
&#x20;           ELSE LEAST(last\_active\_date, '2024-11-30')
&#x20;       END AS effective\_end\_date
&#x20; FROM jotstar\_db.subscribers
&#x20; WHERE subscription\_date <= '2024-11-30'),

**-- STEP 2: Split subscription period into before and after plan change**
split\_periods AS (SELECT
&#x20;       user\_id,
&#x20;       subscription\_plan,
&#x20;       new\_subscription\_plan,

**-- Period before plan change or end date**
&#x20;   GREATEST(subscription\_date, '2024-01-01') AS start\_before,
&#x20;    LEAST(COALESCE(plan\_change\_date, effective\_end\_date), effective\_end\_date) AS end\_before,

**-- Period after plan change**
&#x20;   plan\_change\_date AS start\_after,
&#x20;   effective\_end\_date AS end\_after
FROM base\_data),

**-- STEP 3: Calculate duration (in months) spent in each plan**
revenue\_calc AS(SELECT user\_id,
&#x20;CASE 
&#x20;WHEN start\_before < end\_before
&#x20;THEN TIMESTAMPDIFF(MONTH, start\_before, end\_before) ELSE 0 
&#x20;END AS months\_before,
&#x20;
&#x20;CASE 
&#x20;WHEN start\_after IS NOT NULL 
&#x20;AND start\_after < end\_after
&#x20;THEN TIMESTAMPDIFF(MONTH, start\_after, end\_after) ELSE 0
&#x20;END AS months\_after,
&#x20; subscription\_plan,
&#x20; new\_subscription\_plan
&#x20; FROM split\_periods)

**-- STEP 4: Calculate total revenue**
SELECT
&#x20;   COUNT(DISTINCT user\_id) AS total\_subscribers,
&#x20;   ROUND((SUM(months\_before\*CASE subscription\_plan
&#x20;               WHEN 'VIP' THEN 159
&#x20;               WHEN 'Premium' THEN 359
&#x20;               ELSE 0
&#x20;               END) +
&#x20;           SUM(months\_after\*CASE new\_subscription\_plan
&#x20;               WHEN 'VIP' THEN 159
&#x20;               WHEN 'Premium' THEN 359
&#x20;               ELSE 0
&#x20;               END))/1000000,2) AS total\_revenue\_millions FROM revenue\_calc;

#### 

### **Data Driven Insights:
* 💰10. Jotstar Generates Higher Revenue Despite Smaller Scale
* Revenue analysis revealed a significant monetization advantage.
* Key Metrics:
  1. LioCinema Revenue → ₹16.12M
  2. Jotstar Revenue → ₹38.81M
* Combined Revenue:₹54.93M
* Although LioCinema has a much larger subscriber base, Jotstar generates more than twice the revenue.

👉 **Business Insight:** Jotstar's stronger monetization model compensates for its smaller audience size.


## **8.Business Recommendations**

### **📱 Improve Paid User Conversion**
* Target free users with personalized upgrade offers
* Introduce premium trial experiences
* Simplify subscription upgrade journeys

**Expected Impact:** Higher paid subscriber conversion and revenue growth.



### **🎬 Leverage Combined Content Strengths**
* Expand regional language content
* Cross-promote high-performing content libraries
* Improve content discoverability

**Expected Impact:** Higher engagement and subscriber retention.

### **🔄 Reduce User Inactivity**
* Identify low watch-time users early
* Launch re-engagement campaigns
* Improve personalized recommendations

**Expected Impact:** Lower churn and stronger user retention.

### **📈 Strengthen Premium Subscription Adoption**
* Create bundled subscription offerings
* Enhance premium plan value propositions
* Introduce loyalty benefits for long-term subscribers

**Expected Impact:** Improved monetization performance.

### **💰 Optimize Post-Merger Growth Strategy**
* Use LioCinema's scale for customer acquisition
* Use Jotstar's monetization strengths for revenue growth
* Build a unified subscriber experience

**Expected Impact**: Balanced growth across acquisition, engagement, and revenue.

## **9. Project Deliverables \& Resources**

#### **📊 Project Walkthrough Video**
https://github.com/user-attachments/assets/20c3bf94-e4d7-4a5d-9246-5d638340e457

#### **Contact**

Abhilasha- Data Analyst

📧 Email: connectspace.abhilasha@gmail.com

