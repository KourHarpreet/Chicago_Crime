# Predicting Arrest on Chicago Crime Data


## ABSTRACT

In this report, we show how data mining techniques can be used to solve predictive tasks related to crime data. We identify a predictive task, train and evaluate models to perform predictions and document the results.

## INTRODUCTION

Predictive Policing is a modern solution to fundamental problems all police forces face today. Efficient allocation of resources and preemptive law enforcement. There are various predictive methods that help police departments determine when and where crime will happen before it happens. In this analysis, we will focus on one simple predictive tasks.
 
Predict whether an arrest will happen for a given incident.

The following sections describe the data set, findings from initial analysis, the prediction tasks identified and the results.

## DATASET 

The dataset chosen for this project consists of incidents of crime reported in the city of Chicago from 2001 to 2017. 

Source: (https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2)
Title: *Crimes_-_2001_to_present*
The data set is approx. 6.2 million entries. Each entry consists of the following fields:

Field	Description

```
ID	Record id
Case.Number	Case number
Block	Block address of Crime
IUCR	Code for Crime type
Date	Date and time about the incident occurred
Primary.Type	Category of Crime
Description	Description of crime occurred 
Location.Description	Short description of crime location
Arrest	If the arrest has happened
Domestic	If it is domestic violence
Beat	Office Patrol Area
District	Indicates the police district where the incident occurred
Ward	The ward (City Council district) where the incident occurred
Community.Area	Indicates the community area where the incident occurred. Chicago has 77 community areas
FBI.Code	Indicates the crime classification as outlined in the FBI's National Incident-Based Reporting System (NIBRS
Year	Year in which incident occurred
Latitude	Latitude of incident 
Longitude	Longitude of incident
Day	Day of Month
Month	Month
Weekday	Weekday
```
Some of the records had missing values for the fields and hence were excluded later.
**Note: Variable Date in original dataset has been segregate into Day, Month and Weekday variables.

## DATA CLEANING

Below Data Cleaning, have been done to make our analysis way easier and observatory:
```
a.	The dataset has been reduced to year '2007-2017' as it was too large with 6297578 observations.
b.	All useful variables have been converted to categorical variables.
c.	Removed Missing Values and Whitespaces.
d.	Variable Date in original dataset has been segregate into Day, Month and Weekday variables.
e.	Converted different format of ‘Non-Criminal’ category under Primary. Type variable into one.
f.	Duplicates observations have been removed.
```

## EXPLORATORY ANALYSIS 

Data exploration helps infer useful information and predict important aspects of crime detection and prevention. At the same time, the nature of the data largely determines what kind of prediction tasks can be performed. A preliminary analysis of data was performed to identify useful features for building a predictive model. It revealed some interesting trends and patterns, which are documented below. 
 
