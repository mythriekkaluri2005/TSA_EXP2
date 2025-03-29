# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION

## Name    : E.Mythri
## Reg No. : 212223240034
## Date    : 29-03-2025

### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
### Load the dataset :
```
import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt 
data = pd.read_csv('seattle-weather.csv')
data.head()
```
### Resampling data :
```
data['date'] = pd.to_datetime(data['date'])
data.set_index('date', inplace=True)

resampled_data = data.resample('Y').sum()
resampled_data.head()

resampled_data.index = resampled_data.index.year

resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'date':'Year'},inplace=True)

years = resampled_data['Year'].tolist()
precipitation = resampled_data['precipitation'].tolist()

resampled_data.head()

A - LINEAR TREND ESTIMATION

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, precipitation)]
n = len(years)
b = (n * sum(xy) - sum(precipitation ) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(precipitation ) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]

print(f"Linear Trend: y={a:.2f} + {b:.2f}x")

resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend

resampled_data['precipitation'].plot(kind='line',color='blue',marker='o')
resampled_data['Linear Trend'].plot(kind='line',color='black',linestyle='--')
plt.title("Precipitation with Linear Trend")
plt.xlabel("Year")
plt.ylabel("Precipitation")
plt.legend()
plt.show()


B- POLYNOMIAL TREND ESTIMATION

print(f"\nPolynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")
resampled_data['precipitation'].plot(kind='line',color='blue',marker='o')
resampled_data['Polynomial Trend'].plot(kind='line',color='black',marker='o')
plt.title("Precipitation with Polynomial Trend")
plt.xlabel("Year")
plt.ylabel("Precipitation")
plt.legend()
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION

![image](https://github.com/user-attachments/assets/cc53126c-c85c-4377-bec9-bc4d964db969)


B- POLYNOMIAL TREND ESTIMATION

![image](https://github.com/user-attachments/assets/6017525a-8b58-4b0d-8b19-591f856127a8)


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
