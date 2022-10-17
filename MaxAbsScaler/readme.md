# MaxAbsScaler

Create Dataset
```python
import pandas as pd

# data frame containing the odometer reading (km) and the fuel economy (km/l) of second-hand cars
df_cars = pd.DataFrame([[120000, 11], [250000, 11.5], [175000, 15.8], [350000, 17], [400000, 10]],
                       columns=['odometer_reading', 'fuel_economy'])

df_cars
```
Do the scaling manually
```python
def maximum_absolute_scaling(df):
    # copy the dataframe
    df_scaled = df.copy()
    # apply maximum absolute scaling
    for column in df_scaled.columns:
        df_scaled[column] = df_scaled[column]  / df_scaled[column].abs().max()
    return df_scaled

# call the maximum_absolute_scaling function
df_cars_scaled = maximum_absolute_scaling(df_cars)

df_cars_scaled
```

Using Scikit-Learn
```python
from sklearn.preprocessing import MaxAbsScaler
abs_scaler = MaxAbsScaler()
abs_scaler.fit(df_cars) # kind of train the scaler
# the maximum absolute values calculated by the fit method
abs_scaler.max_abs_ #40000 y 17 
scaled_data = abs_scaler.transform(df_cars) #use the scaler
# store the results in a data frame
df_scaled = pd.DataFrame(scaled_data, columns=df_cars.columns)
# visualize the data frame
df_scaled
```

same result!

#### Recover the data
In order to recover the data we use the inverse_transform method
```python
recover_data = abs_scaler.inverse_transform(df_scaled)
```

### Power

```python
from sklearn.preprocessing import PowerTransformer
scaler = PowerTransformer(method='yeo-johnson')
scaler.fit(df_cars) # kind of train the scaler
# the maximum absolute values calculated by the fit method
scaler.max_abs_ #40000 y 17 
scaled_data = scaler.transform(df_cars) #use the scaler
# store the results in a data frame
df_scaled = pd.DataFrame(scaled_data, columns=df_cars.columns)
# visualize the data frame
df_scaled
```

#### Recover the data
In order to recover the data we use the inverse_transform method
```python
recover_data = scaler.inverse_transform(df_scaled)
```