# 🚗 Parking Lot Utilization Analysis Dashboard in Power BI

Welcome to the **Parking Lot Utilization Dashboard** — an advanced Power BI project that analyzes parking trends using card access data. This dashboard tracks real-time occupancy, peak usage patterns, and access group behaviors for efficient parking management.

---

## 📊 Project Overview

This dashboard analyzes parking entry and exit transactions over time to track:

- 🚗 Cumulative active cars in the parking lot  
- 📈 Daily, weekly, and monthly peak usage  
- 🧑‍💼 Access group-based parking trends  
- 📅 Time-based patterns across different calendar periods  

---

## 📁 Dataset Overview (Not Uploaded)

Although the datasets are **not included** in this repository due to privacy and size concerns, here is a detailed explanation of their structure:

### `CardTransaction.csv`

Contains raw transaction data for each card swipe at the parking gate:

- `CardNumber`: Unique identifier for each user card  
- `LotNumber`: Identifier for the parking lot  
- `EntranceTime`: Timestamp of entry  
- `ExitTime`: Timestamp of exit  

### `CardAccessGroupAssignment.csv`

Maps each card to its access group(s):

- `CardNumber`: Unique identifier  
- `AccessGroup`: Role or department assigned to the card (e.g., Staff, Visitor)  

---

## 🧹 Data Preparation (Power Query)

- Converted `EntranceTime` and `ExitTime` columns to `DateTime`  
- Handled missing values:
  - If `EntranceTime` is missing → set to midnight of the exit date  
  - If `ExitTime` is missing → set to 23:59:59 of the entry date  
- Created `ActualEntry` and `ActualExit` columns  
- Calculated `DurationMinutes` as the difference between entry and exit  
- Normalized `AccessGroup` column by splitting multiple groups into separate rows  
- Created `Events` table with +1 (entry) and –1 (exit) records for tracking lot flow  

---

## 🧠 Data Model Design

- Created a `Calendar` table using DAX:
```DAX
Calendar = 
  ADDCOLUMNS(
    CALENDAR(DATE(2021,1,1), DATE(2025,12,31)),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date],"MMM YYYY"),
    "DayOfWeek", FORMAT([Date],"dddd")
  )
