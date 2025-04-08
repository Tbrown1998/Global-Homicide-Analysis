## Global Homicide Rate Analysis:

## Understanding Trends While Comparing Nigeria & Africa to the Rest of the World

![dh4tiu9ne4911](https://github.com/user-attachments/assets/ac7bc260-b6b2-4dee-a7d4-5269f885b75c)


**Homicide** remains a significant global issue, with stark differences across countries, subregions, and continents. Understanding the scale and pattern of homicides across the world can reveal insights into socio-political stability, public safety, and developmental challenges. However, a comparative and regional perspective especially for Africa and Nigeria is often missing in mainstream data narratives.

---

### 🎯 Project Objectve
To conduct a thorough analysis of global homicide data, with special focus on Nigeria and Africa, comparing their patterns, rates, and trends with other regions around the world.

### Expected Outcomes
- Clear visualization of global homicide distribution
- Insight into regional disparities and socio-economic implications
-  comparative lens to evaluate Nigeria and Africa's performance
-  Data-driven narrative for policy makers and researchers

--- 

## 🧰 Technology Stack

- **Python**  
  - `pandas`, `numpy` – Data Cleaning, Data manipulation  
  - `matplotlib`, `seaborn` – Data visualization
  -  ![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-2.0.0-150458?logo=pandas&logoColor=white) ![Matplotlib](https://img.shields.io/badge/Matplotlib-3.5.0-blue?logo=python&logoColor=white) ![Seaborn](https://img.shields.io/badge/Seaborn-0.11.0-black?logo=python&logoColor=white) 
- **Jupyter Notebook** – For interactive development
- ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)
- **Git & GitHub** – Version control and project showcase


---

## 🧾 Data Source

The dataset is sourced from [Data World Bank](https://data.worldbank.org/indicator/VC.IHR.PSRC.P5).

#### Dataset Overview
- `location:` Country name
- `region:` Continent or macro-region
- `subregion:` Geographical subregion
- `rate:` Homicide rate per 100,000 people
- `count:` Number of homicide cases
- `year:` Year of data record
- `percentage_of_total:` Country's share of global homicide count
- **Note:** Each country’s data corresponds to the most recent available year.

---

## Data Processing Pipeline

```mermaid
graph TD
    A[Raw Data] --> B[Load Data]
    B --> C[Python Cleaning]
    C --> D[Data Exploration]
    D --> E[Key Insights & Findings]
```
---

## 🔍 Analysis Workflow
1. Importing all Libraries & dependenices
   - Load datasets
   - initial exploration
2. Data cleaning
3. Exploratory Data Analysis (EDA)
   - Global Summary
   - Regional & Subregional Insights
   - Nigeria & Africa Focus
   - Distribution Analysis
4. Key Findings

--- 

## Step 1
**Import all dependencies**
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
```
**Loading Datasets & Initial Exploration**
```python
df = pd.read_csv('homicide_by_countries.csv')

#first 10 rows of dataset
df.head(10)

#last 10 rows of dataset
df.tail(10)

#shape of dataset
df.shape

#information about columns, datatypes, general DataFrame
df.info()

#Statistical Summary Of all Numerical Columns
df.describe()

# Statistical Summary Of all Columns
df.describe(include='any')
```
## Step 2
**Data Cleaning**
```python
df['count'].sum()

# Check for missing values
df.isnull().sum()

# convert column type to correct dtype

df.columns
my_list = ['Count', 'Year', 'Rate']
for i in my_list:
    df[i] = df[i].astype(int)
df.info()

# Convert column titles to all lowercase
df.columns = df.columns.str.lower()
df.columns

#Feature Engineering
df['percentage_of_total'] = (df['count'] * 100 / df['count'].sum()).round(2)
df
```

### Step 3 Exploratory Data Analysis (EDA)
**Global Summary (Regional & Subregional Insights)**
```python
# Global homicide count and average rate

global_count = df['count'].sum()
global_avg_rate = df['rate'].mean()
year_range = df['year'].min(), df['year'].max()

print(f"Total Homicide Count: {global_count:,}")
print(f"Global Average Homicide Rate: {global_avg_rate:.2f} Per 100,00 People")
print(f"Year Range: {year_range[0]} to {year_range[1]}")
```
##### Output:
- **Total Homicide Count: 378,846**
- **Global Average Homicide Rate: 6.41 Per 100,00 People**
- **Year Range: 2006 to 2021**

**- Top Countries By Homicide Rate (per 100k people)**
```python
# Top 5 countries by highest homicide rate
top_countries = df.sort_values('rate', ascending=False).head(5)

plt.figure(figsize=(8,6))
sns.barplot(x='rate', y='location', data=top_countries, color='crimson', width=0.5)
plt.title('Top 5 Countries by Homicide Rate', fontsize= 16)
plt.xlabel('Homicide Rate (per 100k)', fontsize= 14)
plt.ylabel('Country', fontsize= 14)
plt.xticks(fontsize=14)
plt.yticks(fontsize=14)
plt.show()
```
![image](https://github.com/user-attachments/assets/22d94e6f-68cc-4aa5-8d4d-207f3f3216d3)



```python
# Top 10 countries by percentage of global homicides

top_countries_by_percentage = df.sort_values('percentage_of_total', ascending=False).head(10)
top_countries_by_percentage
```
![Screenshot (114)](https://github.com/user-attachments/assets/14d0af50-7c90-4ec2-8158-71eef0ecde3b)

```python
# Top 5 countries by homicide count

top_countries_by_count = df.sort_values('count', ascending=False).head(5)
top_countries_by_count

plt.figure(figsize=(10,6))
sns.barplot(x='count', y='location', data=top_countries_by_count, color='crimson')
plt.title('Top 5 Countries by Homicide Count')
plt.xlabel('Homicide Count')
plt.ylabel('Country')
plt.show()
```
![image](https://github.com/user-attachments/assets/8662fbc8-a65b-4e53-af35-a075734b338e)

#### Regional Analysis

```python
# Grouping Regions by homicide count

region_count = df.groupby('region').agg({
    'count': 'sum',
    'rate': 'mean',
    'percentage_of_total': 'sum'
}).sort_values('count', ascending=False)
region_count
```
![Screenshot (115)](https://github.com/user-attachments/assets/7fa6efb1-bc3b-45c3-bfdc-bab79e8da143)

![image](https://github.com/user-attachments/assets/5b9e07c5-38b8-4379-bb69-fb3b4ad51e70)


```python
#Percentage Of Share by Region

region_share = region_stats['percentage_of_total']
region_share

# Pie chart for homicide share by region

plt.figure(figsize=(4, 4))
region_share.plot(kind='pie', autopct='%1.1f%%', colors=sns.color_palette('Reds', len(region_share)))
plt.title('Global Homicide Share by Region')
plt.ylabel('')
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/f3828d26-90b1-45a3-9cae-992fb8371481)

## How Does Nigeria Compare To The Rest Of The World?

```python
#filtering Nigeria rows

nigeria = df[df['location'] == 'Nigeria'].iloc[0]
nigeria

# Getting global average rate and Africa average rate

africa_df = df[df['region'] == 'Africa']
africa_avg_rate = africa_df['rate'].mean()
africa_avg_count = africa_df['count'].mean()
world_avg_rate = df['rate'].mean()

# Visualize Nigeria vs Africa vs World

comparison = pd.DataFrame({
    'Group': ['Nigeria', 'Africa (avg)', 'World (avg)'],
    'Rate': [nigeria['rate'], africa_avg_rate, world_avg_rate],
    'Count': [nigeria['count'], africa_avg_count, df['count'].mean()]
})

plt.figure(figsize=(8,4))
sns.barplot(x='Group', y='Rate', data=comparison, color='crimson')
plt.title('Homicide Rate: Nigeria vs Africa & World')
plt.ylabel('Homicide Rate')
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/03f5313b-b241-4839-839f-43e577d216fc)

```python
# Homicide count comparison

plt.figure(figsize=(8,4))
sns.barplot(x='Group', y='Count', data=comparison, color='crimson')
plt.title('Homicide Count: Nigeria vs Africa & World')
plt.ylabel('Homicide Count')
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/ddffe33a-6ee1-440d-bddc-d6e37822fd97)

