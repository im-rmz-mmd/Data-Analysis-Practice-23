# 👶 Baby Name Trends Dashboard | Power BI Project

A one-page interactive **Power BI** dashboard analyzing U.S. baby name data across states and time.  
It focuses on **birth trends, gender distribution, name popularity**, and **regional patterns**.

---

## ✨ Dashboard Highlights

- **Total Births** with yearly trend  
- **Most Popular Names** by gender  
- **Top Year with highest birth count**  
- **Births by State and Region**  
- **Births by Gender in each Region**

---

## 🧮 KPI Cards – DAX Measures

### 👶 Total Births
```dax
Total Births = SUM(names[Births])
```

### 👦 Most Popular Boy Name
```dax
Most Popular Boy Name = 
CALCULATE(
    FIRSTNONBLANK(names[Name], 1),
    FILTER(
        names,
        names[Gender] = "M" &&
        names[Births] = 
            CALCULATE(
                MAX(names[Births]),
                names[Gender] = "M"
            )
    )
)
```

### 👧 Most Popular Girl Name
```dax
Most Popular Girl Name = 
CALCULATE(
    FIRSTNONBLANK(names[Name], 1),
    FILTER(
        names,
        names[Gender] = "F" &&
        names[Births] = 
            CALCULATE(
                MAX(names[Births]),
                names[Gender] = "F"
            )
    )
)
```

### 🧭 Number of States
```dax
Number of States = DISTINCTCOUNT(names[State])
```

### 📅 Most Popular Year
```dax
Most Popular Year = 
CALCULATE(
    MAX(names[Year]),
    FILTER(
        VALUES(names[Year]),
        CALCULATE(SUM(names[Births])) = 
            CALCULATE(MAXX(VALUES(names[Year]), CALCULATE(SUM(names[Births]))))
    )
)
```

---

## 📊 Visuals Breakdown

### 1. 📈 Line Chart — Births Over Time
- **X:** Year  
- **Y:** SUM(Births)  
- **Legend:** Gender *(optional)*  
✅ *No DAX required*

---

### 2. 📊 Bar Chart — Top Names
- **X:** Name  
- **Y:** SUM(Births)  
- **Slicers:** Year, Gender  
✅ *Simple aggregation*

---

### 3. 🗺️ Map — Births by State
- **Location:** State  
- **Size:** SUM(Births)  
✅ *DAX not needed*

---

### 4. 🧭 Column Chart — Births by Region and Gender
- **X:** Region *(from `regions.csv`)*  
- **Y:** SUM(Births)  
- **Legend:** Gender  
✅ *Requires data model relationship*

---

## 🧱 Data Modeling

Ensure proper relationship:

```text
names[State] → regions[regions]
```

This enables analysis by broader region labels.

---

## 📁 Dataset Files

- `names.csv`: Raw name data including state, year, gender, and number of births.  
- `regions.csv`: Maps each state to its U.S. region.

---

⭐ *If you found this useful, feel free to give the repo a star!*
