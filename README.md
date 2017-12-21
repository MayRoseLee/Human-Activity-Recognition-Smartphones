# Human-Activity-Recognition-Smartphones
Assignment for Getting and Cleaning Data class
READ.ME
To download the Dataset into R, use the code:
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl, destfile = "HAR")
   A 59.7MB dataset will appear.  From the explorer window click on the HAR folder, unzip the files desired, copy/paste them into the working directory.
First create the test dataset, the files needed  are  X_test.txt, y_test.txt, features.txt, subject_test.txt
Read these files into R using read.table().  
x_test <- read.table("X_test.txt", header= FALSE)
y_test <- read.table("y_test.txt", header = FALSE)
features <- read.table("features.txt", header= FALSE)
subject_test <- read.table("subject_test.txt")
Examine the x_test file.
 x_text contains 2947   and 561 variables.

Examine the features file
 features contains 561 observations and 2 variables. The variable names are V1 and V2. The V2 column of features has the variable names for the 561 variables of x_test.  We only want means and standard deviations.  So locate which variable name has "-mean" or "std" included on it.  Keep these variables, and later, rename them for clarity.
Use the dplyr package. Select the variables which are means and standard deviation using the code
x_test_selected <- select(x_test, V1, V2, V3, V4, V5, V6, V41, V42, V43:V46, V81:V86, V121:V126, V161:V166,  V201, V202, V214, V215, V227, V228, V240, V241, V253, V254, V266:V271, V294: V296, V345, V346, V347: V350, V266: V271,V294: V296, V345: V350, V373, V374,V375,
 V424:V429, V452, V453, V454, V503, V504, V513, V516, V517, V526, V529, V530, V539, V542, V543, V552)

Next, rename the variables that were selected
 x_test_renamed <- rename(x_test_selected, tBodyAcc.mean_X = V1,
                             tBodyAcc.mean_Y = V2,
                             tBodyAcc.mean_Z = V3,
                             tBodyAcc.std_X = V4,
                             tBodyAcc.std_Y = V5,
                             tBodyAcc.std_Z =V6,
                            
                               tGravityAcc.mean_X = V41,
                             tGravityAcc.mean_Y =V42,
                             tGravityAcc.mean_Z =V43,
                             tGravityAcc.std_X = V44,
                             tGravityAcc.std_Y = V45,
                             tGravityAcc.std_Z =V46,
                            
                               tBodyAccJerk.mean_X = V81,
                             tBodyAccJerk.mean_Y = V82,
                             tBodyAccJerk.mean_Z = V83,
                             tBodyAccJerk.std_X = V84,
                             tBodyAccJerk.std_Y = V85,
                             tBodyAccJerk.std_Z = V86,
                            
                              
                               tBodyGyro.mean_X = V121,
                             tBodyGyro.mean_Y = V122,
                             tBodyGyro.mean_Z = V123,
                             tBodyGyro.std_X = V124,
                             tBodyGyro.std_Y = V125,
                             tBodyGyro.std_Z = V126,
                            
                              
                               tBodyGyroJerk.mean_X = V161,
                             tBodyGyroJerk.mean_Y = V162,
                             tBodyGyroJerk.mean_Z = V163,
                             tBodyGyroJerk.std_X = V164,
                             tBodyGyroJerk.std_Y = V165,
                             tBodyGyroJerk.std_Z = V166,
                             
                               tBodyAccMag.mean= V201,
                             tBodyAccMag.std = V202,
                             
                               tGravityAccMag.mean= V214,
                             tGravityAccMag.std =V215,
                             
                               tBodyAccJerkMag.mean = V227,
                             tBodyAccJerkMag.std = V228,
                            
                               tBodyGyroMag.mean = V240,
                             tBodyGyroMag.std = V241,
                            
                               tBodyGyroJerkMag.mean= V253,
                             tBodyGyroJerkMag.std = V254,
                            
                               fBodyAcc.mean_X = V266,
                             fBodyAcc.mean_Y = V267,
                             fBodyAcc.mean_Z = V268,
                             fBodyAcc.std_X = V269,
                             fBodyAcc.std_Y = V270,
                             fBodyAcc.std_Z = V271,
                          fBodyAcc.meanFreq_X = V294,
                          fBodyAcc.meanFreq_Y = V295,  
                          fBodyAcc.meanFreq_Z = V296, 
                                                       
                              fBodyAccJerk.mean_X = V345,
                             fBodyAccJerk.mean_Y = V346,
                             fBodyAccJerk.mean_Z = V347,
                             fBodyAccJerk.std_X = V348,
                             fBodyAccJerk.std_Y = V349,
                            fBodyAccJerk.std_Z = V350,
                             fBodyAccJerk.meanFreq_X = V373,
                             fBodyAccJerk.meanFreq_Y = V374,
                             fBodyAccJerk.meanFreq_Z = V375,
                              
                               fBodyGyro.mean_X = V424,
                             fBodyGyro.mean_Y = V425,
                             fBodyGyro.mean_Z = V426,
                             fBodyGyro.std_X = V427,
                             fBodyGyro.std_Y = V428,
                            fBodyGyro.std_Z = V429,
                             fBodyGyro.meanFreq_X = V452,
                          fBodyGyro.meanFreq_Y = V453,
                          fBodyGyro.meanFreq_Z = V454,
                               fBodyAccMag.mean = V503,
                             fBodyAccMag.std = V504,
                           fBodyAccMag.meanFreq = V513,
                           fBodyBodyAccJerkMag.mean = V516,
                           fBodyBodyAccJerkMag.std =V517,
                           fBodyBodyAccJerkMag.meanFreq = V526,
                           fBodyBodyGyroMag.mean = V529,
                           fBodyBodyGyroMag.std = V530,
                           fBodyBodyGyroMag.meanFreq = V539,
                           fBodyBodyGyroJerkMag.mean = V542,
                           fBodyBodyGyroJerkMag.std= V543,
                           fBodyBodyGyroJerkMag.meanFreq = V552)
                           
 

 Looking at the subject_test file--here, V1 is the subject.  Rename this column “subject”.
 subject_test <- rename(subject_test, subject= V1)
 For the y_test file, V1 is the type of  activity.  Rename this column “activity” using this code.
 y_test <- rename(y_test, activity = V1)
 
 Use cbind to create a data frame with subjects, activity types, and test measurements.  Call this dataframe testdata.
 testdata <- cbind(subject_test, y_test, x_test_renamed)