### Global Comparisons

```python
# Global Homicide Rate Distribution

plt.figure(figsize=(10, 6))
sns.histplot(df['rate'], kde=True, color='crimson')
plt.title('Distribution of Homicide Rates Globally')
plt.xlabel('Homicide Rate (per 100k)')
plt.ylabel('Frequency')
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/7b228109-86e3-44c5-ad4e-f53297439dca)

```python
# Plotting homicide rate over years globally

plt.figure(figsize=(10,6))
sns.lineplot(data=df.groupby('year')['rate'].mean(), color='crimson')
plt.title('Average Homicide Rate by Year (Global)')
plt.xlabel('Year')
plt.ylabel('Average Homicide Rate (per 100k)')
plt.tight_layout()
plt.show()

```
![image](https://github.com/user-attachments/assets/565daf3d-6a35-4e17-a774-0acb2b386706)

--- 

## 📌 Key Findings
### 🌍 Global Perspective
- Latin America dominates the top list of countries by homicide rate and count
- Sub-Saharan Africa ranks high in count but not always in rate

### 🇳🇬 Nigeria’s Position
- Nigeria has one of the highest homicide counts in Africa
- The homicide rate is significantly higher than the global average
- Nigeria’s position in global comparison shows it among top contributors to African homicide statistics

### 🌐 Africa vs the World
- Africa's subregions show higher concentration of homicide than global average
- However, countries in Latin America still record higher individual rates
- Africa’s homicide burden is spread across multiple countries rather than concentrated in few

### 📘 Future Recommendations
- Incorporate socio-economic indicators (GDP, unemployment, education levels) to correlate with homicide rates
- Time-series analysis for countries with longer trend records
- Geospatial visualizations using choropleth maps

---

## 📌 About Me
Hi, I'm Oluwatosin Amosu Bolaji, a Data Analyst with strong skills in Python, SQL, Power BI, and Excel. I turn raw data into actionable insights through automation, data storytelling, and visual analytics.

- **💡 Tools & Tech:** **Python** (Pandas, NumPy, Matplotlib, Seaborn) | **SQL** (MsSQL, Postgree, MySQL) | **Microsoft Power BI** | **Microsoft Excel**
- **🔹 Key Skills:** Data wrangling, dashboarding, reporting, and process optimization.
- ![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-2.0.0-150458?logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-1.21.0-013243?logo=numpy&logoColor=white) ![Matplotlib](https://img.shields.io/badge/Matplotlib-3.5.0-blue?logo=python&logoColor=white) ![Seaborn](https://img.shields.io/badge/Seaborn-0.11.0-black?logo=python&logoColor=white) ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white) ![Plotly](https://img.shields.io/badge/Plotly-5.5.0-3F4F75?logo=plotly)
- ![SQL](https://img.shields.io/badge/SQL-Server-red?logo=microsoft-sql-server&logoColor=white) ![MS SQL](https://img.shields.io/badge/Microsoft_SQL_Server-CC2927?logo=microsoft-sql-server&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white)
- ![PowerBI](https://img.shields.io/badge/Power_BI-F2C811?logo=powerbi&logoColor=black) ![DAX](https://img.shields.io/badge/DAX-F2C811?logo=powerbi&logoColor=black) ![Power Query](https://img.shields.io/badge/Power_Query-F2C811?logo=powerbi&logoColor=black)
- ![Excel](https://img.shields.io/badge/Excel-217346?logo=microsoft-excel&logoColor=white)

#### 🚀 **Always learning. Always building. Data-driven to the core.**  

### 📫 **Let’s connect!**  
- 📩 oluwabolaji60@gmail.com
- 🔗 : [LinkedIn](https://www.linkedin.com/in/oluwatosin-amosu-722b88141)
- 🌐 : [My Portfolio](https://www.datascienceportfol.io/oluwabolaji60) 
- 𝕏 : [Twitter/X](https://x.com/thee_oluwatosin?s=21&t=EqoeQVdQd038wlSUzAtQzw)
- 🔗 : [Medium](https://medium.com/@oluwabolaji60)
- 🔗 : [View my Repositories](https://github.com/Tbrown1998?tab=repositories)



