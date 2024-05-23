
# Airline Passenger Satisfaction Prediction ✈️

## 🙇‍♂️ Problem description
The project aims to predict airline passenger satisfaction based on various factors such as flight distance, in-flight service, ease of online booking, and departure/arrival time convenience. Understanding the factors that contribute to passenger satisfaction is crucial for airlines to improve their services, enhance customer experience, and increase customer loyalty. By analyzing this dataset, we aim to provide valuable insights into what drives passenger satisfaction and how airlines can better meet customer expectations.


## 🗂️ Dataset
We used this publicly available dataset from kaggle which contains an airline passenger satisfaction survey.<br>
https://www.kaggle.com/datasets/teejmahal20/airline-passenger-satisfaction


## 🧱 Project pipeline
<img src="assets/pipeline.png" alt=" " >

**1. 🧹 Data Exploring & Cleaning**:
- Explore the features and the unique values for each.
- Explore dataset size:
o Training data: 103904 rows × 25 columns
o Test data: 25976 rows × 25 columns
- Remove nulls from training & test dataset.
- Check if there are duplicate rows
- Remove unnecessary columns:  ID, Unamed:0

**2. 🛰️ Exploratory Data Analysis**:<br>
  **2.1 Univariate Analysis**<br>
    2.1.1 Charts for categorical variables:<br>
      <img src="assets/univariate_pie_1.png" alt="" >
      <img src="assets/univariate_pie_2.png" alt="" >
      <img src="assets/univariate_pie_3.png" alt="" >
      <img src="assets/univariate_pie_4.png" alt="" >
      <img src="assets/univariate_pie_5.png" alt="" >
      <img src="assets/univariate_pie_6.png" alt="" >
      <img src="assets/univariate_pie_7.png" alt="" >

   **• Insights**:
      
     - There is an almost equal number of male and female participants in the survey.
      
     - Most of passengers are neutral or dissatisfied = 56.7% ==> we need to analysis the reasons and try to find business solutions to make them more satisfied
      
     - We have more loyal customer data (81.7%)
      
     - Most of travels are for Business travel (69%)
      
     - Very few people fly in the economy plus class. They usually prefer Economy or Business.<br>

 2.1.2 Histogram for numerical variables<br>
       <img src="assets/univariate_histograms_training.png" alt="" ><br>

   • **Insights**: <br>
   - Most of the delays are 0, which is a good indicator.<br>
   - The variables Flight Distance and Departure Delay and Arrival Delay are all heavily right-skewed.<br>

   Investigate problem of outliers:

      Portion of outliers in each column:
      
       Departure Delay in Minutes: 0.139831
       
       Arrival Delay in Minutes:   0.134699
       
       Flight Distance:            0.022049
         
         
- Since the portion of rows having the outliers in the "Flight Distance" is very small so we will remove it.<br>
- We will normalize "Departure Delay in Minutes","Arrival Delay in Minutes"<br>
<img src="assets/univariate_histograms_after_handling_outliers_training.png" alt="" ><br>

**2.2 Bivariate Analysis**<br>
2.2.1 Bar charts & Pie charts for categorical features<br>
<img src="assets/bivariate_bar.png" alt="" ><br>
Then we focused on plotting the distribution for satisfied & dissatisfied for each feature:<br>
<img src="assets/bivariate_pie.png" alt="" ><br>
2.2.2 Histograms for numerical columns
<img src="assets/bivariate_histograms.png" alt="" ><br>

Grouping to help in insights:<br>
<img src="assets/grouping.png" alt="" ><br>