Now testdata has 2947 observations and 81 variables.

 
Add a column to indicate the type of data(test or training)
 testdata <- mutate (testdata, type= "test")
Now testdata has 2947 observations and 82 variables.


y-test contains the integers 1 to 6.  These numbers correspond to the 6 types of activities
1=”walking”
2 = “walking upstairs”
3= “walking downstairs
4= “sitting”
5 =”standing”
6 = “laying”


The y_test  file consists of a single column of integers from 1 to 6.  There are 2947 rows, so the activities can be matched with the observations of x_test_renamed.


###Subject_test   Each row identifies the subject who performed the activity for each window sample.  Its range is from 1 to 30.  There are 2947 rows, so the subjects can be matched with the observations of x_test_renamed.





  ### Creating a dataframe for training data was similar to creating the dataframe for test data.  From the explorer window, unzip the files desired, copy/paste them into the working directory.
  Files were X_train.txt, y_train.txt, features.txt, subject_train.txt
   Read the files into R using read.table( ).  
     x_train <- read.table("X_train.txt", header= FALSE)
     y_train <- read.table("y_train.txt", header = FALSE)
    features <- read.table("features.txt", header= FALSE)
     subject_train <- read.table("subject_train.txt")
  

      The V2 column of features has the variable names for the 561 variables of x_train.  We only want means and standard deviations of measurements.
So locate which variable name has "-mean" or "std" included on it.  Keep these variables and later rename them for clarity.
Use dplyr package.  Select the variables which are means and standard deviations. 
        
     x_train_selected <- select(x_train, V1:V6, V41:V46, V81:V86, V121:V126, V161:V166, 
                                V201, V202, V214, V215, V227, V228, V240, V241, V253, V254, V266: V271,V294:V296, V345:V350,     V373:V375,  V424: V429,  V452, V453, V454, V503, V504, V513, V516, V517, V526, V529, V530, V539, V542, V543, V552 )
