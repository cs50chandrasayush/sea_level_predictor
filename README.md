# sea_level_predictor

This project is part of the **freeCodeCamp Data Analysis with Python Certification**. It analyzes historical sea level data to predict future trends using linear regression.

## 📊 Project Objective

- **Visualize** historical sea level data from 1880 to 2013.
- **Predict** sea level rise through the year 2050 using:
  - A regression line based on all available data.
  - A regression line based on data from the year 2000 onwards.

## 🧰 Technologies Used

- Python 🐍
- Pandas 🐼
- Matplotlib 📊
- SciPy (linregress) 📈

## 📁 Dataset

- **Source**: [Global Average Absolute Sea Level Change, 1880–2014](https://datahub.io/core/sea-level-rise)
- **File**: `epa-sea-level.csv`

## ⚙️ How It Works

```python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

def draw_plot():
    # Read data from file
    df = pd.read_csv('epa-sea-level.csv')

    # Create scatter plot
    fig, ax = plt.subplots(figsize=(10, 6))
    ax.scatter(df['Year'], df['CSIRO Adjusted Sea Level'])

    # Create first line of best fit
    slope, intercept, _, _, _ = linregress(df['Year'], df['CSIRO Adjusted Sea Level'])
    x_pred = pd.Series(range(1880, 2051))
    y_pred = slope * x_pred + intercept
    ax.plot(x_pred, y_pred, color='red', label='Fit: All Data')

    # Create second line of best fit
    df_recent = df[df['Year'] >= 2000]
    slope_recent, intercept_recent, _, _, _ = linregress(df_recent['Year'], df_recent['CSIRO Adjusted Sea Level'])
    x_recent = pd.Series(range(2000, 2051))
    y_recent = slope_recent * x_recent + intercept_recent
    ax.plot(x_recent, y_recent, color='green', label='Fit: 2000 onwards')

    # Add labels and title
    ax.set_xlabel('Year')
    ax.set_ylabel('Sea Level (inches)')
    ax.set_title('Rise in Sea Level')
    ax.legend()

    # Save plot and return axis
    fig.savefig('sea_level_plot.png')
    return ax
✅ Output
Scatter Plot: Displays historical sea level data.

Red Line: Linear regression based on all data (1880–2013).

Green Line: Linear regression based on data from 2000 onwards.

Saved Plot: sea_level_plot.png