• **Insights**: <br>
- Gender nearly doesn't affect satisfaction.<br>
- Loyal passengers have higher satisfaction percentages than Disloyal ones.<br>
- Satisfied Passengers usually go for Business travel.<br>
- Most people of Passengers going for Personal Travel are not satisfied.<br>
- Satisfied Passengers use Business Class while travelling.<br>
- Passengers using Eco travelling are the least Satisfied Passengers.<br>
- More than 80% of passengers flying in economy are either Neutral or Dissatisfied. That shows us that it needs some improvement.<br>
- Most Satisfied Passengers are in range [37-53] year & Most Unsatisfied are in range [7-36] year.<br>
- Satisfied Passengers have more long-distance flights than the dissatisfied.<br>
- The more the delay the less the satisfied passenger's portion.<br>
- The most frequency in the levels of satisfaction is 4 for all except: [Inflight Wi-Fi service, Ease of Online booking, Gate location] is 3<br>
- Rate 3 is the most frequent between unsatisfied passengers in services <br>
- Rate 4 is the most frequent between satisfied passengers in services <br>
- The ratings are almost evenly distributed between 1 and 5. With that in mind, the positive thing is that there are more positive or neutral ratings (3 through 5) than negative ones (0 through 2).<br>
- Our passengers have mixed opinions about the Departure and Arrival Time Convenience. We concluded that there is not that much correlation between total Satisfaction and Departure and Arrival Time Convenience.<br>

2.2.3 Correlation between satisfaction and other columns<br>
<img src="assets/bivariate_correlation.png" alt="" ><br>
**Insights**:<br>
Positively Correlated: - Business Class ,online boarding, inflight entertainment, seat comfort, on-board service, Legroom service, cleanliness, Flight distance, and Business travels are strong reasons for people satisfaction.<br>
Negatively Correlated: - Personal Travels, Economy Class, Eco plus Class or being Disloyal Customer results in Unsatisfaction.<br>

**2.3 Multivariate Analysis**<br>
<img src="assets/multivariate_correlation.png" alt="" ><br>
**Insights**:<br>
- Departure Delay is highly correlated with Arrival Delay. [Will deal with this in feature engineering].<br>
- Inflight WiFi service and Ease of online booking are + correlated.<br>
- Inflight entertainment, Food and Drink, Seat comfort and cleanliness are + correlated.<br>
- Baggage handling is + correlated with Inflight service.<br>

<img src="assets/arrival_departure_correlation.png" alt="" ><br>

• **Insights**:<br>
- There is a strong correlation between the two columns we can drop one of the two columns and as Arrival Delay in Minutes column has some null, we can drop it.<br>
- Remove quintile columns ['Age_quintile', 'Flight Distance_quintile', 'Arrival Delay in Minutes_quintile', 'Departure Delay in Minutes_quintile']<br>


**2.4 Clustring:**<br>
Applying Kmeans on the data with 3 clusters<br>
<img src="assets/cluster_distribution.png"><br>
The portion of each class:<br>
<ol>
 <li>Class 1 ==> 0.630900</li>
 <li>Class 0 ==> 0.219453</li>
 <li>Class 2 ==> 0.149648</li>
</ol>

• Most of the data (63%) is in one cluster (cluster 1) <br>
• Showing aggregates of each numeric column grouped by the cluster.<br>

<img src="assets/clusters_data.png"><br>

• **Insights**:<br>
− All age values are in the 3 clusters [7-85]<br>
− Flight Distances is distributed on all clusters without intersection between them:<br>
− Cluster 1 contains flight distance in the range [1137:2418]<br>
− Cluster 0 contains flight distance in the range [31:1136]<br>
− Cluster 2 contains flight distance in the range [2419:4983]<br>
− Value 0 for seat comfort column is only in cluster 1<br>
− Value 0 for Checkin service column is only in cluster 1<br>
− Values in range [1017:1592] don't exist in class 0<br>
− Values in range [1305:1592] don't exist in class 2<br>

Show the cluster distribution over the categories of categorical features:<br>
<img src="assets/distribution_by_cluster.png"><br>

<img src="assets/quintile_distribution_by_cluster.png"><br>

