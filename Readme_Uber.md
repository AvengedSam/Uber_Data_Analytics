# Importing Libraries needed


```python
import pandas as pd
import io
import requests
```


```python
df = pd.read_csv('uber_data.csv')
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>VendorID</th>
      <th>tpep_pickup_datetime</th>
      <th>tpep_dropoff_datetime</th>
      <th>passenger_count</th>
      <th>trip_distance</th>
      <th>pickup_longitude</th>
      <th>pickup_latitude</th>
      <th>RatecodeID</th>
      <th>store_and_fwd_flag</th>
      <th>dropoff_longitude</th>
      <th>dropoff_latitude</th>
      <th>payment_type</th>
      <th>fare_amount</th>
      <th>extra</th>
      <th>mta_tax</th>
      <th>tip_amount</th>
      <th>tolls_amount</th>
      <th>improvement_surcharge</th>
      <th>total_amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:07:55</td>
      <td>1</td>
      <td>2.50</td>
      <td>-73.976746</td>
      <td>40.765152</td>
      <td>1</td>
      <td>N</td>
      <td>-74.004265</td>
      <td>40.746128</td>
      <td>1</td>
      <td>9.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>12.35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:11:06</td>
      <td>1</td>
      <td>2.90</td>
      <td>-73.983482</td>
      <td>40.767925</td>
      <td>1</td>
      <td>N</td>
      <td>-74.005943</td>
      <td>40.733166</td>
      <td>1</td>
      <td>11.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>3.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>15.35</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:31:06</td>
      <td>2</td>
      <td>19.98</td>
      <td>-73.782021</td>
      <td>40.644810</td>
      <td>1</td>
      <td>N</td>
      <td>-73.974541</td>
      <td>40.675770</td>
      <td>1</td>
      <td>54.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>8.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>63.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>3</td>
      <td>10.78</td>
      <td>-73.863419</td>
      <td>40.769814</td>
      <td>1</td>
      <td>N</td>
      <td>-73.969650</td>
      <td>40.757767</td>
      <td>1</td>
      <td>31.5</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>3.78</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>41.62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>5</td>
      <td>30.43</td>
      <td>-73.971741</td>
      <td>40.792183</td>
      <td>3</td>
      <td>N</td>
      <td>-74.177170</td>
      <td>40.695053</td>
      <td>1</td>
      <td>98.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>15.50</td>
      <td>0.3</td>
      <td>113.80</td>
    </tr>
  </tbody>
</table>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>VendorID</th>
      <th>tpep_pickup_datetime</th>
      <th>tpep_dropoff_datetime</th>
      <th>passenger_count</th>
      <th>trip_distance</th>
      <th>pickup_longitude</th>
      <th>pickup_latitude</th>
      <th>RatecodeID</th>
      <th>store_and_fwd_flag</th>
      <th>dropoff_longitude</th>
      <th>dropoff_latitude</th>
      <th>payment_type</th>
      <th>fare_amount</th>
      <th>extra</th>
      <th>mta_tax</th>
      <th>tip_amount</th>
      <th>tolls_amount</th>
      <th>improvement_surcharge</th>
      <th>total_amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:07:55</td>
      <td>1</td>
      <td>2.50</td>
      <td>-73.976746</td>
      <td>40.765152</td>
      <td>1</td>
      <td>N</td>
      <td>-74.004265</td>
      <td>40.746128</td>
      <td>1</td>
      <td>9.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>12.35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:11:06</td>
      <td>1</td>
      <td>2.90</td>
      <td>-73.983482</td>
      <td>40.767925</td>
      <td>1</td>
      <td>N</td>
      <td>-74.005943</td>
      <td>40.733166</td>
      <td>1</td>
      <td>11.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>3.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>15.35</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:31:06</td>
      <td>2</td>
      <td>19.98</td>
      <td>-73.782021</td>
      <td>40.644810</td>
      <td>1</td>
      <td>N</td>
      <td>-73.974541</td>
      <td>40.675770</td>
      <td>1</td>
      <td>54.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>8.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>63.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>3</td>
      <td>10.78</td>
      <td>-73.863419</td>
      <td>40.769814</td>
      <td>1</td>
      <td>N</td>
      <td>-73.969650</td>
      <td>40.757767</td>
      <td>1</td>
      <td>31.5</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>3.78</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>41.62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>5</td>
      <td>30.43</td>
      <td>-73.971741</td>
      <td>40.792183</td>
      <td>3</td>
      <td>N</td>
      <td>-74.177170</td>
      <td>40.695053</td>
      <td>1</td>
      <td>98.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>15.50</td>
      <td>0.3</td>
      <td>113.80</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>1</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:15</td>
      <td>1</td>
      <td>0.50</td>
      <td>-73.990898</td>
      <td>40.750519</td>
      <td>1</td>
      <td>N</td>
      <td>-73.998245</td>
      <td>40.750462</td>
      <td>2</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>1</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:32:41</td>
      <td>1</td>
      <td>3.40</td>
      <td>-74.014488</td>
      <td>40.718296</td>
      <td>1</td>
      <td>N</td>
      <td>-73.982361</td>
      <td>40.752529</td>
      <td>1</td>
      <td>14.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>2.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>16.80</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>1</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:37:23</td>
      <td>1</td>
      <td>9.70</td>
      <td>-73.963379</td>
      <td>40.774097</td>
      <td>1</td>
      <td>N</td>
      <td>-73.865028</td>
      <td>40.770512</td>
      <td>1</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>8.80</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>44.14</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>2</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:09</td>
      <td>1</td>
      <td>0.92</td>
      <td>-73.984901</td>
      <td>40.763111</td>
      <td>1</td>
      <td>N</td>
      <td>-73.970695</td>
      <td>40.759148</td>
      <td>1</td>
      <td>5.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>1.36</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>8.16</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>1</td>
      <td>2016-03-01 06:17:11</td>
      <td>2016-03-01 06:22:00</td>
      <td>1</td>
      <td>1.00</td>
      <td>-73.990685</td>
      <td>40.750473</td>
      <td>1</td>
      <td>N</td>
      <td>-73.980354</td>
      <td>40.754910</td>
      <td>2</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>6.80</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 19 columns</p>
</div>



# Convert the flat file into data model structure


```python
# check the correctness of formats of data
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 100000 entries, 0 to 99999
    Data columns (total 19 columns):
     #   Column                 Non-Null Count   Dtype  
    ---  ------                 --------------   -----  
     0   VendorID               100000 non-null  int64  
     1   tpep_pickup_datetime   100000 non-null  object 
     2   tpep_dropoff_datetime  100000 non-null  object 
     3   passenger_count        100000 non-null  int64  
     4   trip_distance          100000 non-null  float64
     5   pickup_longitude       100000 non-null  float64
     6   pickup_latitude        100000 non-null  float64
     7   RatecodeID             100000 non-null  int64  
     8   store_and_fwd_flag     100000 non-null  object 
     9   dropoff_longitude      100000 non-null  float64
     10  dropoff_latitude       100000 non-null  float64
     11  payment_type           100000 non-null  int64  
     12  fare_amount            100000 non-null  float64
     13  extra                  100000 non-null  float64
     14  mta_tax                100000 non-null  float64
     15  tip_amount             100000 non-null  float64
     16  tolls_amount           100000 non-null  float64
     17  improvement_surcharge  100000 non-null  float64
     18  total_amount           100000 non-null  float64
    dtypes: float64(12), int64(4), object(3)
    memory usage: 14.5+ MB
    


