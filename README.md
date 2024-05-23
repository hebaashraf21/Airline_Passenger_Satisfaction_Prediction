
# Airline Passenger Satisfaction Prediction ✈️

## 🙇‍♂️ Problem description
The project aims to predict airline passenger satisfaction based on various factors such as flight distance, in-flight service, ease of online booking, and departure/arrival time convenience. Understanding the factors that contribute to passenger satisfaction is crucial for airlines to improve their services, enhance customer experience, and increase customer loyalty. By analyzing this dataset, we aim to provide valuable insights into what drives passenger satisfaction and how airlines can better meet customer expectations.


## 🗂️ Dataset
We used this publicly available dataset from kaggle which contains an airline passenger satisfaction survey.<br>
https://www.kaggle.com/datasets/teejmahal20/airline-passenger-satisfaction


## 🧱 Project pipeline
<img src="assets/pipeline.png" alt=" " >

1. **Data Exploring & Cleaning**:
- Explore the features and the unique values for each.
- Explore dataset size:
o Training data: 103904 rows × 25 columns
o Test data: 25976 rows × 25 columns
- Remove nulls from training & test dataset.
- Check if there are duplicate rows
- Remove unnecessary columns:  ID, Unamed:0

2. **Exploratory Data Analysis**:<br>
  2.1 Univariate Analysis<br>
      2.1.1 Charts for categorical variables:<br>
      <img src="assets/univariate_pie_1.png" alt="" >
      <img src="assets/univariate_pie_2.png" alt="" >
      <img src="assets/univariate_pie_3.png" alt="" >
      <img src="assets/univariate_pie_4.png" alt="" >
      <img src="assets/univariate_pie_5.png" alt="" >
      <img src="assets/univariate_pie_6.png" alt="" >
      <img src="assets/univariate_pie_7.png" alt="" ><br>

      • Insights:<br>
      - There is an almost equal number of male and female participants in the survey.<br>
      - Most of passengers are neutral or dissatisfied = 56.7% ==> we need to analysis the reasons and try to find business solutions to make them more satisfied<br>
      - We have more loyal customer data (81.7%) <br>
      - Most of travels are for Business travel (69%)<br>
      - Very few people fly in the economy plus class. They usually prefer Economy or Business.<br>

      2.1.2 Histogram for numerical variables<br>
       <img src="assets/univariate_histograms_training.png" alt="" ><br>

   • Insights: <br>
   - Most of the delays are 0, which is a good indicator.<br>
   - The variables Flight Distance and Departure Delay and Arrival Delay are all heavily right-skewed.<br>

   Investigate problem of outliers:<br>

      Portion of outliers in each column:<br>
         Departure Delay in Minutes 0.139831<br>
         Arrival Delay in Minutes   0.134699<br>
         Flight Distance            0.022049<br>

- Since the portion of rows having the outliers in the "Flight Distance" is very small so we will remove it.<br>
- We will normalize "Departure Delay in Minutes","Arrival Delay in Minutes"<br>
<img src="assets/univariate_histograms_after_handling_outliers_training.png" alt="" ><br>

2.2 Bivariate Analysis<br>
2.2.1 Bar charts & Pie charts for categorical features<br>
<img src="assets/bivariate_bar.png" alt="" ><br>
Then we focused on plotting the distribution for satisfied & dissatisfied for each feature:<br>
<img src="assets/bivariate_pie.png" alt="" ><br>
2.2.2 Histograms for numerical columns
<img src="assets/bivariate_histograms.png" alt="" ><br>

Grouping to help in insights:<br>
<img src="assets/grouping.png" alt="" ><br>

• Insights: <br>
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
Insights:<br>
Positively Correlated: - Business Class ,online boarding, inflight entertainment, seat comfort, on-board service, Legroom service, cleanliness, Flight distance, and Business travels are strong reasons for people satisfaction.<br>
Negatively Correlated: - Personal Travels, Economy Class, Eco plus Class or being Disloyal Customer results in Unsatisfaction.<br>

2.3 Multivariate Analysis<br>
<img src="assets/multivariate_correlation.png" alt="" ><br>
Insights:<br>
- Departure Delay is highly correlated with Arrival Delay. [Will deal with this in feature engineering].<br>
- Inflight WiFi service and Ease of online booking are + correlated.<br>
- Inflight entertainment, Food and Drink, Seat comfort and cleanliness are + correlated.<br>
- Baggage handling is + correlated with Inflight service.<br>

<img src="assets/arrival_departure_correlation.png" alt="" ><br>

• Insights:<br>
- There is a strong correlation between the two columns we can drop one of the two columns and as Arrival Delay in Minutes column has some null, we can drop it.<br>
- Remove quintile columns ['Age_quintile', 'Flight Distance_quintile', 'Arrival Delay in Minutes_quintile', 'Departure Delay in Minutes_quintile']<br>


2.4 Clustring:<br>
Applying Kmeans on the data with 3 clusters<br>
<img src="assets/cluster_distribution.png"><br>
The portion of each class:<br>
o Class 1 ==> 0.630900 <br>
o Class 0 ==> 0.219453 <br>
o Class 2 ==> 0.149648 <br>
• Most of the data (63%) is in one cluster (cluster 1) <br>
• Showing aggregates of each numeric column grouped by the cluster.<br>

<img src="assets/clusters_data.png"><br>

• Insights:<br>
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

• Insights:<br>
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








      
      

   