• **Insights**:<br>
- Cluster 1 is the major class in all values in all columns.<br>
- Satisfied customers are distributed over all cluster.<br>
- Dissatisfied or neutral customers are distributed over all cluster.<br>
- Each gender is distributed over all clusters.<br>
- Loyal customer is distributed over all clusters.<br>
- Cluster 2 doesn't contain Disloyal customers.<br>
- The portion of customers with type of travel is personal in cluster 2 is very small.<br>
- All values of [Inflight WiFi service, departure arrival time convenient, Ease of online booking, Gate Location, Food and drink,<br>
- seat comfort, inflight entertainment, on-board service, Baggage handling, Checkin service, inflight service & cleanliness] are distributed over all clusters.<br>
- The portion of departure arrival time convenient with value 0 in cluster 2 is very small.<br>
- Cluster 2 doesn't contain customers of Eco plus class.<br>
- The portion of of customers of Eco class in cluster 2 is very small.<br>
- Cluster 2 doesn't contain values 0 of Online boarding.<br>
- Values 0 of Leg room service are all in cluster 1.<br>

**2.5 Association Rules** <br>
Applying Apriori algorithm with minimum support = 0.25 and minimum cardinality = 2<br><br>

•Top 10 rules sorted by support:<br><br>
<img src="assets/top_10_support.png"><br>

•Top 10 rules sorted by confidence:<br><br>
<img src="assets/top_10_confidence.png"><br>

•Top 10 rules sorted by lift:<br><br>
<img src="assets/top_10_lift.png"><br>

• Most frequent 2-itemset: {'Type of Travel_Business travel', 'Customer Type_Loyal Customer'}<br>
    o Frequency: 0.5085<br>
• Top 5 frequent items:<br><br>
<img src="assets/top_5_frequent.png"><br><br>

Associaton Rules Analysis <br><br>
<img src="assets/association_rules_analysis.png"><br><br>

•Top 10 rules sorted by lift:<br><br>
<img src="assets/top_10_lift_final.png"><br>
- The most interesting rules that are likely to provide real business value and insights are those with high lift values.<br>
- Lift measures how much more likely the consequent (rhs) is, given the antecedent (lhs), compared to if the two were independent.<br><br>

