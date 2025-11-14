# HR Employee Attrition Analysis (Power BI)

This project involves building an interactive dashboard to analyze the root causes of employee attrition (turnover) at IBM. The goal is to provide actionable insights for the Human Resources department to help retain talent.

---

### 📊 Interactive Demo (GIF)

*(Place your 60-90 second screen recording GIF here. Show navigation between pages, clicking on slicers, and hovering over key charts.)*

![HR Dashboard Demo](HR_Dashboard_Demo.gif)

---

### 1. The Challenge: A Single, Denormalized Flat File

The primary challenge was that the raw data was provided as a **single, large, denormalized table** (a "flat file") containing all 35 columns. This structure is highly inefficient for analysis, mixes facts (like Employee ID) with descriptive dimensions (like Department or Job Satisfaction), and leads to slow performance in BI tools.

---

### 2. The Solution: Normalization & Data Modeling

My first and most critical step was to **normalize** this flat file. I architected and built a proper **Star Schema Data Model** from scratch within Power BI to create an optimized and efficient report.

**A) ETL (Power Query):**
* The data was loaded into Power Query for initial cleaning and transformation.
* Key steps included: Handling missing values (`NULLs`), renaming columns for clarity, replacing values, and optimizing data types for the new model.
* This screenshot shows the "Applied Steps" taken within Power Query to prepare the data:

![Power Query Applied Steps](Power_Query.png)

**B) Data Modeling (Building the Star Schema):**
* I identified and separated the single table into a central **Fact Table** (containing quantitative data like Employee Number and Age) and two logical **Dimension Tables** (`Experience&CareerPath` and `Satisfaction&Evaluation`) to describe the data.
* I then established the correct **one-to-many relationships** from the dimensions to the fact table. This optimized model is the "engine" of the report and the foundation for accurate analysis.

![HR Data Model](Data_Model.png)

**C) DAX (Measure Table):**
* A dedicated `Measures_Table` was created to house all DAX calculations.
* This is the **optimization** step: using Measures instead of Calculated Columns ensures the report is fast and scalable, especially with large datasets.
* DAX was used to create critical KPIs (Key Performance Indicators) that were not in the original data, such as:
    * `[Attrition Rate]`
    * `[Attrition Count]`
    * `[AVG Years at Company for Attrition Employee]`

---

### 3. Key Insights Discovered

The final dashboard provides clear answers to the business question:

* **OverTime is the #1 Driver:** Employees who work `OverTime` are significantly more likely to leave.
* **Job Satisfaction Matters:** Employees with "Low" (Level 1) Job Satisfaction have the highest attrition rate (over 36%).
* **The "First 2 Years" are Critical:** The risk of attrition is highest within the first two years of employment and drops significantly afterward.
