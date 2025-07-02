# RDAMP-Sales-Analysis

**Problem Description:**

ACE, a nationwide retail chain, has seen significant sales growth over the past two years. As the company prepares to expand into additional regions and optimize its current operations, senior leadership requires an introductory business intelligence report summarizing key sales performance trends.

*Your role as a newly onboarded data analyst is to perform an initial data exploration and create a report that answers foundational business questions using the attached sales dataset.*

**Business Impact**
This report will serve as a baseline to identify regional performance gaps, customer behavior patterns, and product category profitability, helping the executive team focus on high-impact areas in subsequent strategy sessions. 

*Estimated Time*
*4–6 hours*

**Acceptance Criteria :**
1. Perform data quality assessment (missing values, anomalies, duplicates) 
2. Summarize total sales, revenue, and discount rates by region and segment 
3. Identify top 5 best-selling products and underperforming products by revenue 
4. Provide insights into product categories with highest margins 
5. Analyze sales distribution across Order Mode (Online vs In-Store) 
6. Use your preferred tools in carrying out this exercise (Power BI, Excel, Tableau, Python, etc.) 
7. Present findings and recommendations in a professional report and Include at least 3 visualizations to support key insights.


-----------------START OF ANALYSIS------------------------------------
TOOLS USED : EXCEL & POWERBI 

1. Create a raw copy of dataset to start with exploratory data analysis
2. Review in Excel for missing values , errors or duplicates.
   a. Check Date correct format
       i.  =Istext(B2) : Rows Mixed with Text Format & Date Format
       ii. =TEXT(B2,"MM/DD/YYYY") : Convert text to MM/DD/YYYY
       iii. Convert text to Date Using Date Function
       iv . =Date(year,month,date)
       v. Year :  =RIGHT(D2,4)
       vi. Month : =MID(D2,FIND("/",D2,1)+1,2)
       vii. Date : = =LEFT(D2,FIND("/",D2,1)-1)
   b. Observed Missing Values on Country & Region
       i. Created a unqiue identifier (city-postal) to match store_location and Ace_superstore dataset
       ii. Using VLookup fill country & region :
       iii. =VLOOKUP(F2,'Store locations'!$C:$E,3,FALSE) Anomaly : Region have incorrect data  - Fixed using Vlookup
       iv.  =VLOOKUP(F2,'Store locations'!$C:$D,2,FALSE) Anomaly : Country Missing data - Fixed using Vlookup
       v. Replace Yorkshire & the Humber -> Yorkshire and the Humber
    c. Observed Missing Values on Category
       i. Sort Sub-category A-Z : to group subcategory and filling up missing values in category by comparing the adjacent values
    d. Observed Costprice & SalesPrice with Negative value :
       i. =ABS(N2) =ABS(O2) to reflect correct number and round to 2 decimal places.
    e. Observed discount column with Null values
       i. Replace null values with 0 : No discount given
       ii format to percentage
  
   
4. Load Clean excel file in PowerBI
   
5. Perform further data quality assessment and profil based on entire dateset.
   a. Enable Column quality to check each column for error or missing values.
   b. Enable column profile to check data statistics ( min , max , errors)
   c. Enable Column Distribution to assess duplicate/unique Values.
   d. Correct Formats
     i. Text : Order ID , Order Mode , Customer ID , City, Postal Code , Country, Region , Proeduct ID , Product Name , Category , Sub-Category.
  ii. Date : Order Date
 iii. Fixed Decimal Number : Sales , Cost Price round to 2 decimal places
  iv. Whole Number : Quantity



7.  Summarize total sales, revenue, and discount rates by region and segment 
   i. Tolal Sales = Sum( Ace_Superstore_retail_dataset[Sales] * Ace_Superstore_retail_dataset[Quantity])
   ii.Revenue = 
   
