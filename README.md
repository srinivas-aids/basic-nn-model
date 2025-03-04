# Developing a Neural Network Regression Model

## AIM

To develop a neural network regression model for the given dataset.

## THEORY

First we can take the dataset based on one input value and some mathematical calculaus output value.next define the neaural network model in three layers.first layer have four neaurons and second layer have three neaurons,third layer have two neaurons.the neural network model take inuput and produce actual output using regression.

## Neural Network Model

![6](https://user-images.githubusercontent.com/93427183/187445695-2dcd3c81-a1a6-413d-af10-261940af8697.png)

## DESIGN STEPS

### STEP 1:

Loading the dataset

### STEP 2:

Split the dataset into training and testing

### STEP 3:

Create MinMaxScalar objects ,fit the model and transform the data.

### STEP 4:

Build the Neural Network Model and compile the model.

### STEP 5:

Train the model with the training data.

### STEP 6:

Plot the performance plot

### STEP 7:

Evaluate the model with the testing data.

## PROGRAM:

~~~
```
Developed by: u.srinivas
RegisterNumber:  212221230108

import pandas as pd
from google.colab import auth
import gspread
from google.auth import default

auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
import tensorflow as tf
tf.__version__

worksheet = gc.open('firstdataset').sheet1
rows = worksheet.get_all_values()


df = pd.DataFrame(rows[1:], columns=rows[0])
df.head(n=10)
df.dtypes
df = df.astype({'X':'float'})
df = df.astype({'Y':'float'})
df.dtypes
X = df[['X']].values
X
Y = df[['Y']].values
Y
X_train,X_test,Y_train,Y_test = train_test_split(X,Y,test_size=0.33,random_state=50)
X_test.shape
X_train
scaler = MinMaxScaler()
scaler.fit(X_train)
X_train_scaled = scaler.transform(X_train)
X_train_scaled


ai_brain = Sequential([
    Dense(2,activation = 'relu'),
    Dense(1)
])
ai_brain.compile(optimizer = 'rmsprop',loss = 'mse')
ai_brain.fit(x = X_train_scaled,y = Y_train,epochs = 20000)
loss_df = pd.DataFrame(ai_brain.history.history)
loss_df.plot()
X_test
X_test_scaled = scaler.transform(X_test)
X_test_scaled
ai_brain.evaluate(X_test_scaled,Y_test)


input = [[110]]
input_scaled = scaler.transform(input)
input_scaled.shape
input_scaled
ai_brain.predict(input_scaled)
~~~
## Dataset Information

![1](https://user-images.githubusercontent.com/93427183/187444868-55f149ae-2084-4355-9cf1-c77be1340fb4.png)


## OUTPUT

### Training Loss Vs Iteration Plot

![2](https://user-images.githubusercontent.com/93427183/187444928-10163abf-d48d-4c69-b993-1ffe11f9659b.png)


### Test Data Root Mean Squared Error

![3](https://user-images.githubusercontent.com/93427183/187444961-2806444c-14ef-41c2-b7d3-28e0db50d566.png)


### New Sample Data Prediction

sample input:


![5](https://user-images.githubusercontent.com/93427183/187445148-1af714ba-be91-4783-8b60-61014138c862.png)


sample output:


![4](https://user-images.githubusercontent.com/93427183/187445220-6bac3735-2a1c-4384-8fc5-e8ea0b9992f2.png)

## RESULT:

Thus a neural network regression model for the given dataset is written and executed successfully.