```python
# convert columns of datetime into proper format

df['tpep_pickup_datetime'] = pd.to_datetime(df['tpep_pickup_datetime'])
df['tpep_dropoff_datetime'] = pd.to_datetime(df['tpep_dropoff_datetime'])
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 100000 entries, 0 to 99999
    Data columns (total 19 columns):
     #   Column                 Non-Null Count   Dtype         
    ---  ------                 --------------   -----         
     0   VendorID               100000 non-null  int64         
     1   tpep_pickup_datetime   100000 non-null  datetime64[ns]
     2   tpep_dropoff_datetime  100000 non-null  datetime64[ns]
     3   passenger_count        100000 non-null  int64         
     4   trip_distance          100000 non-null  float64       
     5   pickup_longitude       100000 non-null  float64       
     6   pickup_latitude        100000 non-null  float64       
     7   RatecodeID             100000 non-null  int64         
     8   store_and_fwd_flag     100000 non-null  object        
     9   dropoff_longitude      100000 non-null  float64       
     10  dropoff_latitude       100000 non-null  float64       
     11  payment_type           100000 non-null  int64         
     12  fare_amount            100000 non-null  float64       
     13  extra                  100000 non-null  float64       
     14  mta_tax                100000 non-null  float64       
     15  tip_amount             100000 non-null  float64       
     16  tolls_amount           100000 non-null  float64       
     17  improvement_surcharge  100000 non-null  float64       
     18  total_amount           100000 non-null  float64       
    dtypes: datetime64[ns](2), float64(12), int64(4), object(1)
    memory usage: 14.5+ MB
    


```python
# Cleaning the dataset

