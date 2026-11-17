# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 13/13/2026

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

data = pd.read_csv('NVIDIA_STOCK.csv', skiprows=2)

data.columns = ['Date', 'Adj Close', 'Close', 'High', 'Low', 'Open', 'Volume']

data.head()

data['Date'] = pd.to_datetime(data['Date'])

data.set_index('Date', inplace=True)

data['stock_diff'] = data['Close'] - data['Close'].shift(1)

result = seasonal_decompose(data['Close'], model='additive', period=252)

data['stock_sea_diff'] = result.resid

data['stock_log'] = np.log(data['Close'])

data['stock_log_diff'] = data['stock_log'] - data['stock_log'].shift(1)

result = seasonal_decompose(data['stock_log_diff'].dropna(), model='additive', period=252)

data['stock_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Close'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('Stock Price')

plt.subplot(6, 1, 2)
plt.plot(data['stock_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Stock Price')

plt.subplot(6, 1, 3)
plt.plot(data['stock_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Stock Price')

plt.subplot(6, 1, 4)
plt.plot(data['stock_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Stock Price)')

plt.subplot(6, 1, 5)
plt.plot(data['stock_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(Stock Price))')

plt.subplot(6, 1, 6)
plt.plot(data['stock_log_seasonal_diff'], label='Log Transformation and Regular Differencing and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(Stock Price)))')

plt.tight_layout()
plt.show()

data.plot(kind='line')
plt.show()
```

### OUTPUT:


REGULAR DIFFERENCING:
<img width="1392" height="233" alt="image" src="https://github.com/user-attachments/assets/64449891-e7f4-48c9-a8b5-738e90c78d77" />


SEASONAL ADJUSTMENT:
<img width="1388" height="243" alt="image" src="https://github.com/user-attachments/assets/01e51b43-1dd8-475c-88c3-31d9b8fe1a9e" />


LOG TRANSFORMATION:

<img width="1387" height="237" alt="image" src="https://github.com/user-attachments/assets/2d19072e-7c3b-490d-afb5-132734c8cf94" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
