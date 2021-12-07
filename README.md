# GRIP: The Sparks Foundation
Task 1: Prediction using Supervised Learning Predict the percentage of marks a student score based upon the number of hours they studied.
# Author: MANJOT SINGH
SUPERVISED MACHINE LEARNING USNING LINEAR REGRESSION

#Import all necessary Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

url ="http://bit.ly/w-data"
s_data = pd.read_csv(url)
print('Data imported successfully')
s_data.head(10)

#Plotting the distribution of scores
s_data.plot(x='Hours', y='Scores',style='o')
plt.title('Hours vs Percentage')
plt.xlabel('Hours Studied')
plt.ylabel('Percentage Score')
plt.show()

# Preparing the data
X=s_data.iloc[:,:-1].values
y=s_data.iloc[:,1].values

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test= train_test_split(X, y,
                                  test_size=0.2, random_state=0)

#Training the algorithm
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, y_train)
print("Training Complete")


#Plotting the regression line
line = regressor.coef_*X+regressor.intercept_
#Plotting the test data
plt.scatter(X,y)
plt.plot(X, line);
plt.show()

#Making Prediction 
print(X_test) #testing the data - in Hours
y_pred = regressor.predict(X_test) #Predicting the scores

#Comparing actual Vs Predicted Data
df = pd.DataFrame({'Actual': y_test, 'Predicted': y_pred})
df

#Testing with our own data
hours = 9.25
test = np.array([hours])
test = test.reshape (-1,1)
own_pred = regressor.predict(test)
print("No of Hours = {}".format(hours))
print("Predicted Score = {}".format(own_pred[0]))

#Evaluating the data
from sklearn import metrics
print('Mean Absolute Error:',
metrics.mean_absolute_error(y_test,y_pre
