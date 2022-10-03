# linear-regression

### import libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### Prepare Dataframe with house prices

```python
USAhousing = pd.read_csv('USA_Housing.csv')
# Head method shows us only a few rows
USAhousing.head(6)
USAhousing.info()
USAhousing.describe()
# Columns is an object variable
USAhousing.columns
```

#### Visualization 
Given a dataframe, seaborn.pairplot in the diagonal shows the distribution of each feature.
On the other hand on the rest shows the 2D scatter plot
````python
import matplotlib.pyplot as plt
# kde option shows the dite like a Probability Density Curve
# By default we just see a scatter plot of points
# kde kind of make it continous
sns.pairplot(USAhousing, kind="kde")
plt.show()
# Here we see the Price distribution is normal
sns.distplot(USAhousing['Price'])
plt.show()
USAhousing.corr()
# Here more visually we can see what features are more correlated with the Price
sns.heatmap(USAhousing.corr())
plt.show()
````

```python
# X is a Pandas Dataframe that holds only our features
# We just removed the Price
X = USAhousing[['Avg. Area Income', 'Avg. Area House Age', 'Avg. Area Number of Rooms',
               'Avg. Area Number of Bedrooms', 'Area Population']]
# y is a Pandas Series 
# Just have the information about the prices
y = USAhousing['Price']
from sklearn.model_selection import train_test_split
# We use the SciKit function to create out Train Data and Test Data
# With test Size we say 40% of data is for testing
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.4, random_state=101)
X_test
```
```python
from sklearn.linear_model import LinearRegression
lm = LinearRegression()
lm.fit(X_train,y_train)

```


