# Data-Analysis-using-Pandas-NumPy-Matplotlib-and-Seaborn

## 1. Project Overview
This project focuses on **exploratory data analysis (EDA)** of a GDP per capita dataset containing estimates from IMF, World Bank, and UN.  

We analyze the data to:  
- Inspect dataset structure and summary statistics  
- Handle missing or zero values  
- Perform visualizations (histograms, scatter plots, bar plots, boxplots)  
- Identify and remove outliers  
- Compare estimates across different sources  

This analysis is useful for learners and analysts looking to strengthen their skills in **data cleaning, analysis, and visualization using Python**.

---

## 2. Tools and Libraries Used
The following tools and libraries were used:  
- **Python 3.8+**  
- **Pandas** – for data manipulation and analysis  
- **NumPy** – for numeric operations and handling missing values  
- **Matplotlib / Seaborn** – for data visualization  
- **Jupyter Notebook / Google Colab** – for interactive analysis  

---

## 3. Objectives
The objectives of this project are:  
- Explore the GDP per capita dataset, including inspecting the head, tail, and sample rows  
- Check dataset shape, column data types, and summary statistics  
- Identify missing or zero values and handle them appropriately  
- Perform groupby operations to analyze estimates by region  
- Identify top and bottom countries based on IMF, World Bank, and UN estimates  
- Visualize distributions, correlations, and outliers using histograms, heatmaps, bar plots, scatter plots, and boxplots  
- Remove outliers using IQR method and compare the impact on average estimates  

---
## 🛠️ Skills Demonstrated

During this project, the following skills and techniques were applied:

- **Data Manipulation with Pandas**  
  - Loading CSV files, inspecting data with `.head()`, `.tail()`, `.sample()`, `.shape`, `.info()`, `.describe()`  
  - Handling missing or zero values using `.replace()` and `.fillna()`  
  - Creating new columns and performing row-wise calculations  

- **Data Aggregation and Analysis**  
  - Grouping data by categories using `.groupby()`  
  - Calculating mean, median, min, max, and using `.nlargest()` / `.nsmallest()`  

- **Data Visualization with Matplotlib and Seaborn**  
  - Histograms, scatter plots, bar plots, boxplots, and heatmaps  
  - Identifying correlations between numeric columns  
  - Visualizing distribution and spotting outliers  

- **Outlier Detection and Removal**  
  - Using Interquartile Range (IQR) to identify and filter outliers  

- **Exploratory Data Analysis (EDA)**  
  - Summarizing key statistics  
  - Understanding data distribution and regional differences  
  - Comparing GDP estimates from multiple sources  

- **Python Libraries Used**  
  - Pandas, NumPy, Matplotlib, Seaborn
   
----

## 4. Key Steps & Examples
**Task:** Group the dataset by `UN_Region` and calculate the **average IMF_Estimate** for each region, then sort the results.

### Group by UN_Region and calculate mean IMF_Estimate, then sort

df.groupby("UN_Region")["IMF_Estimate"].mean().sort_values()

<img width="454" height="257" alt="image" src="https://github.com/user-attachments/assets/d44f64eb-9aaf-4fd0-aee6-5927e04db920" />

*Task:** Identify the top 5 countries with the highest **IMF_Estimate** values.

### Return top 5 countries by IMF_Estimate
df.nlargest(5, "IMF_Estimate")
<img width="888" height="199" alt="image" src="https://github.com/user-attachments/assets/1d7dad97-5b76-426c-8fa8-47b77b69b28e" />

**Task:** Identify the 5 countries with the lowest **UN_Estimate** values.

### Return bottom 5 countries by UN_Estimate
df.nsmallest(5, "UN_Estimate")
<img width="903" height="202" alt="image" src="https://github.com/user-attachments/assets/a3b86734-b595-4312-ba2a-407896392b26" />

**Task:** Replace all zero values in the `IMF_Estimate` column with `NaN` to handle them as missing data.

import numpy as np

### Replace 0 with NaN in IMF_Estimate
df["IMF_Estimate"] = df["IMF_Estimate"].replace(0, np.nan)
<img width="898" height="201" alt="image" src="https://github.com/user-attachments/assets/020602ad-26cd-4795-aef2-8a5c29548e67" />


**Task:** Create a new column `avg_worldbank_un` that stores the average of `WorldBank_Estimate` and `UN_Estimate` for each country.

### Calculate row-wise average of WorldBank_Estimate and UN_Estimate
df['avg_worldbank_un'] = df[['WorldBank_Estimate', 'UN_Estimate']].mean(axis=1)

### Display first few rows
df.head()
<img width="1061" height="187" alt="image" src="https://github.com/user-attachments/assets/312a2b15-63a0-4783-b119-b25f72e9a45e" />

**Task:** Fill the `NaN` values in the `IMF_Estimate` column with the previously calculated `avg_worldbank_un`.

### Fill missing IMF_Estimate values with avg_worldbank_un
df["IMF_Estimate"] = df["IMF_Estimate"].fillna(df["avg_worldbank_un"])
<img width="1068" height="210" alt="image" src="https://github.com/user-attachments/assets/7df4e80c-d0ed-46e7-966e-602d05269bc5" />

**Task:** Plot histograms for all numeric columns in the dataset to inspect their distributions.

import matplotlib.pyplot as plt
import seaborn as sns

### Plot histograms for all numeric columns
df.hist(figsize=(10,8))
plt.show()
<img width="864" height="692" alt="image" src="https://github.com/user-attachments/assets/bd19d794-b0a5-44b4-8b4f-9882acc4f4f8" />

## ➤ Correlation Heatmap

**Task:** Visualize the correlation between IMF, UN, and WorldBank GDP estimates using a heatmap.

import matplotlib.pyplot as plt
import seaborn as sns

### Calculate correlation matrix
corr = df[["IMF_Estimate", "UN_Estimate", "WorldBank_Estimate"]].corr()

### Create heatmap
plt.figure(figsize=(9,6))
sns.heatmap(corr, annot=True, fmt=".2f", cmap='GnBu', annot_kws={"size": 12})
plt.show()
<img width="717" height="518" alt="image" src="https://github.com/user-attachments/assets/0fb33ef5-41d8-457d-96c8-fbaf567ae64a" />

**Task:** Create a horizontal bar plot to visualize WorldBank GDP estimates for each UN region.

### Horizontal bar plot
sns.barplot(x="WorldBank_Estimate", y="UN_Region", data=df, errorbar=None)
plt.show()
<img width="681" height="443" alt="image" src="https://github.com/user-attachments/assets/dbbd0ae0-ef00-4178-8ee7-415120ef0fc1" />


**Task:** Create a scatter plot to visualize UN GDP estimates for each UN region.

### Scatter plot of UN_Estimate by UN_Region
df.plot(x='UN_Region', y='UN_Estimate', kind='scatter',
        figsize=(10,6),
        title="Scatter Plot")
plt.show()
<img width="901" height="555" alt="image" src="https://github.com/user-attachments/assets/0a4901fe-90fc-491e-8b9f-363c5cd5f0c4" />

**Task:** Create a boxplot to visualize the distribution of `UN_Estimate` and identify potential outliers

### Boxplot for UN_Estimate
sns.boxplot(x=df["UN_Estimate"])
plt.show()
<img width="654" height="446" alt="image" src="https://github.com/user-attachments/assets/598ba9c4-e05b-4c65-a63b-be1ad5ef3464" />
df[df["UN_Estimate"]>50000].head()
<img width="886" height="196" alt="image" src="https://github.com/user-attachments/assets/3219e385-7451-423d-be0d-bcfb6c345f6c" />