• **Insights**:<br>
o If a customer's type of travel is "Personal Travel", then there is a strong association with the customer being classified as "Eco" class and a "Loyal Customer".<br>
o The lift value of 2.3681 indicates that the occurrence of the antecedent and consequent together is 2.3681 times more likely than if they were statistically independent.<br>
o This means that customers who travel for personal reasons are 2.3681 times more likely to be classified as "Eco" class and "Loyal Customers" compared to what would be expected if these attributes were unrelated.<br>
o The confidence value of 0.8167 indicates that 81.67% of the transactions that contain "Personal Travel" also contain "Eco" class and "Loyal Customer".<br>
o The support value of 0.2535 indicates that 25.35% of the transactions contain both "Personal Travel" and "Eco" class and "Loyal Customer".<br>
o If a customer is classified as "Eco" class and is a "Loyal Customer", then there is a strong association with their type of travel being "Personal Travel".<br>
o The lift value of 2.3681 indicates that the occurrence of the consequent given the antecedent is 2.3681 times more likely than if they were statistically independent.<br>
o This means that customers who are classified as "Eco" class and "Loyal Customers" are 2.3681 times more likely to travel for personal reasons compared to what would be expected if these attributes were unrelated.<br>
o The confidence value of 0.7350 indicates that 73.50% of the transactions that contain "Eco" class and "Loyal Customer" also contain "Personal Travel".<br>
o The support value of 0.2535 indicates that 25.35% of the transactions contain both "Eco" class and "Loyal Customer", and "Personal Travel".<br>
o If a customer is classified as a "Loyal Customer" and their satisfaction level is "neutral or dissatisfied", then there is a strong association with their type of travel being "Personal Travel".<br>
o The lift value of 2.0927 indicates that the occurrence of the consequent given the antecedent is 2.0927 times more likely than if they were statistically independent.<br>
o This means that if a customer is classified as a "Loyal Customer" and their satisfaction level is "neutral or dissatisfied", there is 2.0927 times more likely that their type of travel will be "Personal Travel" compared to what would be expected if these attributes were unrelated.<br>
o The confidence value of 0.6495 indicates that 64.95% of the transactions that contain "Loyal Customer" with a satisfaction level of "neutral or dissatisfied" also contain "Personal Travel".<br>
o The support value of 0.2775 indicates that 27.75% of the transactions contain both "Loyal Customer" with a satisfaction level of "neutral or dissatisfied", and "Personal Travel".<br>
o If a customer's type of travel is "Personal Travel", then there is a strong association with the customer being classified as a "Loyal Customer" and having a satisfaction level of "neutral or dissatisfied".<br>
o The lift value of 2.0927 indicates that the occurrence of the consequent given the antecedent is 2.0927 times more likely than if they were statistically independent.<br>
o This means that if a customer's type of travel is "Personal Travel", there is a higher likelihood that the customer will be classified as a "Loyal Customer" and have a satisfaction level of "neutral or dissatisfied" compared to what would be expected if these attributes were unrelated.<br>
o The confidence value of 0.8940 indicates that 89.40% of the transactions that contain "Personal Travel" also contain "Loyal Customer" with a satisfaction level of "neutral or dissatisfied".<br>
o The support value of 0.2775 indicates that 27.75% of the transactions contain both "Personal Travel" and "Loyal Customer" with a satisfaction level of "neutral or dissatisfied".<br>
o If a customer's type of travel is "Business travel" and their satisfaction level is "satisfied", then there is a moderate association with the customer being classified as "Business" class and a "Loyal Customer".<br>
o The lift value of 1.8417 indicates that the occurrence of the consequent given the antecedent is 1.8417 times more likely than if they were statistically independent.<br>
o The confidence value of 0.7499 indicates that 74.99% of the transactions that contain "Business travel" with a satisfaction level of "satisfied" also contain "Business" class and "Loyal Customer".<br>
o The support value of 0.3013 indicates that 30.13% of the transactions contain both "Business travel" with a satisfaction level of "satisfied", and "Business" class and "Loyal Customer".<br>
o If a customer is classified as "Business" class and is a "Loyal Customer", then there is a moderate association with their type of travel being "Business travel" and their satisfaction level being "satisfied".<br>
o The lift value of 1.8417 indicates that the occurrence of the consequent given the antecedent is 1.8417 times more likely than if they were statistically independent.<br>
o The confidence value of 0.7400 indicates that 74.00% of the transactions that contain "Business" class and "Loyal Customer" also contain "Business travel" with a satisfaction level of "satisfied".<br>
o The support value of 0.3013 indicates that 30.13% of the transactions contain both "Business" class and "Loyal Customer", and "Business travel" with a satisfaction level of "satisfied".<br>
o If a customer is classified as "Eco" class, then there is a moderate association with their type of travel being "Personal Travel".<br>
o The lift value of 1.8257 indicates that the occurrence of the consequent given the antecedent is 1.8257 times more likely than if they were statistically independent.<br>
o The confidence value of 0.5666 indicates that 56.66% of the transactions that contain "Eco" class also contain "Personal Travel".<br>
o The support value of 0.2549 indicates that 25.49% of the transactions contain both "Eco" class and "Personal Travel".<br>
o If a customer's type of travel is "Personal Travel", then there is a strong association with the customer being classified as "Eco" class.<br>
o The lift value of 1.8257 indicates that the occurrence of the consequent given the antecedent is 1.8257 times more likely than if they were statistically independent.<br>
o The confidence value of 0.8214 indicates that 82.14% of the transactions that contain "Personal Travel" also contain "Eco" class.<br>
o The support value of 0.2549 indicates that 25.49% of the transactions contain both "Personal Travel" and "Eco" class.<br>
o If a customer is classified as a "Loyal Customer" and their type of travel is "Personal Travel", then there is a strong association with the customer being classified as "Eco" class.<br>
o The lift value of 1.8247 indicates that the occurrence of the consequent given the antecedent is 1.8247 times more likely than if they were statistically independent.<br>
o The confidence value of 0.8209 indicates that 82.09% of the transactions that contain both "Loyal Customer" and "Personal Travel" also contain "Eco" class.<br>
o The support value of 0.2535 indicates that 25.35% of the transactions contain both "Loyal Customer" and "Personal Travel", and "Eco" class.<br>
o If a customer is classified as "Eco" class, then there is a moderate association with the customer being classified as a "Loyal Customer" and their type of travel being "Personal Travel".<br>
o The lift value of 1.8247 indicates that the occurrence of the consequent given the antecedent is 1.8247 times more likely than if they were statistically independent.<br>
o The confidence value of 0.5635 indicates that 56.35% of the transactions that contain "Eco" class also contain both "Loyal Customer" and "Personal Travel".<br>
o The support value of 0.2535 indicates that 25.35% of the transactions contain "Eco" class, "Loyal Customer", and "Personal Travel".<br>

