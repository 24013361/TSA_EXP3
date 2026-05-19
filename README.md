# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 19/5/26
### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load the dataset
df = pd.read_csv('chennai_temperature_10years.csv')

# Display columns
print("Columns in dataset:", df.columns)

# Convert Date column to datetime
df['Date'] = pd.to_datetime(df['Date'])

# Use Temperature column for ACF
data = df['Temperature'].dropna().values

# Parameters
N = len(data)
lags = range(35)

autocorr_values = []

# Mean and Variance
mean_data = np.mean(data)
variance_data = np.var(data)

# ACF Calculation
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum(
            (data[:-lag] - mean_data) * (data[lag:] - mean_data)
        ) / N

        autocorr_values.append(auto_cov / variance_data)

# Plot ACF
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)

plt.title('Autocorrelation Function (ACF) of Chennai Temperature')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')

plt.grid(True)
plt.show()

```

### OUTPUT:
<img width="689" height="455" alt="Screenshot 2026-05-19 082221" src="https://github.com/user-attachments/assets/9dc71a45-1d83-45c7-adc9-40482e3a6acb" />

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
