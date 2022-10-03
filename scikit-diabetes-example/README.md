# Diabetes

### Import libraries

```python
import matplotlib.pyplot as plt
import numpy as np
from sklearn import datasets, linear_model
from sklearn.metrics import mean_squared_error, r2_score
```

### Load and explore data

```python
# Load the diabetes dataset
diabetes_X, diabetes_y = datasets.load_diabetes(return_X_y=True)
# We see we have a numpy array
type(diabetes_X)
# We see we have 444 rows (events) and 10 columns (features)
diabetes_X.shape
# Use only one feature
# https://numpy.org/doc/stable/reference/generated/numpy.expand_dims.html
# First colon... keep all raws, 
# Then we define a new dimension and take just the third element
diabetes_X[:, 2].shape # array of all third elements
diabetes_X[:, np.newaxis].shape # (442,1,10)
diabetes_X[:, np.newaxis,2].shape # 442,1 diabetes_X[:, 2][:,np.newaxis]
diabetes_X = diabetes_X[:, np.newaxis, 2]
# Be ready to play until you get what you need

# Split the data into training/testing sets
# For train all until the last 20
diabetes_X_train = diabetes_X[:-20]
# For train the last 20
diabetes_X_test = diabetes_X[-20:]

# Split the targets into training/testing sets, same numbers
diabetes_y_train = diabetes_y[:-20]
diabetes_y_test = diabetes_y[-20:]
```

### Train the model

```python
# Create linear regression object
regr = linear_model.LinearRegression()

# Train the model using the training sets
regr.fit(diabetes_X_train, diabetes_y_train)

```

### Make predictions

```python
# Make predictions using the testing set
diabetes_y_pred = regr.predict(diabetes_X_test)
```


### Have a look to error coefficients

```python
# The coefficients
print("Coefficients: \n", regr.coef_)
# The mean squared error
print("Mean squared error: %.2f" % mean_squared_error(diabetes_y_test, diabetes_y_pred))
# The coefficient of determination: 1 is perfect prediction
print("Coefficient of determination: %.2f" % r2_score(diabetes_y_test, diabetes_y_pred))
```