**3. 🔧 Preprocessing**

1- Encode categorical variables. 2- Drop Arrival delay in minutes column.<br>
2- Drop unnecessary columns (columns that don’t affect satisfaction)['Gender','Gate location','Departure/Arrival time convenient']<br>
3- Apply grouping on features with continuous variables<br>
4- Standardization: scaling features by subtracting the mean and then dividing by the standard deviation.<br>
   This results in features that have a mean of 0 and a standard deviation of 1.<br>

**4. 🔩 Model Building, Results and Evaluation:**   <br><br>
<img src="assets/models.png"><br>

• CatBoost achieved the highest F1 Score & Balanced Accuracy <br><br>
• Multi Nominal Naive Bayes without applying grouping on features with continuous variables from sklearn:<br>
o Balanced Accuracy: 0.8741036230929793<br>
o Training Accuracy: 0.7680455035417308<br>
o Testing Accuracy: 0.7649034093153716<br>
o Validation Accuracy: 0.7680455332217699<br>
o F1 Score: 0.7330791657322269<br>
o Precision: 0.7187335092348285<br>
o Recall: 0.7480091533180778<br><br>
• Multi Nominal Naive Bayes with applying grouping on features with continuous variables from sklearn:<br>
o Balanced Accuracy: 0.8660401815904305<br>
o Training Accuracy: 0.7687865722205113<br>
o Testing Accuracy: 0.7656145063801209<br>
o Validation Accuracy: 0.7687288538824919<br>
o F1 Score: 0.7336236699142458<br>
o Precision: 0.7199506520972858<br>
o Recall: 0.7478260869565218<br><br>
• Multi Nominal Naive Bayes without applying grouping on features with continuous variables from scratch using map reduce:<br>
o Balanced Accuracy: 0.7650422898817919<br>
o Training Accuracy: 0.8885220973206036<br>
o Testing Accuracy: 0.7626516019436653<br>
o f1_score: 0.7399809573271012<br>
o precision: 0.7018307199737296<br>
o recall: 0.7825171624713959<br><br>
• Multi Nominal Naive Bayes with applying grouping on features with continuous variables from scratch using map reduce:<br>
o Balanced Accuracy: 0.7611859775085901<br>
o Training Accuracy: 0.9015629812134278<br>
o Testing Accuracy: 0.7623750641962628<br>
o f1_score: 0.7321547846996482<br>
o precision: 0.7128858827610128<br>
o recall: 0.7524942791762014<br>



## azure:<br>

<img src="assets/compute.png"><br>
<img src="assets/workspace.png"><br>
<img src="assets/codeRun.png"><br>









      
      

   
