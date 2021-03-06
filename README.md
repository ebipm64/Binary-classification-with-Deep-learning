# Relevant Information:

   This dataset is based on "Bank Marketing" UCI dataset (please check the description at: http://archive.ics.uci.edu/ml/datasets/Bank+Marketing).
   The data is enriched by the addition of five new social and economic features/attributes (national wide indicators from a ~10M population country), published by the Banco de Portugal and publicly available at: https://www.bportugal.pt/estatisticasweb.
   This dataset is almost identical to the one used in [Moro et al., 2014] (it does not include all attributes due to privacy concerns). 
   Using the rminer package and R tool (http://cran.r-project.org/web/packages/rminer/), we found that the addition of the five new social and economic attributes (made available here) lead to substantial improvement in the prediction of a success, even when the duration of the call is not included. Note: the file can be read in R using: d=read.table("bank-additional-full.csv",header=TRUE,sep=";")
   
   # Goal:
   in this project we are goinf to is to predict if the client will subscribe a bank term deposit (variable y)
   
   Input variables:
   # Bank client data:
   1 - age (numeric) 
   
   2 - job : type of job (categorical: "admin.","blue-collar","entrepreneur","housemaid","management","retired","self-employed","services","student","technician","unemployed","unknown")
   
   3 - marital : marital status (categorical: "divorced","married","single","unknown"; note: "divorced" means divorced or widowed)
   
   4 - education (categorical: "basic.4y","basic.6y","basic.9y","high.school","illiterate","professional.course","university.degree","unknown")
   
   5 - default: has credit in default? (categorical: "no","yes","unknown")
   
   6 - housing: has housing loan? (categorical: "no","yes","unknown")
   
   7 - loan: has personal loan? (categorical: "no","yes","unknown")
   
   8 - contact: contact communication type (categorical: "cellular","telephone") 
   
   9 - month: last contact month of year (categorical: "jan", "feb", "mar", ..., "nov", "dec")
   
  10 - day_of_week: last contact day of the week (categorical: "mon","tue","wed","thu","fri")
  
  11 - duration: last contact duration, in seconds (numeric). Important note:  this attribute highly affects the output target (e.g., if duration=0 then y="no"). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.
  12 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
  
  13 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
  
  14 - previous: number of contacts performed before this campaign and for this client (numeric)
  
  15 - poutcome: outcome of the previous marketing campaign (categorical: "failure","nonexistent","success")
  
  16 - emp.var.rate: employment variation rate - quarterly indicator (numeric)
  
  17 - cons.price.idx: consumer price index - monthly indicator (numeric)     
  
  18 - cons.conf.idx: consumer confidence index - monthly indicator (numeric)     
  
  19 - euribor3m: euribor 3 month rate - daily indicator (numeric)
  
  20 - nr.employed: number of employees - quarterly indicator (numeric)

  Output variable (desired target):
  21 - y - has the client subscribed a term deposit? (binary: "yes","no")

---------------------------------------------------------------------------------------------------------------------------------
# Data Cleaning: 
a) First check the data set for NULL values

b) As the most of the features are categorical it's hard to fill out the "unknown" data with conventional method to fill them out. Meanwhile the data set are large enougth so we drop 'Unknown' data. 

# Explorotory Data Analysis(Exploratory Data Analysis)
In this section we do some analysis base on the data set

a) As we see there is district separation in target base on the Age 

![age vs target](https://user-images.githubusercontent.com/71351619/132996477-80004a1e-7c6f-40e6-8910-aaa31a102802.png)

b) Check the correlation between numerical features and target; As it's seen the "duration" is mostly correlated feature vs target

![target corr](https://user-images.githubusercontent.com/71351619/132996750-714fa1ef-ef56-4bbc-bfd0-7f6a1791bea7.png)
---------------------------------------------------------------------------------------------------------------------------------
# Preparation
Following steps were applied:
a) Balance the labels using the oversamplig method

b) Convert the object types features to numerical; using get_dummies method

c) Split the data to train and test sets

d) Scale the features using  StandardScaler

---------------------------------------------------------------------------------------------------------------------------------
# Model Deployment

a) Define the model: Total layer 4; 2 hidden layer

b) Activation function: Relu for first 3 layers. As this is a classification task then the last layer must be a Sigmoid

c) Avoiding the overfitting:
For avoinding the overfitting I applied two scales

1. Define the Dropout layer

2. Use the earlystopping

---------------------------------------------------------------------------------------------------------------------------------
# Model Evaluation

a) Plot the loss for train and test data set to monitor the overfitting

<img width="474" alt="loss vs val" src="https://user-images.githubusercontent.com/71351619/135737688-ea4d06c3-94ba-46b6-a566-1439ae8bc68f.png">


b) Classification Report


<img width="700" alt="Classification Report" src="https://user-images.githubusercontent.com/71351619/133947797-d824ca47-1f49-49a0-99ea-528757c889f0.PNG">


c) Plot ROC and AUC(Area Under Curve) curve

![ROC curve](https://user-images.githubusercontent.com/71351619/133947742-37644023-6b1b-496f-8f3f-16d0ee2228a0.png)






e) Confusion_matrix


<img width="102" alt="confusion matrix" src="https://user-images.githubusercontent.com/71351619/135737691-9a68eada-c212-47a7-b785-08000b04c947.PNG">