Crime and Arrest rate by year     :
        
                   ![crime and arrest rate by year](https://user-images.githubusercontent.com/23300177/37783651-672e0cac-2dcc-11e8-8dbb-44731116f17b.jpg)
 

Above Figure, represent the crime statistics for Chicago taking into account the number of crime and arrest rate over the period of years. This helped to give a better overall summary of the crimes occurrence and arrests that happened throughout the year 2007-2017. It is clear from the graph that the arrest rates and the crime rates are decreasing over year.

Crime and Arrest rate by month     :

![crime and arrest rate by month jpg](https://user-images.githubusercontent.com/23300177/37783710-8add1b0c-2dcc-11e8-9d3a-53ac177591d1.png)
 

Above Figure, represent the crime statistics for Chicago taking into account the number of crime and arrest rate over the period of months. This helped to give a better overall summary of the crimes occurrence and arrests that happened throughout the months for year 2007-2017. It is clear from the graph that there is a seasonal influence in crime rate.


Crime and Arrest by Weekday    :

![crime and arrest rate by weekday](https://user-images.githubusercontent.com/23300177/37783754-a60a05b6-2dcc-11e8-8971-de2ca79a3213.png)

The below visualizations depicts the number of crime occurrences and arrests on a particular day of week.

                                            
Figure 'Crime by Day' shows the number of crime occurrence over the weekdays in Chicago. Where Friday has the maximum number of crimes occurrence and Sunday has the least number of crimes occurrence.

 

Figure 'Arrest by Day' shows the number of arrest of crimes over the weekdays in Chicago. Where Friday has the maximum number of crimes arrest and Sunday has the least number of crimes arrest. 

Overall, there are some similarities between the occurrence of crime and arrest rate in two figures.
  
Crime and Arrest by Primary Type of crime     :

![crime and arrest by primary type of crime](https://user-images.githubusercontent.com/23300177/37783780-b5eabad4-2dcc-11e8-9c90-81fc4ab9a3ff.png)


Above Figures provide a statistical comparison between numbers of particular crime type committed and arrest rate of the crime type. We chose to limit the comparison to top 10 crimes and arrests in order to get a fair comparison. While most of the crime occurrence belong to Theft crime type we graphed over the arrest rate and found that the arrests rate are more for narcotics crime type among total number of crimes. It helps to better understand and visualize the numbers of crime committed and compare the same with the arrest rate for that particular crime.

Crime by Location     :
           ![crime by location](https://user-images.githubusercontent.com/23300177/37783812-c50718f0-2dcc-11e8-9b9e-fdfa3d682adc.png)


This Figure shows the number of crime occurrences over different locations in Chicago. With many locations, we chose to display top fifteen different areas. Street having the most crime rate among the 158 locations while Department store has the minimum crime rate in top 15 areas of the total crimes. Overall, the street seems to be the most dangerous area.

  These insights help to understand the distribution of incident and some interesting trends and patterns.


## PREDICTIVE TASK 

We identified a predictive task based on the information available in the data set. 

**Predicting whether an arrest will be made for a committed crime:  Our predictive task was to predict arrests for reported crimes.

To perform this prediction we used KNN- k nearest neighbors, which is a simple algorithm that stores all available cases and classifies new cases by a majority vote of its k neighbors. This algorithm segregates unlabeled data points into well-defined groups.

We took a random sample of 25000 observations to predict the arrest likelihood based on past arrests in our model. 

As our entire explanatory variable are categorical, we create dummies for the same. This feature is of paramount importance since the scale used for the values for each variable might be different. The best practice is to convert the value to 1 if the feature was present, 0 if absent and transform all the values to a common scale.

The KNN algorithm is applied to the training data set and the results are verified on the test data set.
For this, we would divide the data set into 2 portions in the ratio of 80: 20 for the training and test data set respectively i.e. 19958 observations for training dataset and 5042 observations for test dataset

The explanatory variables were chosen based on the pre-processing done during the exploratory analysis. ‘7’ variables were considered:
```
a) Month: In which the crime happened represented as a 12 features vector 
b) Type of crime such as Narcotics, Battery etc. represented as a 34 features vector, one for each crime type. This was represented as a feature vector with categorical labels (1 if present, 0 if absent). A total of 32 categories were identified. 
c) Location description: A short description of the street/location in which the crime happened. The location description was used as a categorical label and represented as a binary value (1 if the feature was present, 0 if absent). 
d) Beat: A beat is the smallest police geographic area in which crime happened.
e) Weekday: In which day of the week crime happened represented as a 7 features vector.
f) District: Indicates the police district where the incident occurred.
g) Year: In which year (2007-2017) a crime occurred.
```

Month was chosen because our exploratory analysis indicates that it is a seasonal influence in crime rate. This is revealed in above Figure. Since it is correlated with the rate of crime, by transitivity it is also correlated with the arrest rate for the crime. If there is more crime in a month then correspondingly, there will be more arrests. Our analysis also indicated that the probability of an arrest is heavily influenced by crime type. 

Above Figure also reveals that there are high disparities in arrest rate with some of the crime categories. Since this is the case, it seems that crime type is a strong predictor of whether or not there will be an arrest. 

The location description was thought to influence arrest rate as well because it seems that it is more common for arrests to be made in some locations more often than others. For example, it may be more likely for an individual to be arrested for battery in the middle of a parking lot than in a more discrete location such as an alley way. This feature was added because of this qualitative assumption. We found that the score improved after adding this as a feature. 

Beat, Weekday, District, Year were taken under consideration as they influence the time and area of the crime.

All of the features were represented as binary vectors in order to allow equal representation and individual weights for each possible choice of each feature. Preprocessing was done on all of the categorical variables in order to map them to their corresponding binary feature vector representations.

Train a model     :

knn () function needs to be used to train a model. The knn() function identifies the k-nearest neighbors using Euclidean distance where k is a user-specified number.

The value for k in our model is 111.

Knn() function returns a factor value of arrest labels for each observation in the test data.


## EVALUATION AND RESULTS 

The following section documents the evaluation results for the predictive tasks described in the previous section. Explanatory variables are defined and predictive models are built in an attempt to improve the  performance. The results are documented and analyzed. 

Pros of KNN: The algorithm is highly unbiased in nature and makes no prior assumption of the underlying data. Being simple and effective in nature, it is easy to implement and has gained good popularity.

For each predictive task, we split the data set into training and test set. We then trained the models and used them to predict the labels on the test set.

The total accuracy of the model is 83.16144% 

Confusion matrix     :
```

predictions	Testing.label
	FALSE	TRUE
FALSE	3681	841
TRUE	8	512
```

A confusion matrix shows the number of correct and incorrect predictions made by the classification model compared to the actual outcomes (target value) in the data. The above table displays a 2 * 2 confusion matrix for two classes (False and True). 

This indicates that the arrest probability for the type of crime committed has a very strong influence in whether or not there will be an arrest. 

## CONCLUSION 

In this project, we used data mining techniques to perform predictive tasks on crime data. A predictive task were implemented - predicting arrests for a given type of crime in a given location. Pre-processing of data prior to training the model helped us identify useful features for building the models. The models used the techniques we learnt in the course. The results from evaluation are discussed and documented. Though we observed repeated patterns in crime count over months with summer being the highest, it did not add value to the prediction of whether or not arrests will be made but did help influence the prediction in term of number of crimes in a beat day. The type of crime also played strong role in predicting arrests and crime frequencies in Chicago. These tasks can be further extended to include much more extensive patterns in predictive crime if information about the victims and the offenders are made available.






