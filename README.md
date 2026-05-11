# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA

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

# Load dataset
data = pd.read_csv('/content/Video_Games_Sales.csv')

# Convert year column
data['Year_of_Release'] = pd.to_datetime(data['Year_of_Release'], format='%Y', errors='coerce')

# Remove missing values
data = data.dropna(subset=['Year_of_Release', 'Global_Sales'])

# Set index
data.set_index('Year_of_Release', inplace=True)

# Yearly total sales
data = data[['Global_Sales']].resample('YE').sum()

# Replace zero sales to avoid log error
data['Global_Sales'] = data['Global_Sales'].replace(0, 0.01)

# Regular differencing
data['sales_diff'] = data['Global_Sales'].diff()

# Seasonal decomposition
result1 = seasonal_decompose(data['Global_Sales'], model='additive', period=3)
data['sales_sea_diff'] = result1.resid

# Log transform
data['sales_log'] = np.log(data['Global_Sales'])

# Log differencing
data['sales_log_diff'] = data['sales_log'].diff()

# Remove NaN and inf values before decomposition
clean_log_diff = data['sales_log_diff'].replace([np.inf, -np.inf], np.nan).dropna()

# Seasonal decomposition after log diff
result2 = seasonal_decompose(clean_log_diff, model='additive', period=3)

# Add back to dataframe
data.loc[clean_log_diff.index, 'sales_log_seasonal_diff'] = result2.resid

# Plotting
plt.figure(figsize=(16,16))

plt.subplot(6,1,1)
plt.plot(data['Global_Sales'], label='Original')
plt.legend()
plt.title('Original Global Sales')

plt.subplot(6,1,2)
plt.plot(data['sales_diff'], label='Regular Difference')
plt.legend()
plt.title('Regular Differencing')

plt.subplot(6,1,3)
plt.plot(data['sales_sea_diff'], label='Seasonal Adjustment')
plt.legend()
plt.title('Seasonal Adjustment')

plt.subplot(6,1,4)
plt.plot(data['sales_log'], label='Log Transformation')
plt.legend()
plt.title('Log Transformation')

plt.tight_layout()
plt.show()
data.plot(kind='line', figsize=(12,6))
plt.grid(True)
plt.show()

```

### OUTPUT:

ORIGINAL GLOBAL SALES:
<img width="705" height="183" alt="image" src="https://github.com/user-attachments/assets/6b3c345e-9c6b-4bc5-95d2-7e762875f278" />

REGULAR DIFFERENCING:
<img width="744" height="191" alt="image" src="https://github.com/user-attachments/assets/affcb023-89fd-4ee6-8455-13e829803570" />

SEASONAL ADJUSTMENT:
<img width="729" height="188" alt="image" src="https://github.com/user-attachments/assets/096c76ac-988d-42e5-9a23-3a77fc0e828d" />

LOG TRANSFORMATION:
<img width="696" height="191" alt="image" src="https://github.com/user-attachments/assets/1c2f00ee-a519-4699-b0f0-f9da65c7317d" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
