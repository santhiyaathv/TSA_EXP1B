# Ex.No: 1 B                    CONVERSION OF NON STATIONARY TO STATIONARY DATA

## AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Gold Price Prediction.

## ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
   
## PROGRAM:
### Importing the necessary Packages:
```
SANTHIYA B
212224230247
```
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

### Loading the dataset:
```
data=pd.read_csv('Gold Price Prediction.csv')
```
### Convert 'Date' column to datetime format
```
data['Date'] = pd.to_datetime(data['Date'])
```
### Set 'Date' as the index
```
data.set_index('Date', inplace=True)
```
### Create a figure and set of subplots
```
plt.figure(figsize=(12, 10))
```
### Plot 1: Gold Price Today
```
plt.subplot(3, 1, 1)  # 3 rows, 1 column, 1st subplot
plt.plot(data.index, data['Price Today'], label='Gold Price Today', color='blue')
plt.title('Gold Price Today Over Time')
plt.xlabel('Date')
plt.ylabel('Gold Price')
plt.legend()
plt.grid(True)
```
### Plot 2: Twenty Moving Average vs. Fifty Moving Average
```
plt.subplot(3, 1, 2)  # 3 rows, 1 column, 2nd subplot
plt.plot(data.index, data['Twenty Moving Average'], label='20-Day Moving Average', color='orange')
plt.plot(data.index, data['Fifty Day Moving Average'], label='50-Day Moving Average', color='green')
plt.title('20-Day vs 50-Day Moving Averages')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.grid(True)
```
### Plot 3: Volume Over Time
```
plt.subplot(3, 1, 3)  # 3 rows, 1 column, 3rd subplot
plt.bar(data.index, data['Volume '], label='Trading Volume ', color='purple')
plt.title('Trading Volume Over Time')
plt.xlabel('Date')
plt.ylabel('Volume ')
plt.legend()
plt.grid(True)
```
### Adjust layout and show the plots
```
plt.tight_layout()
plt.show()

```

## OUTPUT:
### rading Volume Over Time:
<img width="869" height="275" alt="image" src="https://github.com/user-attachments/assets/838594ad-122b-4c4f-af0b-3f6851e55131" />



### Twenty Moving Average vs. Fifty Moving Average
<img width="873" height="252" alt="image" src="https://github.com/user-attachments/assets/6ac0cb19-2d9e-4838-a890-76dc6b02daed" />

### Gold Price Today


<img width="892" height="295" alt="image" src="https://github.com/user-attachments/assets/853ccea0-5f7d-4dd2-9bb3-ae64912d7ad9" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on Gold Price Prediction
data.
