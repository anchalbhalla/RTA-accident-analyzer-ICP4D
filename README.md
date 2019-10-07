# transport-accident-analyzer-ICP4D
This demo showcases the capabilities of IBM Cloud Pak for Data while solving the a use case related to a transportation authority. It analyses the accidents occurred in Dubai in 2017 and then uses machine learning models to analyse driver and location risk. The front end is build as a shiny application. 

## Pre - Data Engineering
- The original dataset was in Arabic and hence had to be translated to English. I used Google sheets and <b>google translate</b> to perform the operation. 
- The dataset had to group age of drivers in 10 different age groups. This was performed on <b>Excel</b> using the <b>Vlookup</b> function. 
- The data also had to specify the time groups and <b>Vlookup</b> was used for this part as well 
- Next, only 6 locations needed to be selected, hence <b>Data Refinery</b> was used to filter out the locations 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/data1.gif"> 

## Collect 

In collect part data connections need to be created. A Data connection was created for Db2 Warehourse on Cloud. To do that the following was done: 

##### Steps
1. Create a analystics project 
2. Create a data source  
3. Add host, username, password, DB name 
4. Test connection 
5. Add connection

## Organize 

This is the task of a data engineer. In this step <b>data discovery</b> will be performed, <b>business glossary terms</b> will be added and <b>governence rules and policies</b> are added. <b>Data lineage</b> will be also be demonstrated with this. 

### Data Discovery 
Used to analyse the data quality and assign terms to the datasets and project. 

##### Steps 
1. Add the connection 
2. Select analyse data quality
3. Select assign terms
4. Click Discover
5. Assign the terms from the appropriate category 

<img src = "https://github.com/anchalbhalla/mortgage-default-prediction-icp4d/blob/master/gifs/discovery.png">

### Business Glossary 

Create a business glossary understood by everyone

##### Steps
1. Create a category
2. Create a terms
3. Save
4. Repeat 2 to 3 until done 

<img src = "https://github.com/anchalbhalla/mortgage-default-prediction-icp4d/blob/master/gifs/terms.png">

### Goverence 
Compliance to rules and policies of the industry is very important for every business 

<img src = "https://github.com/anchalbhalla/mortgage-default-prediction-icp4d/blob/master/gifs/rules.png">

### Data Lineage  
Data lineage shows the interconnection between all terms, rules and the datasets. It can seen how the terms and rules are linked to the appropriate dataset. 

## Cognos Dashboards 
### Insights Gained: 
#### Driver Age: 
- People between the age 20 - 29 cause lot of accidents and when the injury severity is increased the age group rises to 30 - 39 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/visual1.png">

  
#### Accident Timing: 
- Most of the accidents happen Early in the morning or Morning time. This could be because of the increase in traffic on roads. 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/visual2.png">

  
#### Driver profile analysis: 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/visual3.png">

- Most of the accidents are caused by drivers in the age 20 - 29 and most of them are students or students in a military school. 
- Blue Collar occupations such as painters, car drivers, etc. also between the age of 20 - 29 cause a lot accidents. Hence safer driving awarness has to be spread to this community. 
- These drivers are also the highest number of people who did not wear a seat belt during the accident.
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/graph1.gif">

#### Location and Cause analysis: 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/visual4.png">

- Main kind of accidents is Hitting another vehicle 
- Emirates Road has the most number of accidents 
- So the main cause of accident at Emirates Road is Hitting another vehicle and hitting into an iron barrier, this could mean there is some design malfunction which needs to be manually accessed by the authorities.

<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/graph2.gif">


## Modelling - SPSS 

#### Driver Risk Model 
Various classification models were tried and tested for this case. But most of them gave a very low accuracy. But the best one was XG Boost Trees which gave an accuracy above 75%. Below is the list of the models tested: 
- <b>XG Boost Trees</b>
- Random forest 
- Neural networks
- C5 - decision tree algorithm
- Logistic Regression 

Before moving into the modelling, the data had to be balanced since the imbalance in the injury severity was causing a class imbalance and reducing the model accuracy.
Also, the dataset was partitioned into training and testing. And it had a 95-5 partition.
  
 This was the flow created for this model. This flow can be retrieved from flow2.str file in this repositary: 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/spss1.png">



#### Location Risk Model 
Various classification models were tried and tested for this case. But most of them gave a very low accuracy. But the best one was CHAID which gave an accuracy above 75%. Below is the list of the models tested: 
- <b>CHAID</b>
- Random forest 
- Neural networks
- XG Boost Trees
- Logistic Regression 
- Auto Classifier models
 
 Also, the dataset was partitioned into training and testing. And it had a 95-5 partition.
 
 This was the flow created for this model. This flow can be retrieved from flow3.str file in this repositary: 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/spss2.png">



## Shiny Application 
Once the model is created it needs to be deployed by creating a project release. This will deploy the model into production and we can use the API endpoint in our shiny application to get the final results as seen below.

### Analysing Driver Profile Risk 
Features to be analysed: 
- Age 
- Gender
- Occupation
- Driving license issue date
- Car manufactured year 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/app1.gif">


### Analysing Location Risk
Features to be analysed: 
- Accident Time
- Accident Location 
- Weather
- Type of accident
- Cause of accident 
<img src = "https://github.com/anchalbhalla/transport-accident-analyzer-cloud/blob/master/pics%20and%20gifs/app2.gif">
