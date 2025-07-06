![image](https://github.com/user-attachments/assets/77a08f3e-9023-4b1b-bed4-fa15fa424b19)
<h1>Ace Superstore Sales Data Dashboard</h1>
TASK-INT001-RDAMP <a href="https://app.powerbi.com/view?r=eyJrIjoiMTQ4NTczMWUtNjAwMy00ZjE0LWJjMDItZDA1NjI4NDY2ODFjIiwidCI6ImUxNjYwMTdmLWFmNTYtNDU2OC05NDg4LTgxNWUzZjZlZGNjNyJ9&pageName=30bc83d1934980295e63"> PowerBI Dashboard Link</a>

Reported By: Joefer Jan Cosio

<h2>Problem Description</h2>
<p>ACE, a nationwide retail chain, has seen significant sales growth over the past two years. As the company prepares to expand into additional regions and optimize its current operations, senior leadership requires an introductory business intelligence report summarizing key sales performance trends.</p>

<h2>Business Impact</h2>
<p>This report will serve as a baseline to identify regional performance gaps, customer behavior patterns, and product category profitability, helping the executive team focus on high-impact areas in subsequent strategy sessions.<p>
   
<h2>Business Criteria</h2>
<ol>
   <li>Clean and validated data</li>
   <li>Summarized total sales, revenue, and discount rates by region and segment </li>
   <li>Identified top 5 best-selling products and underperforming products by revenue </li>
   <li>Provided insights into product categories with highest margins</li>
   <li>Analyzed sales distribution across Order Mode (Online vs In-Store)</li>
   <li>Orgainized findings and recommendations in a professional report and Included at least 3 visualizations to support key insights.</li>
</ol>

<h2>About The data</h2>
<p>Ace Superstore Retail Dataset contain information of orders between Jan 2023 to Dec 2025.</p>

<h2>Dataset Schema</h2>

| Column Name    | Data Type | Description                                                                 |
|----------------|-----------|-----------------------------------------------------------------------------|
| Order ID       | String    | Unique identifier for each order transaction                                |
| Order Date     | Date      | Date when the order was placed (may include past and recent years) mm/dd/yyyy |
| Order Mode     | String    | Channel through which the order was made: “Online” or “In-Store”            |
| Customer ID    | String    | Unique identifier for the customer placing the order                        |
| City           | String    | Customer’s city (some missing values may occur)                             |
| Postal Code    | String    | UK postal code linked to customer’s location                                |
| Country        | String    | Country of the customer (e.g England, Scotland, e.t.c)                      |
| Region         | String    | UK region (e.g., North, South, West); some values may be missing            |
| Product ID     | String    | Unique identifier for each product sold                                     |
| Product Name   | String    | Name/description of the product (may contain missing values)                |
| Category       | String    | Product’s broader classification (e.g., “Food - Spices”)                    |
| Sub-Category   | String    | Detailed product classification (e.g., “Rubs and Seasonings”)               |
| Cost Price     | Float     | Internal cost to the company for each unit of product sold                  |
| Sales          | Float     | Total revenue generated from the sale of each unit of product               |
| Quantity       | Integer   | Number of units sold in the order                                           |
| Discount       | Float     | Discount rate applied to the product, ranging from 0 to 1 (e.g., 0.15 = 15%)|


<h2>TOOLS & TECHNIQUES USED IN ANALYSIS</h2>

  1. EXCEL
     + Data cleaning | String Manipulation | Descriptive Statistics | Data Aggregation         
         > COUNT() , COUNTBLANK() , Istext() , Text() ,Date() , Right() , MID() , FIND() , LEFT() , VLOOKUP() , IF() , ISBLANK() , CONCAT() , MIN() , MAX()
       
         > PIVOT Table
         

  3. POWERBI
        + Data Profiling
           >    Leveraged Column Profile, Column Quality, and Column Distribution for further data assessment and validation.
        + DAX Calculations
          >    Developed calculated columns and measures to support advanced analysis, ranking, filtering, and KPI tracking.
        + KPI Cards with Conditional Formatting
          >   Tracked key performance metrics year-over-year (2025 vs 2024), including:
        + Data Storytelling
           + Audience
               > This dashboard is tailored for key decision-makers, including: Head of Operations, Executive Teams, Senior Leadership, Regional Managers, and Marketing Teams.
               
               > It provides relevant insights aligned with their strategic and operational priorities.
          
           + Visualization Strategy
               > Incorporates a mix of: Time-Series visuals for performance trends over time
               
               > Categorical visuals for comparing segments, products, and regions and highlight regional gaps
               
           + Dashboard Layout Pattern
               > Follows best practices in visual hierarchy using
               
               > "F" Layout for scanning from top-left to bottom-right (emphasizes KPIs and trends)
               
               > "Z" Layout for storytelling flow across summary, breakdown, and detail sections
               
        + Data Visualization Analytics
           + Column Chart
              > Total Revenue By region : highlighting Best & Underperforming region using Rules
           + Column Chart
              > Total Revenue By Product : Highlighting Top5 and Bottom5 using DAX RANKX and Rules
           + Bar Chart
              > Total Revenue By Category : Highlighting Top5 and Bottom5 using DAX RANKX and Rules
           + Bar Chart
              > Total Revenue By Segment : Highlighting Top5 and Bottom5 using DAX RANKX and Rules
           + Donut Chart + Card
              > Total Revenue By Order Mode and total orders.
           + Table Chart
              > Summarize Total Order , Units Sold , %sales , Average Discount , Profit Margin ( weighted ) By region with Totals.
           + Table Chart
              > Identifying Top category , Top Segment , Top Product By Region Using DAX TOPN/RANKX & CALCULATE.
           + Ribbon Chart
              > Revenue Trend Year-on-Year By Region
           + Bar Chart
              > %Count of Order Mode By Region.
           + Scatter Plot
              > Profit Margin Vs Revenue By Category with bubble size representing Total Profit.
           + Area Chart
             >  Profit Margin Year-on-Year Trend

<h2>Data Preparation and Extract-Transform-Load</h2>

1. Create a raw copy of dataset to start with exploratory data analysis
2. Review in Excel for missing values , errors or duplicates.
      > Use Countblank() to check for empty cells
      > use Count() to check for numerical values in `[order_date]` , `[Sales]` , `[Cost price]` ,`[Quantity]` & `[Discount]`
      > Concat `[Order ID]` , `[Order Date]` ,`[City]`,`[Product Name]`,`[Quantity]` to check duplicate orders.
      > Use Min() , Max() to check numerical outliers.
4. Use the following Excel functions to check and clean `[order_date]` column, convert text to date format and find Year,month,date      
      >  =Istext(B2) : Rows Mixed with Text Format & Date Format
      
      >  =TEXT(B2,"MM/DD/YYYY") : Convert text to MM/DD/YYYY
      
      >  =Date(RIGHT(D2,4),MID(D2,FIND("/",D2,1)+1,2),LEFT(D2,FIND("/",D2,1)-1))
      
5. Clean & Fill Missing Values on `[Country]` & `[Region]` using VLOOKUP to lookup correct data using `[Postal Code]` in store_location dataset.
      >  Region = VLOOKUP(F2,'Store locations'!$C:$E,3,FALSE)
      
      >  Country = VLOOKUP(F2,'Store locations'!$C:$D,2,FALSE)
      
      >  Standardize `[Region]` Name by Replacing *Yorkshire & the Humber* -> **Yorkshire and the Humber**
      
6. Clean missing values in `[category]`
      >    Sort `[Sub-category] Alphabetically to group subcategory and fill missing values in category by comparing the adjacent values
      
7. Replace Null values in `[discount]` column
      >    Replace null values with 0 and format as percentage : Assume Null values No discount given      
8. Create new Excel sheet , Copy&Paste the cleaned data and rename `[RDAMP_Task1]` Load Clean excel file in PowerBI
9. Perform further data quality check based on entire dateset.
      >    Enable Column quality to check each column for error or missing values.
      
      >    Enable column profile to check data statistics ( min , max , errors)
      
      >    Enable Column Distribution to assess duplicate/unique Values.
10. Correct Formats
      >    Text : Order ID , Order Mode , Customer ID , City, Postal Code , Country, Region , Proeduct ID , Product Name , Category , Sub-Category.
      
      >    Date : Order Date
      
      >    Fixed Decimal Number : Sales , Cost Price round to 2 decimal places
      
      >    Whole Number : Quantity

11. Create New Column `PriceValue` to flag negative amounts  in `[Sales]` & `[Cost price]` fields without deleting any rows, Can then filter on this column in Power BI to analyse either only `positive values` or to include the `negative values` as required.
12. Create New column `Segment` by splitting `[category]` with Delimiter `“ – “` to optimize main category , `[segment]` with missing values will be replace by `[sub-category]` value
13. Create `_MeasureGroup` to organize all measures.

<h2>Calculated Columns</h2>

| Calculated Columns                   |Formula                                                                                                                                                     |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`[Revenue]`                           | = Ace_Superstore_retail_dataset[Sales] * Ace_Superstore_retail_dataset[Quantity]                                                                           |
|`[Unit Profit]`                       | = Ace_Superstore_retail_dataset[Sales] - Ace_Superstore_retail_dataset[Cost Price]                                                                         |
|`[Total Profit]`                      | = (Ace_Superstore_retail_dataset[Sales] - Ace_Superstore_retail_dataset[Cost Price]) * Ace_Superstore_retail_dataset[Quantity]                             | 
|`[Total Cost]`                        | = Ace_Superstore_retail_dataset[Cost Price] * Ace_Superstore_retail_dataset[Quantity]                                                                      |
|`[Profit Margin (Unweighted)]`        | = (Ace_Superstore_retail_dataset[Sales]-Ace_Superstore_retail_dataset[Cost Price]) / Ace_Superstore_retail_dataset[Sales]                                  |

<h2>Calculated Measures</h2>

| Calculated Measures                   |Formula                                                                                                                                                     |
|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`[Average Discount]`                  |  = AVERAGE(Ace_Superstore_retail_dataset[Discount])                                                                                                         |
|`[Average Order]`                     |  = Average(Ace_Superstore_retail_dataset[Quantity])                                                                                                         |         
|`[Total Orders]`                      |  = COUNT(Ace_Superstore_retail_dataset[Order ID])                                                                                                           |      
|`[Total Units Sold]`                  |  = SUM(Ace_Superstore_retail_dataset[Quantity])                                                                                                             |      
|`[Total Revenue]`                     |  = SUM(Ace_Superstore_retail_dataset[Revenue])                                                                                                              |    
|`Profit Margin (Weighted)`            |  = ( (SUM(Ace_Superstore_retail_dataset[Revenue]) - SUM(Ace_Superstore_retail_dataset[Total Cost])) / sum(Ace_Superstore_retail_dataset[Revenue]) )         |    

<h2>Calculated Measures (TopN/BottomN)</h2>

| Calculated Measures (Ranking)                          |Formula                                                                                                                                                      |
|--------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TopN Product By Total Revenue                          | =                                                                                                                                                           |
|                                                        |   VAR RankingContext = VALUES ( Ace_Superstore_retail_dataset[Product Name] )
|                                                        |   RETURN
|                                                        |   CALCULATE(
|                                                        |   [Total Revenue],
|                                                        |  TOPN ( 1, ALL ( Ace_Superstore_retail_dataset[Product Name] ), [Total Revenue]),
|                                                        |  RankingContext)
| TopN Category By Total Revenue                         | =                                                                                                                                                           |
|                                                        |  VAR RankingContext = VALUES ( Ace_Superstore_retail_dataset[Category] )
|                                                        |  RETURN
|                                                        |  CALCULATE(
|                                                        |  [Total Revenue],
|                                                        |  TOPN ( 1, ALL ( Ace_Superstore_retail_dataset[Category] ), [Total Revenue]),
|                                                        |  RankingContext)
| TopN Segment  By Total Revenue                         | =                                                                                                                                                           |
|                                                        |  VAR RankingContext = VALUES ( Ace_Superstore_retail_dataset[Segment] )
|                                                        |  RETURN
|                                                        |   CALCULATE(
|                                                        |  [Total Revenue],
|                                                        |  TOPN ( 1, ALL ( Ace_Superstore_retail_dataset[Segment] ), [Total Revenue]),
|                                                        |  RankingContext)                                         
| TopN & BottomN ProductName By Total Revenue            | =                                                                                                                                                           |
|                                                        |  VAR _rank_top =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Product Name] ) ), [Total Revenue],, DESC, DENSE )
|                                                        |  VAR _rank_bottom =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Product Name] ) ), [Total Revenue],, ASC, DENSE )
|                                                        |  VAR _result =
|                                                        |  IF (
|                                                        |  _rank_top <= 5,
|                                                        |  [Total Revenue],
|                                                        |  IF ( _rank_bottom <= 5, [Total Revenue], BLANK () ) )
|                                                        |  RETURN
|                                                        |  _result                                                                 
| TopN & BottomN Category By Total Revenue               | =                                                                                                                                                           |
|                                                        |  VAR _rank_top =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Category] ) ), [Total Revenue],, DESC, DENSE )
|                                                        |  VAR _rank_bottom =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Category] ) ), [Total Revenue],, ASC, DENSE )
|                                                        |  VAR _result =
|                                                        |  IF (
|                                                        |  _rank_top <= 5,
|                                                        |  [Total Revenue],
|                                                        |  IF ( _rank_bottom <= 5, [Total Revenue], BLANK () ) )
|                                                        |  RETURN
|                                                        |  _result 
| TopN & BottomN Segment By Total Revenue                | =                                                                                                                                                           |
|                                                        |  VAR _rank_top =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Segment] ) ), [Total Revenue],, DESC, DENSE )
|                                                        |  VAR _rank_bottom =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Segment] ) ), [Total Revenue],, ASC, DENSE )
|                                                        |  VAR _result =
|                                                        |  IF (
|                                                        |  _rank_top <= 5,
|                                                        |  [Total Revenue],
|                                                        |  IF ( _rank_bottom <= 5, [Total Revenue], BLANK () ) )
|                                                        |  RETURN
|                                                        |  _result                                                                 
| TopN & BottomN Category By Profit Margin               | =                                                                                                                                                           |
|                                                        |  VAR _rank_top =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Category] ) ), [Profit Margin (Weighted)],, DESC, DENSE )
|                                                        |  VAR _rank_bottom =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Category] ) ), [Profit Margin (Weighted)],, ASC, DENSE )
|                                                        |  VAR _result =
|                                                        |  IF (
|                                                        |  _rank_top <= 5,
|                                                        |  [Profit Margin (Weighted)],
|                                                        |   IF ( _rank_bottom <= 5, [Profit Margin (Weighted)], BLANK () ) )
|                                                        |  RETURN
|                                                        |  _result                                                             
| TopN & BottomN Segment By Profit Margin                | =                                                                                                                                                           |
|                                                        |  VAR _rank_top =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Segment] ) ), [Profit Margin (Weighted)],, DESC, DENSE )
|                                                        |  VAR _rank_bottom =
|                                                        |  RANKX ( ( ALLSELECTED ( Ace_Superstore_retail_dataset[Segment] ) ), [Profit Margin (Weighted)],, ASC, DENSE )
|                                                        |  VAR _result =
|                                                        |  IF (
|                                                        |  _rank_top <= 5,
|                                                        |  [Profit Margin (Weighted)],
|                                                        |  IF ( _rank_bottom <= 5, [Profit Margin (Weighted)], BLANK () ) )
|                                                        |  RETURN
|                                                        |  _result          

<h2>POWER BI DASHBOARD IMAGES</h2>

<h3>TOP-LEVEL-SUMMARY</h3>

![image](https://github.com/user-attachments/assets/e4dc3154-7152-4c64-8f86-1b048bbf37bd)

<h3>REGIONAL_ANALYSIS</h3>

![image](https://github.com/user-attachments/assets/19cc9a81-09a7-48c8-97cf-551280e7073a)

<h3>PRODUCT_ANALYSIS</h3>

![image](https://github.com/user-attachments/assets/42d58207-4671-4354-bd4d-3e93ede8a133)

<h3>FILTER PAGE </h3>

![image](https://github.com/user-attachments/assets/55f57458-cbd5-4a1b-b3c8-dabb530e27f9)


<h2>Screenshots</h2>

<h3>Highlight Top & Bottom using Rules</h3>

![image](https://github.com/user-attachments/assets/b8ae6ba7-d3af-42c0-ae9c-59475b2e72d3)

<h3>KPI Card Conditional Formatting </h3>

![image](https://github.com/user-attachments/assets/77ea7716-5828-4235-ac38-48b866c81120)

<h3>Organize MeasuredGroup</h3>

![image](https://github.com/user-attachments/assets/c63ca657-123d-41dd-9570-c3bc92244e82)

<h3>Data Profiling </h3>

![image](https://github.com/user-attachments/assets/3188d614-8c5b-451f-821a-995821f359ce)

![image](https://github.com/user-attachments/assets/c35b0864-567a-4f4e-bdb4-88f7b033bacb)