Only 79 variables, as compared to 561 at the beginning.
Rename the variables that were selected using this code.
     x_train_renamed <- rename(x_train_selected, tBodyAcc.mean_X = V1,
                              tBodyAcc.mean_Y = V2,
                              tBodyAcc.mean_Z = V3,
                              tBodyAcc.std_X = V4,
                              tBodyAcc.std_Y = V5,
                              tBodyAcc.std_Z =V6,
                              
                              tGravityAcc.mean_X = V41,
                              tGravityAcc.mean_Y =V42,
                              tGravityAcc.mean_Z =V43,
                              tGravityAcc.std_X = V44,
                              tGravityAcc.std_Y = V45,
                              tGravityAcc.std_Z =V46,
                              
                              tBodyAccJerk.mean_X = V81,
                              tBodyAccJerk.mean_Y = V82,
                              tBodyAccJerk.mean_Z = V83,
                              tBodyAccJerk.std_X = V84,
                              tBodyAccJerk.std_Y = V85,
                              tBodyAccJerk.std_Z = V86,
                              
                              
                              tBodyGyro.mean_X = V121,
                              tBodyGyro.mean_Y = V122,
                              tBodyGyro.mean_Z = V123,
                              tBodyGyro.std_X = V124,
                              tBodyGyro.std_Y = V125,
                              tBodyGyro.std_Z = V126,
                              
                              
                              tBodyGyroJerk.mean_X = V161,
                              tBodyGyroJerk.mean_Y = V162,
                              tBodyGyroJerk.mean_Z = V163,
                              tBodyGyroJerk.std_X = V164,
                              tBodyGyroJerk.std_Y = V165,
                              tBodyGyroJerk.std_Z = V166,
                              
                              tBodyAccMag.mean= V201,
                              tBodyAccMag.std = V202,
                              
                              tGravityAccMag.mean= V214,
                              tGravityAccMag.std =V215,
                              
                              tBodyAccJerkMag.mean = V227,
                              tBodyAccJerkMag.std = V228,
                              
                              tBodyGyroMag.mean = V240,
                              tBodyGyroMag.std = V241,
                              
                              tBodyGyroJerkMag.mean= V253,
                              tBodyGyroJerkMag.std = V254,
                              
                              fBodyAcc.mean_X = V266,
                              fBodyAcc.mean_Y = V267,
                              fBodyAcc.mean_Z = V268,
                              fBodyAcc.std_X = V269,
                              fBodyAcc.std_Y = V270,
                              fBodyAcc.std_Z = V271,
                              fBodyAcc.meanFreq_X = V294,
                              fBodyAcc.meanFreq_Y = V295,  
                              fBodyAcc.meanFreq_Z = V296, 
                              
                              fBodyAccJerk.mean_X = V345,
                              fBodyAccJerk.mean_Y = V346,
                              fBodyAccJerk.mean_Z = V347,
                              fBodyAccJerk.std_X = V348,
                              fBodyAccJerk.std_Y = V349,
                              fBodyAccJerk.std_Z = V350,
                              fBodyAccJerk.meanFreq_X = V373,
                              fBodyAccJerk.meanFreq_Y = V374,
                              fBodyAccJerk.meanFreq_Z = V375,
                              
                              fBodyGyro.mean_X = V424,
                              fBodyGyro.mean_Y = V425,
                              fBodyGyro.mean_Z = V426,
                              fBodyGyro.std_X = V427,
                              fBodyGyro.std_Y = V428,
                              fBodyGyro.std_Z = V429,
                              fBodyGyro.meanFreq_X = V452,
                              fBodyGyro.meanFreq_Y = V453,
                              fBodyGyro.meanFreq_Z = V454,
                              fBodyAccMag.mean = V503,
                              fBodyAccMag.std = V504,
                              fBodyAccMag.meanFreq = V513,
                              fBodyBodyAccJerkMag.mean = V516,
                              fBodyBodyAccJerkMag.std =V517,
                              fBodyBodyAccJerkMag.meanFreq = V526,
                              fBodyBodyGyroMag.mean = V529,
                              fBodyBodyGyroMag.std = V530,
                              fBodyBodyGyroMag.meanFreq = V539,
                              fBodyBodyGyroJerkMag.mean = V542,
                              fBodyBodyGyroJerkMag.std= V543,
                              fBodyBodyGyroJerkMag.meanFreq = V552)
                              
     
