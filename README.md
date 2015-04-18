# michael1
here is the project of practical machine learning

data1 <- read.csv("D:/pml-training.csv",header=T,stringsAsFactors=FALSE)
data2 <- read.csv("D:/pml-testing.csv",header=T,stringsAsFactors=FALSE)
library(caret)
data_train <-  names(data1) %in% c("new_window", "kurtosis_roll_belt", "kurtosis_picth_belt",
                                   "kurtosis_yaw_belt", "skewness_roll_belt", "skewness_roll_belt.1", "skewness_yaw_belt",
                                   "max_yaw_belt", "min_yaw_belt", "amplitude_yaw_belt", "avg_roll_arm", "stddev_roll_arm",
                                   "var_roll_arm", "avg_pitch_arm", "stddev_pitch_arm", "var_pitch_arm", "avg_yaw_arm",
                                   "stddev_yaw_arm", "var_yaw_arm", "kurtosis_roll_arm", "kurtosis_picth_arm",
                                   "kurtosis_yaw_arm", "skewness_roll_arm", "skewness_pitch_arm", "skewness_yaw_arm",
                                   "max_roll_arm", "min_roll_arm", "min_pitch_arm", "amplitude_roll_arm", "amplitude_pitch_arm",
                                   "kurtosis_roll_dumbbell", "kurtosis_picth_dumbbell", "kurtosis_yaw_dumbbell", "skewness_roll_dumbbell",
                                   "skewness_pitch_dumbbell", "skewness_yaw_dumbbell", "max_yaw_dumbbell", "min_yaw_dumbbell",
                                   "amplitude_yaw_dumbbell", "kurtosis_roll_forearm", "kurtosis_picth_forearm", "kurtosis_yaw_forearm",
                                   "skewness_roll_forearm", "skewness_pitch_forearm", "skewness_yaw_forearm", "max_roll_forearm",
                                   "max_yaw_forearm", "min_roll_forearm", "min_yaw_forearm", "amplitude_roll_forearm",
                                   "amplitude_yaw_forearm", "avg_roll_forearm", "stddev_roll_forearm", "var_roll_forearm",
                                   "avg_pitch_forearm", "stddev_pitch_forearm", "var_pitch_forearm", "avg_yaw_forearm",
                                   "stddev_yaw_forearm", "var_yaw_forearm")
data_train <- data1[!data_train]
for (i in 1:ncol(data_train)){
  if(any(is.na(data_train[,i]))){
    data_train <- data_train[,-i]
  }
}
train <-  createDataPartition(y=data_train$classe,p=0.6,list=FALSE)
data_train <- data_train[,-1]
data_training <- data_train[train,]
data_testing <- data_train[-train,]
data_test <- data2[,names(data2)%in%colnames(data_training)]
library(rpart)
modFit <- rpart(classe~.,data=data_training,method="class")
datapredict <- predict(modFit,data_testing,type="class")
matrix <- confusionMatrix(datapredict,data_testing$classe)
answers <- predict(modFit,data_test,type="class")
answers