# removing the duplicates
df = df.drop_duplicates().reset_index(drop=True)

# Assigning primary key to trip_id column

df['trip_id'] = df.index
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>VendorID</th>
      <th>tpep_pickup_datetime</th>
      <th>tpep_dropoff_datetime</th>
      <th>passenger_count</th>
      <th>trip_distance</th>
      <th>pickup_longitude</th>
      <th>pickup_latitude</th>
      <th>RatecodeID</th>
      <th>store_and_fwd_flag</th>
      <th>dropoff_longitude</th>
      <th>dropoff_latitude</th>
      <th>payment_type</th>
      <th>fare_amount</th>
      <th>extra</th>
      <th>mta_tax</th>
      <th>tip_amount</th>
      <th>tolls_amount</th>
      <th>improvement_surcharge</th>
      <th>total_amount</th>
      <th>trip_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2016-03-01</td>
      <td>2016-03-01 00:07:55</td>
      <td>1</td>
      <td>2.50</td>
      <td>-73.976746</td>
      <td>40.765152</td>
      <td>1</td>
      <td>N</td>
      <td>-74.004265</td>
      <td>40.746128</td>
      <td>1</td>
      <td>9.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>12.35</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2016-03-01</td>
      <td>2016-03-01 00:11:06</td>
      <td>1</td>
      <td>2.90</td>
      <td>-73.983482</td>
      <td>40.767925</td>
      <td>1</td>
      <td>N</td>
      <td>-74.005943</td>
      <td>40.733166</td>
      <td>1</td>
      <td>11.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>3.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>15.35</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2016-03-01</td>
      <td>2016-03-01 00:31:06</td>
      <td>2</td>
      <td>19.98</td>
      <td>-73.782021</td>
      <td>40.644810</td>
      <td>1</td>
      <td>N</td>
      <td>-73.974541</td>
      <td>40.675770</td>
      <td>1</td>
      <td>54.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>8.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>63.80</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>2016-03-01</td>
      <td>2016-03-01 00:00:00</td>
      <td>3</td>
      <td>10.78</td>
      <td>-73.863419</td>
      <td>40.769814</td>
      <td>1</td>
      <td>N</td>
      <td>-73.969650</td>
      <td>40.757767</td>
      <td>1</td>
      <td>31.5</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>3.78</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>41.62</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>2016-03-01</td>
      <td>2016-03-01 00:00:00</td>
      <td>5</td>
      <td>30.43</td>
      <td>-73.971741</td>
      <td>40.792183</td>
      <td>3</td>
      <td>N</td>
      <td>-74.177170</td>
      <td>40.695053</td>
      <td>1</td>
      <td>98.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>15.50</td>
      <td>0.3</td>
      <td>113.80</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



# Creating the Tables

# Datetime Table


```python
# Dropping duplicates of  datetime
datetime_dim = df[['tpep_pickup_datetime', 'tpep_dropoff_datetime']].reset_index(drop=True)

# Extracting the Hours, month, day, year and weekday for pickup time
datetime_dim['pick_hours'] = datetime_dim['tpep_pickup_datetime'].dt.hour
datetime_dim['pick_day'] = datetime_dim['tpep_pickup_datetime'].dt.day
datetime_dim['pick_month'] = datetime_dim['tpep_pickup_datetime'].dt.month
datetime_dim['pick_year'] = datetime_dim['tpep_pickup_datetime'].dt.year
datetime_dim['pick_weekday'] = datetime_dim['tpep_pickup_datetime'].dt.weekday
```


```python
datetime_dim
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tpep_pickup_datetime</th>
      <th>tpep_dropoff_datetime</th>
      <th>pick_hours</th>
      <th>pick_day</th>
      <th>pick_month</th>
      <th>pick_year</th>
      <th>pick_weekday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:07:55</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:11:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:31:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:15</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:32:41</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:37:23</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:09</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>2016-03-01 06:17:11</td>
      <td>2016-03-01 06:22:00</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 7 columns</p>
</div>




```python
# Extracting the Hours, day, moth, year and weekday for dropoff time
datetime_dim['drop_hours'] = datetime_dim['tpep_dropoff_datetime'].dt.hour
datetime_dim['drop_day'] = datetime_dim['tpep_dropoff_datetime'].dt.day
datetime_dim['drop_month'] = datetime_dim['tpep_dropoff_datetime'].dt.month
datetime_dim['drop_year'] = datetime_dim['tpep_dropoff_datetime'].dt.year
datetime_dim['drop_weekday'] = datetime_dim['tpep_dropoff_datetime'].dt.weekday
```


```python
datetime_dim
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tpep_pickup_datetime</th>
      <th>tpep_dropoff_datetime</th>
      <th>pick_hours</th>
      <th>pick_day</th>
      <th>pick_month</th>
      <th>pick_year</th>
      <th>pick_weekday</th>
      <th>drop_hours</th>
      <th>drop_day</th>
      <th>drop_month</th>
      <th>drop_year</th>
      <th>drop_weekday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:07:55</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:11:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:31:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:15</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:32:41</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:37:23</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:09</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>2016-03-01 06:17:11</td>
      <td>2016-03-01 06:22:00</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 12 columns</p>