Rename the V1 column in subject_train, using the code
     subject_train <- rename(subject_train, subject= V1)
    
Rename the V1 column in y_train, using the code:
     y_train <- rename(y_train, activity= V1)
Now Create the dataframe traindata using the cbind function.
     traindata <- cbind(subject_train, y_train, x_train_renamed)
Add a column to traindata to indicate training as the type of data..
traindata <- mutate(traindata, type = "training")

Since subjects for testdata and traindata are mutually exclusive, to merge the test and train data, append them using rbind. 
Before rbinding traindata and testdata, make sure that the columns match.  Also have the columns in order, so the subject, type, and activity are first and the measurements are after.
traindata <- select(traindata, subject, type, activity,tBodyAcc.mean_X: fBodyBodyGyroJerkMag.meanFreq )
testdata <- select(testdata, subject, type, activity, tBodyAcc.mean_X: fBodyBodyGyroJerkMag.meanFreq)
Rbind training and test data.  Call this dataset Measurements.
measurements <- rbind(traindata, testdata)
Examine measurements
The variable activity is coded as an integer from 1 to 6, that corresponds to:
1=”walking”
2 = “walking upstairs”
3= “walking downstairs
4= “sitting”
5 =”standing”
6 = “laying”

A strategy to have descriptive labels for activities is to create separate datasets on each of the six activities using the filter ( ) function, create a separate activity column on each of the activity datasets, and then r bind them to make a dataset with descriptive labels for activity.
walking <- filter(measurements, activity==1)
### Create a new column Activity
walking <- mutate(walking, Activity = "walking")
### Delete V1 column
walking <- select(walking, -activity)
Continue doing this for the next activity
walking_upstairs <- filter(measurements, activity==2)
### Create a new column Activity
walking_upstairs <- mutate(walking_upstairs, Activity = "walking up stairs")
### Delete V1 column
walking_upstairs<- select(walking_upstairs, -activity)
walking_downstairs <- filter(measurements, activity==3)
### Create a new column Activity
walking_downstairs <- mutate(walking_downstairs, Activity = "walking downstairs")
### Delete V1 column
walking_downstairs<- select(walking_downstairs, -activity) 
### Create separate datasets on each of the six activities.                            
sitting <- filter(measurements, activity==4)
### Create a new column Activity
sitting<- mutate(sitting, Activity = "sitting")
### Delete V1 column
sitting<- select(sitting, -activity) 
### Create separate datasets on each of the six activities.
standing <- filter(measurements, activity==5)
### Create a new column Activity
  
standing<- mutate( standing,Activity = "standing")
### Delete V1 column
standing<- select( standing, -activity) 
### Create separate datasets on each of the six activities.
laying <- filter(measurements, activity==6)
  ### Create a new column Activity
  
  laying<- mutate( laying,Activity = "laying")
  ### Delete activity column
  laying<- select( laying, -activity)   .  We now have six datasets, one for each activity.  Now r-bind them.
    measurement_dat<- rbind(walking, walking_upstairs, walking_downstairs, sitting, standing, laying)
