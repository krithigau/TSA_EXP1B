# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 22-03-2025

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
data=pd.read_csv('/content/AirPassengers.csv')
data.head()
data['Month']=pd.to_datetime(data['Month']) #data=pd.read_csv("/content/AirPassengers.csv",parse_dates=
data.set_index('Month', inplace=True)
data['passengers_diff']=data['#Passengers']-data['#Passengers'].shift(1)
result = seasonal_decompose(data['#Passengers'], model='additive', period=12)
data['passengers_sea_diff']=result.resid
data['passengers_log'] = np.log(data['#Passengers'])
data['passengers_log_diff']=data['passengers_log']-data['passengers_log'].shift(1)
result = seasonal_decompose (data['passengers_log_diff'].dropna(), model='additive', period=12)
data['passengers_log_seasonal_diff']=result.resid
plt.figure(figsize=(16, 16))
plt.subplot(6, 1, 1)
plt.plot(data['#Passengers'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('No of passengers')
plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of passengers')
plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally djusted No of passengers')
plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log (No of passengers)')
plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff (Log (No of passengers))')
plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], label='Log Transformation and regular Differencing and S')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff (RDiff (Log (No of passengers)))')
plt.tight_layout()
plt.show()
data.plot(kind='line')
```
### OUTPUT:

![Screenshot 2025-03-25 093534](https://github.com/user-attachments/assets/1259c7dc-806e-4034-8241-03af53a2de42)

![Screenshot 2025-03-25 093548](https://github.com/user-attachments/assets/28d3c2b0-84fa-48b4-a14b-730c0dcf3d0d)

![Screenshot 2025-03-25 093604](https://github.com/user-attachments/assets/4c7fc560-adeb-4f02-822a-cad23f7a505e)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
