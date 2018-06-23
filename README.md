# Data-Preprocessing
Data preprocessing for machine learning using R and python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

#importing data
dataset=pd.read_csv('Data.csv')
dataset
 
X=dataset.iloc[:,:-1].values
X
y=dataset.iloc[:,3].values
y

#missing values
from sklearn.preprocessing import Imputer 
imputer =Imputer(missing_values='NaN',strategy='mean', axis=0)
imputer=imputer.fit(X[:,1:3])
X[:,1:3]=imputer.transform(X[:,1:3])
X

#label encoding
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X=LabelEncoder()
X[:,0]=labelencoder_X.fit_transform(X[:,0])
onehotencoder=OneHotEncoder(categorical_features=[0])
X=onehotencoder.fit_transform(X).toarray()
X
labelencoder_y=LabelEncoder()
y=labelencoder_X.fit_transform(y)


#split data
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=0.2, 
                                                    random_state=0)

#feature scaling
from sklearn.preprocessing import StandardScaler
sc_X= StandardScaler()
X_train=sc_X.fit_transform(X_train)
X_test=sc_X.transform(X_test)