</div>




```python
# Assigning index to datetime_dim as datetime_id

datetime_dim['datetime_id'] = datetime_dim.index
```


```python
datetime_dim
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tpep_pickup_datetime</th>
      <th>tpep_dropoff_datetime</th>
      <th>pick_hours</th>
      <th>pick_day</th>
      <th>pick_month</th>
      <th>pick_year</th>
      <th>pick_weekday</th>
      <th>drop_hours</th>
      <th>drop_day</th>
      <th>drop_month</th>
      <th>drop_year</th>
      <th>drop_weekday</th>
      <th>datetime_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:07:55</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:11:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:31:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:15</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>99995</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:32:41</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>99996</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:37:23</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>99997</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:09</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>99998</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>2016-03-01 06:17:11</td>
      <td>2016-03-01 06:22:00</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>99999</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 13 columns</p>
</div>




```python
# Ordering the columns in a proper order

datetime_dim = datetime_dim[['datetime_id', 'tpep_pickup_datetime', 'pick_hours', 'pick_day','pick_month', 'pick_year', 'pick_weekday',
                             'tpep_dropoff_datetime', 'drop_hours','drop_day', 'drop_month', 'drop_year', 'drop_weekday']]
```


```python
datetime_dim
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime_id</th>
      <th>tpep_pickup_datetime</th>
      <th>pick_hours</th>
      <th>pick_day</th>
      <th>pick_month</th>
      <th>pick_year</th>
      <th>pick_weekday</th>
      <th>tpep_dropoff_datetime</th>
      <th>drop_hours</th>
      <th>drop_day</th>
      <th>drop_month</th>
      <th>drop_year</th>
      <th>drop_weekday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 00:07:55</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 00:11:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 00:31:06</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>99995</td>
      <td>2016-03-01 06:17:10</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 06:22:15</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>99996</td>
      <td>2016-03-01 06:17:10</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 06:32:41</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>99997</td>
      <td>2016-03-01 06:17:10</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 06:37:23</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>99998</td>
      <td>2016-03-01 06:17:10</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 06:22:09</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>99999</td>
      <td>2016-03-01 06:17:11</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
      <td>2016-03-01 06:22:00</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
      <td>2016</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 13 columns</p>
</div>



# Creating Passanger Count Table


```python
# Dropping duplicates of Passanger Count
passenger_count_dim = df[['passenger_count']].reset_index(drop=True)

# Assigning the index to passanger_count_id and fixing the index
passenger_count_dim['passenger_count_id'] = passenger_count_dim.index
passenger_count_dim = passenger_count_dim[['passenger_count_id', 'passenger_count']]
```


```python
passenger_count_dim
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>passenger_count_id</th>
      <th>passenger_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>99995</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>99996</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>99997</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>99998</td>
      <td>1</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>99999</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 2 columns</p>
</div>



# Creating Trip Distance Table


```python
# Dropping duplicates of trip distance
trip_distance_dim = df[['trip_distance']].reset_index(drop=True)

# Assigning the index to trip_distance id and fixing the index
trip_distance_dim['trip_distance_id'] = trip_distance_dim.index
trip_distance_dim = trip_distance_dim[['trip_distance_id', 'trip_distance']]
```


```python
trip_distance_dim
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>trip_distance_id</th>
      <th>trip_distance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2.90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>19.98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>10.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>30.43</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>99995</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>99996</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>99997</td>
      <td>9.70</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>99998</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>99999</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 2 columns</p>
</div>



# Creating a Rate code table


