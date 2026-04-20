# Rainfall-Anomaly-Detection-Python-
Python project for detecting rainfall anomalies using rolling statistics and visualisation.
# Rainfall Anomaly Detection

This project uses Python to analyse a small rainfall dataset and detect anomalies using rolling statistics. It demonstrates basic skills in data cleaning, time-series analysis, and visualisation.

## What the project does
- Loads a CSV file with daily rainfall values
- Calculates rolling mean and rolling standard deviation
- Flags days with unusually high or low rainfall
- Plots the results for easy interpretation

## Tools used
- Python
- Pandas
- NumPy
- Matplotlib

## How to run
1. Install the required libraries:
2. Run the script:

## Why I built this
I have worked with hydrological and environmental datasets for many years. This project shows how I can use Python to detect unusual patterns in rainfall data, which is useful for drought monitoring, flood analysis, and water resource planning.
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset (replace with your own CSV if needed)
df = pd.read_csv("rainfall_data.csv")

# Ensure correct types
df["date"] = pd.to_datetime(df["date"])
df = df.sort_values("date")

# Calculate rolling statistics
df["rolling_mean"] = df["rainfall"].rolling(window=7).mean()
df["rolling_std"] = df["rainfall"].rolling(window=7).std()

# Detect anomalies
df["anomaly"] = np.where(
    (df["rainfall"] > df["rolling_mean"] + 2 * df["rolling_std"]) |
    (df["rainfall"] < df["rolling_mean"] - 2 * df["rolling_std"]),
    1,
    0
)

# Plot
plt.figure(figsize=(12, 6))
plt.plot(df["date"], df["rainfall"], label="Daily Rainfall")
plt.plot(df["date"], df["rolling_mean"], label="7-Day Rolling Mean", linestyle="--")
plt.scatter(df[df["anomaly"] == 1]["date"],
            df[df["anomaly"] == 1]["rainfall"],
            color="red", label="Anomaly", zorder=5)
plt.xlabel("Date")
plt.ylabel("Rainfall (mm)")
plt.title("Rainfall Anomaly Detection")
plt.legend()
plt.grid(True)
plt.show()
date,rainfall
2024-01-01,5
2024-01-02,0
2024-01-03,12
2024-01-04,3
2024-01-05,4
2024-01-06,50
2024-01-07,6
2024-01-08,7
2024-01-09,8
2024-01-10,2
2024-01-11,1
2024-01-12,30
2024-01-13,4
2024-01-14,5
