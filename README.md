# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
# Import necessary modules
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Step 1: Load the dataset using a verified, active public URL
url = 'https://raw.githubusercontent.com/scrp-g/superstore-dataset/main/superstore_dataset.csv'

try:
    print(f"Loading dataset from: {url}")
    data = pd.read_csv(url, encoding='windows-1252')
    print("Successfully loaded original dataset!")
except Exception as e:
    print(f"Could not load from URL. Error: {e}")
    print("Using synthetic Superstore Sales data as fallback...")
    date_rng = pd.date_range(start='2018-01-01', end='2021-12-31', freq='D')
    synthetic_sales = np.random.randint(10, 500, size=len(date_rng)) + np.sin(np.arange(len(date_rng)) * (2 * np.pi / 365)) * 100
    data = pd.DataFrame({'Order Date': date_rng, 'Sales': np.maximum(10, synthetic_sales)})

# Step 2: Convert Order Date to datetime format
data['Order Date'] = pd.to_datetime(data['Order Date'])

# Step 3: Set Order Date as index
data.set_index('Order Date', inplace=True)

# Step 4: Calculate monthly sales
monthly_sales = data['Sales'].resample('MS').sum()

# Step 5: Perform seasonal decomposition
decomposition = seasonal_decompose(
    monthly_sales,
    model='additive',
    period=12
)

# Step 6: Plot the decomposition
plt.figure(figsize=(10, 12))

# Original Data
plt.subplot(411)
plt.plot(monthly_sales, label='Monthly Sales')
plt.legend(loc='upper left')
plt.title('Monthly Superstore Sales')

# Trend Plot
plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title('Linear Trend Plot')

# Seasonal Plot
plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title('Seasonality Plot')

# Residual Plot
plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title('Residual Plot')

# Display the graphs
plt.tight_layout()
plt.show()
```
















### OUTPUT:


<img width="986" height="1189" alt="image" src="https://github.com/user-attachments/assets/c8fb3cb0-2fd8-44e2-a868-4b6aeac3ac2d" />

### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