```python
# Creating a dictionary for rate code table
rate_code_type = {
    1 : "Standard rate",
    2 : "JFK",
    3 : "Newark",
    4 : "Nassau or Westchester",
    5 : "Negotiated fare",
    6 : "Group ride"
}

#Creating a table with above index
# Dropping duplicates of rate_code
rate_code_dim = df[['RatecodeID']].reset_index(drop=True)

# Assigning the index to trip_distance id and fixing the index
rate_code_dim['rate_code_id'] = rate_code_dim.index

#Mapping new index to rate code id
rate_code_dim['rate_code_name'] = rate_code_dim['RatecodeID'].map(rate_code_type)

#Creating a table with new column
rate_code_dim = rate_code_dim[['rate_code_id', 'RatecodeID', 'rate_code_name']]
```


```python
rate_code_dim.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rate_code_id</th>
      <th>RatecodeID</th>
      <th>rate_code_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>Standard rate</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Standard rate</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>Standard rate</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
      <td>Standard rate</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>3</td>
      <td>Newark</td>
    </tr>
  </tbody>
</table>
</div>



# Craeting a Table for Pickup and Drop location


```python
# Pickup Table

# Dropping duplicates and resetting index
pickup_location_dim = df[['pickup_longitude', 'pickup_latitude']].reset_index(drop=True)

# Assigning index to pickup_location id
pickup_location_dim['pickup_location_id'] = pickup_location_dim.index

# creating a pickup table
pickup_location_dim = pickup_location_dim[['pickup_location_id', 'pickup_latitude', 'pickup_longitude']]



# Dropoff Table

# Dropping duplicates and resetting index
dropoff_location_dim = df[['dropoff_longitude', 'dropoff_latitude']].reset_index(drop=True)

# Assigning index to dropoff_location id
dropoff_location_dim['dropoff_location_id'] = dropoff_location_dim.index

# creating a dropoff table
dropoff_location_dim = dropoff_location_dim[['dropoff_location_id', 'dropoff_latitude', 'dropoff_longitude']]


```


```python
pickup_location_dim , dropoff_location_dim
```




    (       pickup_location_id  pickup_latitude  pickup_longitude
     0                       0        40.765152        -73.976746
     1                       1        40.767925        -73.983482
     2                       2        40.644810        -73.782021
     3                       3        40.769814        -73.863419
     4                       4        40.792183        -73.971741
     ...                   ...              ...               ...
     99995               99995        40.750519        -73.990898
     99996               99996        40.718296        -74.014488
     99997               99997        40.774097        -73.963379
     99998               99998        40.763111        -73.984901
     99999               99999        40.750473        -73.990685
     
     [100000 rows x 3 columns],
            dropoff_location_id  dropoff_latitude  dropoff_longitude
     0                        0         40.746128         -74.004265
     1                        1         40.733166         -74.005943
     2                        2         40.675770         -73.974541
     3                        3         40.757767         -73.969650
     4                        4         40.695053         -74.177170
     ...                    ...               ...                ...
     99995                99995         40.750462         -73.998245
     99996                99996         40.752529         -73.982361
     99997                99997         40.770512         -73.865028
     99998                99998         40.759148         -73.970695
     99999                99999         40.754910         -73.980354
     
     [100000 rows x 3 columns])



# Creating Payment Type Table


```python
# Creating index for payment type
payment_type_name = {
    1:"Credit Card",
    2:"Cash",
    3:"No Charge",
    4:"Dispute",
    5:"Unknown",
    6:"Voided Trip"
}

# Dropping duplicates and resetting index
payment_type_dim = df[['payment_type']].reset_index(drop=True)

# Assigning index to payment_type id
payment_type_dim['payment_type_id'] = payment_type_dim.index

# creating a payment_type table
payment_type_dim['payment_type_name'] = payment_type_dim['payment_type'].map(payment_type_name)
payment_type_dim = payment_type_dim[['payment_type_id', 'payment_type', 'payment_type_name']]


```


```python
payment_type_dim
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>payment_type_id</th>
      <th>payment_type</th>
      <th>payment_type_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>99995</td>
      <td>2</td>
      <td>Cash</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>99996</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>99997</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>99998</td>
      <td>1</td>
      <td>Credit Card</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>99999</td>
      <td>2</td>
      <td>Cash</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 3 columns</p>
</div>



# Creating a FACT table

# Joining all the table


