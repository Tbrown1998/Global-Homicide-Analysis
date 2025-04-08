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

## 🧰 Tools Stack

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
- Total Homicide Count: 378,846
- Global Average Homicide Rate: 6.41 Per 100,00 People
- Year Range: 2006 to 2021

##### Top Countries By Homicide Rate (per 100k people)
```python
# Top 5 countries by highest homicide rate
top_countries = df.sort_values('rate', ascending=False).head(5)

plt.figure(figsize=(8,6))
sns.barplot(x='rate', y='location', data=top_countries, color='crimson', width=0.5)
plt.title('Countries With Highest Homicide Rate', fontsize= 16)
plt.xlabel('Homicide Rate (per 100k)', fontsize= 14)
plt.ylabel('Country', fontsize= 14)
plt.xticks(fontsize=14)
plt.yticks(fontsize=14)
plt.show()
```
![image](https://github.com/user-attachments/assets/0d536319-c7ff-4b6d-acfd-9789cd2ed121)


##### Top Countries By Percentage Of Global Homicides & Count
```python
# Top 10 countries by percentage of global homicides

top_countries_by_percentage = df.sort_values('percentage_of_total', ascending=False).head(10)
top_countries_by_percentage
```
**Table:**
![Screenshot (118)](https://github.com/user-attachments/assets/feeabfbc-9ca2-4e0c-9ebc-31d8d5072297)

##### Top Countries By Homicides & Count
```python
# Top 5 countries by homicide count

plt.figure(figsize=(8,6))
sns.barplot(x='count', y='location', data=top_countries_by_count, color='crimson', width=0.5)
plt.title('Top 5 Countries by Homicide Count', fontsize=16)
plt.xlabel('Homicide Count', fontsize=14)
plt.ylabel('Country', fontsize=14)
plt.xticks(fontsize=14)
plt.yticks(fontsize=14)
plt.show()
```
![image](https://github.com/user-attachments/assets/c5042d96-59df-4a3a-9f07-58e974f605e1)

--- 

### 🌍 Regional & Subregional Insights
**Regions with Highest Homicide Count**
```python
# Grouping Regions by homicide count

region_count = df.groupby('region').agg({
    'count': 'sum',
    'rate': 'mean',
    'percentage_of_total': 'sum'
}).sort_values('count', ascending=False)
region_count
```
**Table:**
![Screenshot (119)](https://github.com/user-attachments/assets/8672c626-b9fb-46cd-99c7-b0ff09853ea9)

**Visual:**
![image](https://github.com/user-attachments/assets/b38f4ccf-68a6-4a98-a275-84dceadf431c)


##### Homicide count comparison

```python
#Percentage Of Share by Region

region_share = region_count['percentage_of_total']
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

--- 

### 🇳🇬 How Does Nigeria Compare To The Rest Of The World?

```python
#filtering rows for only Nigeria

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
![image](https://github.com/user-attachments/assets/333aba48-d508-4ecd-b450-bb9ea2c29cda)

##### Homicide count comparison
```python
# Homicide count comparison

plt.figure(figsize=(8,4))
sns.barplot(x='Group', y='Count', data=comparison, color='crimson')
plt.title('Homicide Count: Nigeria vs Africa & World')
plt.ylabel('Homicide Count')
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/c9a09740-6daf-4dd8-9859-6f566ec67544)

---

### 🌐 Global Comparisons
**Global Homicide Rate Distribution**
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
![image](https://github.com/user-attachments/assets/8607fc83-0f4d-473d-8fd5-0cb5d785d06b)

**Homicide Rate Over Years Globally**

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
![image](https://github.com/user-attachments/assets/36f63fd0-375e-4e1a-ad61-901ff7de3a0f)

**Choropleth map showing Homicide Rate per Country**
```python
# Filter the most recent data per country (if multiple years exist)
df_map = df[['location', 'rate', 'year']].dropna()
df_map['year'] = pd.to_numeric(df_map['year'], errors='coerce')
df_map = df_map.sort_values('year', ascending=False).drop_duplicates('location')

# Creating choropleth map
fig = px.choropleth(df_map,
                    locations="location",
                    locationmode="country names",
                    color="rate",
                    hover_name="location",
                    color_continuous_scale="Reds",
                    title="Global Homicide Rate by Country (per 100k)")

fig.update_layout(geo=dict(showframe=False, showcoastlines=False))
fig.show()
```
![newplot](https://github.com/user-attachments/assets/370f37f9-0d43-4d24-90df-a7b75c82ca01)

--- 

![Screenshot (124)](https://github.com/user-attachments/assets/66efb331-f0a1-4234-8e95-09e98e7931f1)


![Screenshot (122)](https://github.com/user-attachments/assets/4003f568-056c-4fa8-b470-ee9bfa31954d)

![Screenshot (123)](https://github.com/user-attachments/assets/aa229699-7304-4705-bf3e-77266db2a2a6)


--- 

## 🔍 Key Findings & Insights

### 🌍 Regional & Subregional Insights
- Top subregions with highest homicide counts include Latin America, Sub-Saharan Africa
- Regions like Western Europe, East Asia show very low rates (per 100k)

Regions like Western Europe, East Asia show very low rates
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

### 📊 Distribution Analysis
- Histogram plotted to show distribution of homicide rates globally
- Kernel Density Estimation (KDE) used to understand the shape of distribution
- Most countries have a rate below 10 per 100k, but a few have extreme outliers

### 📘 Future Recommendations
- Incorporate socio-economic indicators (GDP, unemployment, education levels) to correlate with homicide rates
- Time-series analysis for countries with longer trend records
- Geospatial visualizations using choropleth maps

---

## 📌 About Me
Hi, I'm Oluwatosin Amosu Bolaji, a Data Analyst with strong skills in Python, SQL, Power BI, and Excel. I turn raw data into actionable insights through automation, data storytelling, and visual analytics. My work is rooted in analytical thinking, strong business acumen, and technical expertise. Whether it's uncovering hidden trends, optimizing workflows, or translating data into compelling stories, I bring clarity and direction to data—helping organizations make smarter, faster decisions.

## 💡 Tools & Tech:
- **Python** (Pandas, NumPy, Matplotlib, Seaborn)
- **SQL** (MsSQL, Postgree, MySQL)
- **Microsoft Power BI**
- **Microsoft Excel**
- 🔹 **Key Skills:** Data wrangling, dashboarding, reporting, and process optimization.
- ![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-Server-red?logo=microsoft-sql-server&logoColor=white) ![PowerBI](https://img.shields.io/badge/Power_BI-F2C811?logo=powerbi&logoColor=black) ![Excel](https://img.shields.io/badge/Excel-217346?logo=microsoft-excel&logoColor=white)


#### 🚀 **Always learning. Always building. Data-driven to the core.**  

### 📫 **Let’s connect!**  
- 📩 oluwabolaji60@gmail.com
- 🔗 : [LinkedIn](https://www.linkedin.com/in/oluwatosin-amosu-722b88141)
- 🌐 : [My Portfolio](https://www.datascienceportfol.io/oluwabolaji60) 
- 𝕏 : [Twitter/X](https://x.com/thee_oluwatosin?s=21&t=EqoeQVdQd038wlSUzAtQzw)
- 🔗 : [Medium](https://medium.com/@oluwabolaji60)
- 🔗 : [View my Repositories](https://github.com/Tbrown1998?tab=repositories)



