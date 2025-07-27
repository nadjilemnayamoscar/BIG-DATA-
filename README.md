# NAME: NADJILEM NAYAM OSCAR 
# ID 26518

# BIG-DATA-

# 🚕 Uber Fares Dataset Analysis using Power BI

## 📊 Introduction

This project is part of the course **Introduction to Big Data Analytics (INSY 8413)** and focuses on analyzing the **Uber Fares Dataset** to uncover patterns in fare amounts, ride durations, and operational metrics using **Python** and **Power BI Desktop**.

## 🎯 Objective

To develop a comprehensive and interactive Power BI dashboard by:
- Cleaning and preparing raw Uber data using Python
- Performing exploratory data analysis (EDA)
- Engineering new analytical features
- Visualizing patterns across time, space, and pricing
- Presenting key insights and actionable business recommendations

## 🛠 Tools & Technologies
- Python (Pandas, Matplotlib, Seaborn)
- Power BI Desktop
- GitHub (Documentation & Version Control)

---

## 🗂️ Project Structure


---

## 🧪 Steps Performed

### 1. 🧹 Data Preparation
- Loaded dataset into Pandas
```Python
     import pandas as pd
  
    # Replace the filename with the actual one if different
    df = pd.read_csv('uber_fares.csv')  
    df.head()
```
- Assessed structure, types, and quality
  ```Python
      # Ensure datetime column is parsed
    df_cleaned['pickup_datetime'] = pd.to_datetime(df_cleaned['pickup_datetime'])
    
    # 1. Extract time-based features
    df_cleaned['hour'] = df_cleaned['pickup_datetime'].dt.hour
    df_cleaned['day'] = df_cleaned['pickup_datetime'].dt.day
    df_cleaned['month'] = df_cleaned['pickup_datetime'].dt.month
    df_cleaned['day_of_week'] = df_cleaned['pickup_datetime'].dt.dayofweek  # 0=Monday, 6=Sunday
    
    # 2. Create peak time indicator (rush hours: 7–9 AM and 4–7 PM)
    def peak_hour(hour):
        return 'Peak' if (7 <= hour <= 9) or (16 <= hour <= 19) else 'Off-Peak'
    
    df_cleaned['peak_time'] = df_cleaned['hour'].apply(peak_hour)
  ```    

  # 3. Check the new columns
    df_cleaned[['pickup_datetime', 'hour', 'day', 'month', 'day_of_week', 'peak_time']].head()

```python
      # Check the shape of the dataset
      print("📏 Dataset Shape:", df_cleaned.shape)
      
      # Check column names, data types, and non-null counts
      print("\n🧾 Data Types & Non-Null Counts:")
      print(df_cleaned.info())
      
      # Show descriptive statistics for numeric columns
      print("\n📊 Descriptive Statistics:")
      print(df_cleaned.describe())
      
      # Show number of missing values in each column
      print("\n⚠️ Missing Values in Each Column:")
      print(df_cleaned.isnull().sum())
      
      # Display all column names
      print("\n🧩 List of Columns:")
      print(df_cleaned.columns.tolist())

```
- Cleaned missing and inconsistent values
 ```python
      # Make a copy to keep the original safe
    df_cleaned = df.copy()
    
    # Drop rows with missing essential values
    df_cleaned.dropna(subset=['pickup_datetime', 'pickup_latitude', 'pickup_longitude',
                              'dropoff_latitude', 'dropoff_longitude', 'passenger_count', 'fare_amount'],
                      inplace=True)
    
    # Convert pickup_datetime to datetime format
    df_cleaned['pickup_datetime'] = pd.to_datetime(df_cleaned['pickup_datetime'], errors='coerce')
    
    # Drop any rows where datetime conversion failed
    df_cleaned.dropna(subset=['pickup_datetime'], inplace=True)
    
    # Remove invalid fare amounts (e.g., negative or zero fares)
    df_cleaned = df_cleaned[df_cleaned['fare_amount'] > 0]
    
    # Remove invalid passenger counts (e.g., 0 or too many)
    df_cleaned = df_cleaned[(df_cleaned['passenger_count'] > 0) & (df_cleaned['passenger_count'] <= 6)]
    
    # Drop duplicates
    df_cleaned.drop_duplicates(inplace=True)
    
    # Show new shape after cleaning
    print("✅ Dataset shape after cleaning:", df_cleaned.shape)
    
    # Preview cleaned data
    df_cleaned.head()

  ```
- Exported cleaned dataset as `.csv`
  ```python
        # Save the cleaned dataset as CSV
      df_cleaned.to_csv('uber_cleaned.csv', index=False)
      
      # Download the CSV file to your local machine
      from google.colab import files
      files.download('uber_cleaned.csv')

  ```

### 2. 📈 Exploratory Data Analysis (EDA)
- Descriptive statistics: mean, median, std, quartiles
- Visualizations:
  - Fare distribution (histograms, box plots)
  - Relationships: fare vs distance, fare vs time
- Outlier detection

### 3. 🧠 Feature Engineering
- Extracted:
  - Hour, day, month, and day of week
- Coded peak vs off-peak times
- Encoded categorical features
- Saved enhanced dataset for Power BI

### 4. 📊 Power BI Analysis
- Imported cleaned dataset
- Created visuals for:
  - Hourly, daily, monthly ride patterns
  - Seasonal trends
  - Time series analysis
  - Geographic ride distribution

### 5. 🧭 Dashboard Creation
- Designed interactive dashboard with:
  - Slicers and filters
  - Drill-down charts
  - Professional themes and formatting

---

## 📸 Screenshots

### 🔽 Data Cleaning Process
<img width="1557" height="641" alt="part 1" src="https://github.com/user-attachments/assets/0345f02a-84cf-4642-8014-365da0dd0f78" />


### 📉 EDA Visuals
![Fare Distribution](images/eda_plots/fare_distribution.png)

### 📍 Final Dashboard
![Dashboard](images/dashboard_screenshots/dashboard_final.png)

---

## 📄 Final Report

The final report summarizes:
- Objectives and methodology
- Cleaning and EDA results
- Dashboard explanation
- Key insights and recommendations

👉 [View Report (Markdown)](Uber_Fares_Analysis_Report.md)  
👉 OR [View Presentation (PPTX)](Uber_Fares_Presentation.pptx)

---

## 💡 Key Insights
- 🚨 **High fares are common during peak hours and weekends**
- 🕔 **Evening rides showed increased ride frequency**
- 🌍 **Rides were concentrated in urban zones**
- 📊 **Fare amounts have a strong correlation with distance**

---

## 💼 Recommendations
- Dynamic pricing for peak hours to maximize revenue
- Strategic driver deployment based on hourly trends
- Expand operations in low-demand areas with promotional offers

---

## 📬 Submission

**Instructor:** Eric Maniraguha  
**Email:** [eric.maniraguha@auca.ac.rw](mailto:eric.maniraguha@auca.ac.rw)  
**Deadline:** 🗓️ Friday 25 July, 5:00 PM (before Sabbath begins)

---

## ✅ Authors & Group Info

**Course:** INSY 8413 – Introduction to Big Data Analytics  
**Groups:** A, B, & E  
**Tool Used:** Power BI Desktop  

---

## 🛡️ Academic Integrity

All analyses, visualizations, and insights were generated with originality and in alignment with academic integrity guidelines. Collaboration was limited to discussion only — no code sharing.

---

## 🌟 Thank You!

We hope you enjoy exploring this data story as much as we did analyzing it!