```python
fact_table = df.merge(passenger_count_dim, left_on='trip_id', right_on='passenger_count_id') \
             .merge(trip_distance_dim, left_on='trip_id', right_on='trip_distance_id') \
             .merge(rate_code_dim, left_on='trip_id', right_on='rate_code_id') \
             .merge(pickup_location_dim, left_on='trip_id', right_on='pickup_location_id') \
             .merge(dropoff_location_dim, left_on='trip_id', right_on='dropoff_location_id')\
             .merge(datetime_dim, left_on='trip_id', right_on='datetime_id') \
             .merge(payment_type_dim, left_on='trip_id', right_on='payment_type_id') \
             [['trip_id','VendorID', 'datetime_id', 'passenger_count_id',
               'trip_distance_id', 'rate_code_id', 'store_and_fwd_flag', 'pickup_location_id', 'dropoff_location_id',
               'payment_type_id', 'fare_amount', 'extra', 'mta_tax', 'tip_amount', 'tolls_amount',
               'improvement_surcharge', 'total_amount']]

# Not the ideal way to join
```


```python
fact_table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>trip_id</th>
      <th>VendorID</th>
      <th>datetime_id</th>
      <th>passenger_count_id</th>
      <th>trip_distance_id</th>
      <th>rate_code_id</th>
      <th>store_and_fwd_flag</th>
      <th>pickup_location_id</th>
      <th>dropoff_location_id</th>
      <th>payment_type_id</th>
      <th>fare_amount</th>
      <th>extra</th>
      <th>mta_tax</th>
      <th>tip_amount</th>
      <th>tolls_amount</th>
      <th>improvement_surcharge</th>
      <th>total_amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>N</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>9.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>12.35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>N</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>11.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>3.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>15.35</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>N</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>54.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>8.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>63.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>N</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>31.5</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>3.78</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>41.62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>N</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>98.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>15.50</td>
      <td>0.3</td>
      <td>113.80</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99995</th>
      <td>99995</td>
      <td>1</td>
      <td>99995</td>
      <td>99995</td>
      <td>99995</td>
      <td>99995</td>
      <td>N</td>
      <td>99995</td>
      <td>99995</td>
      <td>99995</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>99996</th>
      <td>99996</td>
      <td>1</td>
      <td>99996</td>
      <td>99996</td>
      <td>99996</td>
      <td>99996</td>
      <td>N</td>
      <td>99996</td>
      <td>99996</td>
      <td>99996</td>
      <td>14.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>2.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>16.80</td>
    </tr>
    <tr>
      <th>99997</th>
      <td>99997</td>
      <td>1</td>
      <td>99997</td>
      <td>99997</td>
      <td>99997</td>
      <td>99997</td>
      <td>N</td>
      <td>99997</td>
      <td>99997</td>
      <td>99997</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>8.80</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>44.14</td>
    </tr>
    <tr>
      <th>99998</th>
      <td>99998</td>
      <td>2</td>
      <td>99998</td>
      <td>99998</td>
      <td>99998</td>
      <td>99998</td>
      <td>N</td>
      <td>99998</td>
      <td>99998</td>
      <td>99998</td>
      <td>5.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>1.36</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>8.16</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>99999</td>
      <td>1</td>
      <td>99999</td>
      <td>99999</td>
      <td>99999</td>
      <td>99999</td>
      <td>N</td>
      <td>99999</td>
      <td>99999</td>
      <td>99999</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>6.80</td>
    </tr>
  </tbody>
</table>
<p>100000 rows × 17 columns</p>
</div>




```python
fact_table.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 100000 entries, 0 to 99999
    Data columns (total 17 columns):
     #   Column                 Non-Null Count   Dtype  
    ---  ------                 --------------   -----  
     0   trip_id                100000 non-null  int64  
     1   VendorID               100000 non-null  int64  
     2   datetime_id            100000 non-null  int64  
     3   passenger_count_id     100000 non-null  int64  
     4   trip_distance_id       100000 non-null  int64  
     5   rate_code_id           100000 non-null  int64  
     6   store_and_fwd_flag     100000 non-null  object 
     7   pickup_location_id     100000 non-null  int64  
     8   dropoff_location_id    100000 non-null  int64  
     9   payment_type_id        100000 non-null  int64  
     10  fare_amount            100000 non-null  float64
     11  extra                  100000 non-null  float64
     12  mta_tax                100000 non-null  float64
     13  tip_amount             100000 non-null  float64
     14  tolls_amount           100000 non-null  float64
     15  improvement_surcharge  100000 non-null  float64
     16  total_amount           100000 non-null  float64
    dtypes: float64(7), int64(9), object(1)
    memory usage: 13.7+ MB
    

# Export table to SQL DB