Rename the Activity column so all variables are lower case.
dat <- rename(measurement_dat, activity=Activity)
dat is the tidy data set with descriptive variable names.  Step 4 is completed. 
To get to step 5: Group the data by activity and subject.
by_activity_subject <-group_by (dat, activity, subject)
Look at by_activity_subject.
There are 180 activity_group levels.  180 = 6 * 30, where 6 is the number of activities and 30 is the number of subjects.
Use the summarize function to get means of all variables included, by activity and subject.  Call the dataset data1.
data1 <-summarize(by_activity_subject, mean(tBodyAcc.mean_X ), mean(tBodyAcc.mean_Y),
                 mean(tBodyAcc.mean_Z),
                 mean(tBodyAcc.std_X),
                  mean(tBodyAcc.std_Y),
                 mean(tBodyAcc.std_Z),
                  
                  mean(tGravityAcc.mean_X),
                  mean(tGravityAcc.mean_Y),
                  mean(tGravityAcc.mean_Z),
                  mean(tGravityAcc.std_X),
                  mean(tGravityAcc.std_Y),
                  mean(tGravityAcc.std_Z),
                  
                  mean(tBodyAccJerk.mean_X),
                  mean(tBodyAccJerk.mean_Y),
                  mean(tBodyAccJerk.mean_Z),
                  mean(tBodyAccJerk.std_X),
                  mean(tBodyAccJerk.std_Y),
                  mean(tBodyAccJerk.std_Z),
                  
                  
                  mean(tBodyGyro.mean_X),
                 mean(tBodyGyro.mean_Y),
                 mean(tBodyGyro.mean_Z),
                  mean(tBodyGyro.std_X),
                  mean(tBodyGyro.std_Y),
                  mean(tBodyGyro.std_Z),
                  
                  
                 mean(tBodyGyroJerk.mean_X),
                  mean(tBodyGyroJerk.mean_Y),
                  mean(tBodyGyroJerk.mean_Z),
                  mean(tBodyGyroJerk.std_X),
                  mean(tBodyGyroJerk.std_Y),
                  mean(tBodyGyroJerk.std_Z),
                  
                  mean(tBodyAccMag.mean),
                  mean(tBodyAccMag.std),
                  
                  mean(tGravityAccMag.mean),
                  mean(tGravityAccMag.std),
                  
                  mean(tBodyAccJerkMag.mean),
                  mean(tBodyAccJerkMag.std),
                  
                  mean(tBodyGyroMag.mean),
                  mean(tBodyGyroMag.std ),
                  
                  mean(tBodyGyroJerkMag.mean),
                  mean(tBodyGyroJerkMag.std ),
                  
                  mean(fBodyAcc.mean_X),
                  mean(fBodyAcc.mean_Y),
                  mean(fBodyAcc.mean_Z),
                  mean(fBodyAcc.std_X ),
                  mean(fBodyAcc.std_Y),
                  mean(fBodyAcc.std_Z),
                  mean(fBodyAcc.meanFreq_X),
                  mean(fBodyAcc.meanFreq_Y),  
                  mean(fBodyAcc.meanFreq_Z), 
                  
                 mean(fBodyAccJerk.mean_X ),
                  mean(fBodyAccJerk.mean_Y),
                  mean(fBodyAccJerk.mean_Z ),
                  mean(fBodyAccJerk.std_X),
                  mean(fBodyAccJerk.std_Y),
                  mean(fBodyAccJerk.std_Z),
                  mean(fBodyAccJerk.meanFreq_X),
                  mean(fBodyAccJerk.meanFreq_Y),
                  mean(fBodyAccJerk.meanFreq_Z ),
                  
                  mean(fBodyGyro.mean_X),
                  mean(fBodyGyro.mean_Y),
                  mean(fBodyGyro.mean_Z) ,
                  mean(fBodyGyro.std_X) ,
                  mean(fBodyGyro.std_Y ),
                  mean(fBodyGyro.std_Z) ,
                  mean(fBodyGyro.meanFreq_X),
                  mean(fBodyGyro.meanFreq_Y) ,
                  mean(fBodyGyro.meanFreq_Z ),
                  mean(fBodyAccMag.mean) ,
                  mean(fBodyAccMag.std) ,
                  mean(fBodyAccMag.meanFreq),
                  mean(fBodyBodyAccJerkMag.mean),
                  mean(fBodyBodyAccJerkMag.std ),
                  mean(fBodyBodyAccJerkMag.meanFreq),
                  mean(fBodyBodyGyroMag.mean),
                  mean(fBodyBodyGyroMag.std ),
                  mean(fBodyBodyGyroMag.meanFreq),
                  mean(fBodyBodyGyroJerkMag.mean),
                  mean(fBodyBodyGyroJerkMag.std),
                  mean(fBodyBodyGyroJerkMag.meanFreq))

Data1 has 180 observations and 81 variables.





