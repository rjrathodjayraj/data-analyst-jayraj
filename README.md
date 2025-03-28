# data-analyst-jayraj
# Individual Work 1 - Jayraj Rathod (2304652)

## Descriptive Analysis
Water quality and regulatory compliance are essential for urban infrastructure, ensuring public health and environmental sustainability. The City of Vancouver maintains detailed records of operating permits for water systems and water quality reports. These records provide critical insights into permit conditions, regulatory compliance, and the overall quality of operating water systems.

This project involves analyzing data on operating permits for water systems. The dataset consists of 465 entries, each containing:
- Operating permit number
- System address
- Mechanical system type (e.g., building water treatment, cooling water system)
- Current system status (active/inactive)
- Permit renewal date

Additional irrelevant information was also present and addressed during the data cleaning process.

## Step 1: Data Ingestion
The dataset, `rental-standards-current-issues.csv`, was ingested into AWS DataBrew from an S3 bucket named `city-vancouver-dap-jayraj`. AWS DataBrew enables seamless integration with S3, allowing direct imports into data processing environments (Oteng, 2024).

**Process:**
- Selected dataset from S3
- Auto-detected schema using DataBrew
- Configured settings: first row as headers, comma as delimiter
- Saved dataset as `rental-standards-dataset` in DataBrew

![Data stored in S3](fig1.png)

## Step 2: Data Profiling
A profiling job was created to generate summary statistics on the dataset. Data profiling helps assess data quality, completeness, and potential issues before cleaning (Agrawal, 2024).

**Profiling Insights:**
- Distinct values per column
- Missing values identification
- Numeric and categorical distributions

The profiling output was stored in the `databrew-output` folder in S3.

![Data Profiling](fig2.png)

## Step 3: Data Cleaning
Data cleaning was performed using a DataBrew recipe to apply transformations systematically. The following operations were applied:
- Removed rows with missing `Geom` values to ensure valid geolocation data.
- Renamed columns for consistency (e.g., `BUSINESSOPERATOR` → `business_operator`).
- Removed special characters and extra whitespace from `business_operator` and `Street` columns.

The cleaned dataset was saved in S3 under `databrew-output`.

![Data Cleaning Step 1](fig3.png)
![Data Cleaning Step 2](fig4.png)

## Step 4: Data Cataloging
The cleaning recipe was published to AWS DataBrew, ensuring repeatability and auditability (Pradeep-Misra, 2021). This allowed:
- Versioning of cleaning steps
- Easy retrieval of cleaned datasets and transformation history

The final dataset and cleaning recipe were stored in S3 for future use.

![Dataset saved in S3](fig6.png)

## Step 5: Data Summarization
Key insights derived from profiling, cleaning, and transformation:

- **Initial Dataset:** 473 rows, 9 columns
- **Final Dataset:** 465 rows after removing 8 rows with missing `Geom` values
- **Standardization:** Column names updated, special characters removed
- **Data Stored:** Final dataset saved to S3

### Summary of Key Findings:
- **business_operator:** 411 distinct operators; some managing multiple properties.
- **geo_local_area:** Downtown had the highest concentration of properties.
- **total_units:** Property sizes varied from a few units to over 200.
- **Data Quality:** Missing coordinates were identified and addressed.

![Summarized Data](fig7.png)

---
### 📂 Repository Structure
```
📂 aws-water-quality-analysis
│── 📂 data
│   ├── rental-standards-current-issues.csv
│   ├── cleaned-dataset.csv
│── 📂 images
│   ├── fig1.png
│   ├── fig2.png
│   ├── fig3.png
│   ├── fig4.png
│   ├── fig6.png
│   ├── fig7.png
│── 📂 scripts
│   ├── data_ingestion.py
│   ├── data_profiling.py
│   ├── data_cleaning.py
│── README.md
```
### 🔗 References
1. Oteng, M. (2024). AWS DataBrew for Data Ingestion. 
2. Agrawal, R. (2024). Importance of Data Profiling.
3. Pradeep-Misra, S. (2021). Data Cataloging Best Practices.

---
This GitHub repository showcases a structured approach to data ingestion, profiling, cleaning, and cataloging using AWS DataBrew. 🚀