```python
import pandas as pd
import sqlite3
import shutil

# Assuming you have multiple DataFrames (df1, df2, df3) that you want to export

# Establish a connection to the SQLite database
conn = sqlite3.connect('uber_db.db')

# Export
passenger_count_dim.to_sql('passenger_count_dim', conn, index=False, if_exists='replace')
trip_distance_dim.to_sql('trip_distance_dim', conn, index=False, if_exists='replace')
rate_code_dim.to_sql('rate_code_dim', conn, index=False, if_exists='replace')
pickup_location_dim.to_sql('pickup_location_dim', conn, index=False, if_exists='replace')
dropoff_location_dim.to_sql('dropoff_location_dim', conn, index=False, if_exists='replace')
datetime_dim.to_sql('datetime_dim', conn, index=False, if_exists='replace')
payment_type_dim.to_sql('payment_type_dim', conn, index=False, if_exists='replace')
fact_table.to_sql('fact_table', conn, index=False, if_exists='replace')



# Close the database connection
conn.close()

# Create a backup of the database file
shutil.copyfile('uber_db.db', 'uber_db_backup.db')

```




    'uber_db_backup.db'



# Export each table as CSV for Dashboard


```python
import pandas as pd

# Assuming you have multiple DataFrames (passenger_count_dim, trip_distance_dim, rate_code_dim, etc.) that you want to export

# Export each DataFrame to a CSV file
passenger_count_dim.to_csv('passenger_count_dim.csv', index=False)
trip_distance_dim.to_csv('trip_distance_dim.csv', index=False)
rate_code_dim.to_csv('rate_code_dim.csv', index=False)
pickup_location_dim.to_csv('pickup_location_dim.csv', index=False)
dropoff_location_dim.to_csv('dropoff_location_dim.csv', index=False)
datetime_dim.to_csv('datetime_dim.csv', index=False)
payment_type_dim.to_csv('payment_type_dim.csv', index=False)
fact_table.to_csv('fact_table.csv', index=False)
```

# Export new table for data analytics from SQL query


```python
import sqlite3
import pandas as pd

# Establish a connection to the SQLite database
conn = sqlite3.connect('uber_db.db')
cursor = conn.cursor()

# Create the empty `tbl_analytics` table
create_table_query = """
CREATE TABLE IF NOT EXISTS `tbl_analytics` (
    trip_id INTEGER,
    VendorID INTEGER,
    tpep_pickup_datetime TEXT,
    tpep_dropoff_datetime TEXT,
    passenger_count INTEGER,
    trip_distance REAL,
    rate_code_name TEXT,
    pickup_latitude REAL,
    pickup_longitude REAL,
    "dropoff_latitude" REAL,
    "dropoff_longitude" REAL,
    payment_type_name TEXT,
    fare_amount REAL,
    extra REAL,
    mta_tax REAL,
    tip_amount REAL,
    tolls_amount REAL,
    improvement_surcharge REAL,
    total_amount REAL
)
"""
cursor.execute(create_table_query)

# Insert data into the `tbl_analytics` table
insert_query = """
INSERT INTO `tbl_analytics`
SELECT 
    f.trip_id,
    f.VendorID,
    d.tpep_pickup_datetime,
    d.tpep_dropoff_datetime,
    p.passenger_count,
    t.trip_distance,
    r.rate_code_name,
    pick.pickup_latitude,
    pick.pickup_longitude,
    dropoff.dropoff_latitude,
    dropoff.dropoff_longitude,
    pay.payment_type_name,
    f.fare_amount,
    f.extra,
    f.mta_tax,
    f.tip_amount,
    f.tolls_amount,
    f.improvement_surcharge,
    f.total_amount
FROM 
    `fact_table` f
JOIN 
    `datetime_dim` d ON f.datetime_id = d.datetime_id
JOIN 
    `passenger_count_dim` p ON p.passenger_count_id = f.passenger_count_id  
JOIN 
    `trip_distance_dim` t ON t.trip_distance_id = f.trip_distance_id  
JOIN 
    `rate_code_dim` r ON r.rate_code_id = f.rate_code_id  
JOIN 
    `pickup_location_dim` pick ON pick.pickup_location_id = f.pickup_location_id
JOIN 
    `dropoff_location_dim` dropoff ON dropoff.dropoff_location_id = f.dropoff_location_id
JOIN 
    `payment_type_dim` pay ON pay.payment_type_id = f.payment_type_id
"""
cursor.execute(insert_query)

# Commit the changes to the database
conn.commit()

# Read the table into a DataFrame
tbl_analytics = pd.read_sql_query("SELECT * FROM tbl_analytics", conn)

# Export the DataFrame to a CSV file
tbl_analytics.to_csv('tbl_analytics.csv', index=False)

# Close the database connection
conn.close()

```


