# MuseumOfArtwork-Dashboard
# 🖼️ MoMA (Museum of Modern Art) Power BI Dashboard

This Power BI project analyzes the artworks and artists from the Museum of Modern Art (MoMA) using publicly available datasets. It allows users to explore artist demographics, artwork classifications, and current on-view status in MoMA galleries.

---

## 📁 Dataset Overview

The following cleaned datasets are used in this project:

### 1. Artists_Cleaned.csv
- Information about artists, including:
  - Constituent ID (Primary Key)
  - DisplayName (Name of the artist)
  - Nationality, Gender
  - BeginDate (birth year), EndDate (death year if any)
  - Missing values are replaced with "Unknown"

### 2. Artworks_Cleaned.csv
- Each record represents an artwork in the MoMA collection:
  - Title, Artist ID (foreign key to Constituent ID in Artists table)
  - Date, Medium, Classification, Department, Dimensions
  - All empty or null values replaced with "Unknown"

### 3. MoMA_OnView_Cleaned.xlsx
- Artwork exhibition status at MoMA:
  - Title (used to join with `Artworks`)
  - Gallery, On View (Yes/No)
  - Normalized to contain clean "Yes" or "No" values

### 4. MoMA_Data_Dictionary_Cleaned.csv
- Reference file explaining column meanings across the dataset

---

## 🔗 Data Model Relationships

| Relationship | Type |
|--------------|------|
| Artists[Constituent ID] → Artworks[Artist ID] | One-to-Many |
| Artworks[ObjectID] → MoMA_OnView[ObjectID] | One-to-Many |

The relationships enable slicing and filtering visualizations across artists, their works, and exhibition status.

---

## 📊 Power BI Dashboard Features

The Power BI dashboard built on this data includes the following insights and visuals:

### 🎨 Overview KPIs
- ✅ Total number of artworks
- ✅ Total number of unique artists


### 📈 Visuals
- Bar Chart: Artists by Number of Artworks
- Pie Chart: Distribution of Artwork Classifications vs Medium (e.g., Print, Painting)
- Line Chart: Artworks Acquired Over Time
- Map (Optional): Artist Nationality distribution (if country mapping is possible)
- Matrix: List of Artworks Currently on Display with Gallery Info, Exploration With Drill Down, Drill Through

### 🧩 Slicers
- Artist Nationality
- Classification
- Department

---

## 🛠 Tools Used
- Power BI Desktop for modeling and visualization
- Power Query for ETL and data cleaning
- DAX for custom measures and calculations


---

## ⚙️ Measures Used (Sample DAX)
```DAX
Total Artworks = COUNTROWS('Artworks')

Unique Artists = DISTINCTCOUNT('Artists'[DisplayName])

Artworks On View = 
CALCULATE(
    [Total Artworks],
    'MoMA_OnView'[On View] = "Yes"
)

% On View = 
DIVIDE([Artworks On View], [Total Artworks], 0)
