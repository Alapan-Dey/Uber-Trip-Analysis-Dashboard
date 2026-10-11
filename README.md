# 🚖 Uber Trip Analysis Dashboard | Power BI
 
An interactive, three-page Power BI report that analyses **103,728 Uber trips** across **265 locations** (June, US). It turns raw trip records into answers on booking volume, revenue, trip efficiency, demand by time of day, and the most active pickup/drop-off locations.
 


![Power BI](https://img.shields.io/badge/Tool-Power%20BI-F2C811?logo=powerbi&logoColor=black)
![Data Analysis](https://img.shields.io/badge/Skill-Data%20Analysis-0076A8)
![Dashboard Development](https://img.shields.io/badge/Skill-Dashboard%20Development-6C5CE7)
![DAX](https://img.shields.io/badge/Formula%20Language-DAX-2684FF)
![Data Visualization](https://img.shields.io/badge/Skill-Data%20Visualization-2E8B57)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)


 
---
 
## 📖 Project Overview
 
| | |
|---|---|
| **Objective** | Analyse Uber trip data to understand booking trends, revenue and trip efficiency, and support data-driven decisions on pricing and driver availability |
| **Tool** | Microsoft Power BI (Power Query, DAX, Data Modeling) |
| **Data Volume** | 103,728 trip records · 265 locations |
| **Period** | June (US) |
| **Deliverable** | 3-page interactive dashboard with drill-through, bookmarks and dynamic visuals |
 
---
 
## 🎯 Business Problem
 
Uber stakeholders need a single, interactive view to answer questions such as:
 
- How many trips were booked, and how much revenue did they generate?
- How far and how long do customers travel on average?
- Which days, hours and 10-minute windows have peak demand?
- Which pickup and drop-off locations are the busiest?
- Which vehicle types and payment methods are most popular?

**Expected outcomes**
 
- Identify trends in ride bookings and revenue generation
- Analyse trip efficiency in terms of distance and duration
- Compare booking values and trip patterns across time periods
- Provide insights to optimise pricing models and improve customer satisfaction
---
 
## 🖼️ Dashboard Preview
 
> 📸 **Add your dashboard screenshots in the `images/` folder and update the file names below.**
 
### Page 1: Overview Analysis
![Overview Analysis](/Image/Overview%20Analysis.png)
 
### Page 2: Time Analysis
![Time Analysis](/Image/Time%20Analysis.png)
 
### Page 3: Details Tab
![Details Tab](/Image/Details.png)
 
<!-- Optional: add a short GIF/video demo of drill-through and the reset button -->
<!-- ![Dashboard Demo](images/demo.gif) -->
 
---
 
## 🗂️ Dataset & Data Model
 
### Tables
 
**1. Uber Trip Details (Fact table)**: 103,728 rows. *Grain: one row per trip per customer.*
 
| Column | Description |
|---|---|
| `Trip ID` | Unique identifier for each trip |
| `Pickup Time` | Date and time the customer was picked up |
| `Drop off Time` | Date and time the customer was dropped off |
| `passenger_count` | Number of passengers on the trip |
| `trip_distance` | Total distance of the trip |
| `PULocationID` | Pickup location ID |
| `DOLocationID` | Drop-off location ID |
| `fare_amount` | Total amount paid by the customer |
| `Surge Fee` | Extra amount paid during rush hours |
| `Vehicle` | Type of vehicle booked |
| `Payment_type` | Payment method (Card, Cash, Wallet, etc.) |
 
**2. Location (Dimension table)**: 265 rows
 
| Column | Description |
|---|---|
| `LocationID` | Key used to relate to the fact table |
| `Location` | Pickup / drop-off location name |
| `City` | City name |
 
**3. Calendar (Dimension table)**: built from the `Pickup Time` column (date and time split into separate columns).
 
### Data Model (Star Schema)

![Description of the image](/Image/Model.png)

 
- **Active relationships:** `PULocationID → LocationID` and `Pickup Date → Calendar[Date]`
- **Inactive relationship:** `DOLocationID → LocationID`, activated on demand with `USERELATIONSHIP()` in DAX to calculate drop-off metrics from the same Location table

 
### Calculated Columns Added
 
- **Pickup Date**: extracted from `Pickup Time`
- **Pickup Hour (H M S)**: time portion of `Pickup Time`
- **Trip Type (Day / Night)**: classifies each booking by the time of day it was made
---
 
## 📊 Dashboard Pages & Insights
 
### 🔹 Page 1: Overview Analysis
 
A high-level view of performance with interactive filters.
 
**KPIs**
 
| KPI | Question answered |
|---|---|
| Total Bookings | How many trips were booked? |
| Total Booking Value | What revenue did all bookings generate? |
| Average Booking Value | What is the average revenue per booking? |
| Total Trip Distance | How much distance was covered overall? |
| Average Trip Distance | How far does a customer travel per trip? |
| Average Trip Time | How long does a typical trip last? |
 
**Visuals**
 
- **Dynamic Measure Selector** (disconnected table): lets users switch every chart between *Total Bookings*, *Total Booking Value* and *Total Trip Distance*

- **Booking Analysis**: Breakdown of metrics by Payment Type (Card, Cash, Wallet) and Trip Type (Day/Night).

- **Vehicle Type Grid (Matrix)**: Total Bookings, Total Booking Value, Avg Booking Value and Total Trip Distance per vehicle type, with conditional formatting to flag high and low values
- **Total Bookings by Day**: daily trend, peak and off-peak days
- **Location Analysis**
  - Most frequent pickup point
  - Most frequent drop-off point (uses the inactive relationship)
  - Farthest Trip - Determine the longest trip based on distance travelled
  - Top 5 locations by bookings
  - Analyzes the Most Preferred Vehicle for each location.
 
---
 
### 🔹 Page 2: Time Analysis
 
Understands *when* demand happens, so operations, pricing and driver supply can be planned around it. A **global dynamic measure** controls every visual on the page.
 
| Visual | Purpose |
|---|---|
| **Area chart: by Pickup Time (10-minute bins)** | Spot peak and off-peak demand windows through the day |
| **Line chart: by Day Name (Mon–Sun)** | Compare weekday and weekend demand |
| **Heatmap (Matrix): Hour of day × Day of week** | Highlights the busiest hours on each day using colour scales |
 
---
 
### 🔹 Page 3: Details Tab
 
A granular grid table with key trip fields, built for deep dives.
 
- **Drill-through** from any visual (charts, heatmap) to see the underlying trip records for the selected data point
- **"View Full Data" bookmark** (image button) resets all drill-through filters in one click and returns the full dataset
---
 
## ⚙️ Key Power BI Features Implemented
 
| Feature | Where used |
|---|---|
| Star-schema data modeling | Fact + Location + Calendar tables |
| Active / inactive relationships + `USERELATIONSHIP()` | Pickup vs drop-off location analysis |
| Field Parameter  | Dynamic measure selector across pages |
| Advanced DAX | Most frequent pickup / drop-off location, farthest trip, Top 5 |
| Dynamic titles | Chart headers update with the user's selection |
| Grouping / binning | 10-minute pickup-time bins |
| Conditional formatting | Vehicle matrix and heatmap colour scales |
| Drill-through | Overview / Time pages → Details tab |
| Bookmarks and buttons | Data Details, Clear Filters, View Full Data |
| Tooltips and slicers | Interactive exploration |
 
---
 
## 🛠️ How I Built It
 
1. **Understand the data**: documented the fact table, the dimension table, the grain and the relationships.
2. **Prepare columns**: created `Pickup Date`, `Pickup Hour (H M S)` and `Trip Type (Day/Night)` from `Pickup Time`.
3. **Build the Calendar table** from `Pickup Time` (date and time split into separate parts).
4. **Model relationships**: active `PULocationID` and `Pickup Date` relationships, inactive `DOLocationID` relationship.
5. **Write DAX measures**: core KPIs, most frequent pickup and drop-off location, dynamic measure selector.
6. **Group pickup time** into 10-minute bins for the area chart.
7. **Add dynamic titles**: a title measure per visual so headers follow the selected measure.
8. **Build the heatmap**: matrix of hour × day with a dynamic measure, background and font colour set to the same scale with a mid colour, plus a line chart (axis inverted) to match the matrix row order.
9. **Create drill-through** to the *Details Analysis* page using key columns.
10. **Create the reset bookmark**: with no filters on the Details table, add a **"Show All Unfiltered Data"** bookmark (View → Bookmarks) and attach it to an image button through its Action settings (Type: Bookmark).
---
 
## 💡 Key Insights
 
- In the month of June generating **103.7K**  booking , with an average revenue of per booking **$15.0K**
- Peak demand occurs between **12pm to 6 pm** on Saturday and Sunday , while **1 am to 5 am ** is the quietest period
- **Penn Station/Madison Sq West** is the most frequent pickup point and **Newwark,New Jersey,Queens,The Bronx, ManhattanStaten Island** are the most frequent drop-off point
- **36%** of trips are booked at night vs **64%** during the day
- **Uber Pay** is the most used payment method; **UberX** is the most booked vehicle type
- The farthest trip covered **144.1 miles distance** from **Brooklyn to Queens**
### Business Recommendations
 
- Increase driver availability around peak windows and top pickup locations
- Apply dynamic / surge pricing in high-demand hour and day slots
- Position preferred vehicle types in the locations where they are booked most
---
 
## 🧰 Tech Stack & Skills Demonstrated
 
- **Power BI Desktop**: report design, interactivity, bookmarks, drill-through
- **DAX**: measures, calculated columns, `CALCULATE`, `SWITCH`, `USERELATIONSHIP`, ranking and Top N logic
- **Data Modeling**: star schema, dimension and fact tables, Calendar table, active / inactive relationships
- **Data Analysis**: KPI design, trend, time-pattern and location analysis
- **Dashboard UX**: dynamic titles, slicers, tooltips, reset buttons, conditional formatting
---
 
## 📁 Repository Structure
 
```
Uber-Trip-Analysis/
│
├── Uber_Trip_Analysis.pbix      # Power BI report file
├── data/
│   ├── Uber_Trip_Details.csv    # Fact table
│   └── Location.csv             # Dimension table
├── images/
│   ├── overview_analysis.png
│   ├── time_analysis.png
│   ├── details_tab.png
│   └── data_model.png
├── docs/
│   └── Problem_Statement.docx   # Business requirement
└── README.md
```
 


 