```python
analytics = pd.read_csv('tbl_analytics.csv')

analytics
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>trip_id</th>
      <th>VendorID</th>
      <th>tpep_pickup_datetime</th>
      <th>tpep_dropoff_datetime</th>
      <th>passenger_count</th>
      <th>trip_distance</th>
      <th>rate_code_name</th>
      <th>pickup_latitude</th>
      <th>pickup_longitude</th>
      <th>dropoff_latitude</th>
      <th>dropoff_longitude</th>
      <th>payment_type_name</th>
      <th>fare_amount</th>
      <th>extra</th>
      <th>mta_tax</th>
      <th>tip_amount</th>
      <th>tolls_amount</th>
      <th>improvement_surcharge</th>
      <th>total_amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:07:55</td>
      <td>1</td>
      <td>2.50</td>
      <td>Standard rate</td>
      <td>40.765152</td>
      <td>-73.976746</td>
      <td>40.746128</td>
      <td>-74.004265</td>
      <td>Credit Card</td>
      <td>9.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>12.35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:11:06</td>
      <td>2</td>
      <td>2.90</td>
      <td>Newark</td>
      <td>40.767925</td>
      <td>-73.983482</td>
      <td>40.733166</td>
      <td>-74.005943</td>
      <td>Cash</td>
      <td>11.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>3.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>15.35</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:31:06</td>
      <td>3</td>
      <td>19.98</td>
      <td>JFK</td>
      <td>40.644810</td>
      <td>-73.782021</td>
      <td>40.675770</td>
      <td>-73.974541</td>
      <td>No Charge</td>
      <td>54.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>8.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>63.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:00:00</td>
      <td>5</td>
      <td>10.78</td>
      <td>Negotiated fare</td>
      <td>40.769814</td>
      <td>-73.863419</td>
      <td>40.757767</td>
      <td>-73.969650</td>
      <td>Dispute</td>
      <td>31.5</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>3.78</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>41.62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>1</td>
      <td>2016-03-01 00:00:00</td>
      <td>2016-03-01 00:07:55</td>
      <td>1</td>
      <td>2.50</td>
      <td>Standard rate</td>
      <td>40.765152</td>
      <td>-73.976746</td>
      <td>40.746128</td>
      <td>-74.004265</td>
      <td>Credit Card</td>
      <td>9.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.05</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>12.35</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99999</th>
      <td>99995</td>
      <td>1</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:15</td>
      <td>1</td>
      <td>0.50</td>
      <td>Standard rate</td>
      <td>40.750519</td>
      <td>-73.990898</td>
      <td>40.750462</td>
      <td>-73.998245</td>
      <td>Cash</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>100000</th>
      <td>99996</td>
      <td>1</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:32:41</td>
      <td>1</td>
      <td>3.40</td>
      <td>Standard rate</td>
      <td>40.718296</td>
      <td>-74.014488</td>
      <td>40.752529</td>
      <td>-73.982361</td>
      <td>Credit Card</td>
      <td>14.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>2.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>16.80</td>
    </tr>
    <tr>
      <th>100001</th>
      <td>99997</td>
      <td>1</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:37:23</td>
      <td>1</td>
      <td>9.70</td>
      <td>Standard rate</td>
      <td>40.774097</td>
      <td>-73.963379</td>
      <td>40.770512</td>
      <td>-73.865028</td>
      <td>Credit Card</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>8.80</td>
      <td>5.54</td>
      <td>0.3</td>
      <td>44.14</td>
    </tr>
    <tr>
      <th>100002</th>
      <td>99998</td>
      <td>2</td>
      <td>2016-03-01 06:17:10</td>
      <td>2016-03-01 06:22:09</td>
      <td>1</td>
      <td>0.92</td>
      <td>Standard rate</td>
      <td>40.763111</td>
      <td>-73.984901</td>
      <td>40.759148</td>
      <td>-73.970695</td>
      <td>Credit Card</td>
      <td>5.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>1.36</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>8.16</td>
    </tr>
    <tr>
      <th>100003</th>
      <td>99999</td>
      <td>1</td>
      <td>2016-03-01 06:17:11</td>
      <td>2016-03-01 06:22:00</td>
      <td>1</td>
      <td>1.00</td>
      <td>Standard rate</td>
      <td>40.750473</td>
      <td>-73.990685</td>
      <td>40.754910</td>
      <td>-73.980354</td>
      <td>Cash</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.3</td>
      <td>6.80</td>
    </tr>
  </tbody>
</table>
<p>100004 rows × 19 columns</p>
</div>




```python

```
