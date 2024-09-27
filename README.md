# Sweet Stats Bakery - Power BI Dashboard

## Project Overview
The **Sweet Stats Bakery** Power BI Dashboard is designed to provide a comprehensive analysis of cookie sales, inventory, customer preferences, and marketing effectiveness. By leveraging data visualization and DAX (Data Analysis Expressions) queries, this dashboard offers deep insights into various aspects of the business, enabling stakeholders to make informed, data-driven decisions.

## Objectives
- **Sales Analysis**: Examine cookie sales trends, customer preferences, and product performance.
- **Inventory Management**: Monitor inventory levels and identify trends in product popularity.
- **Marketing Effectiveness**: Analyze the impact of marketing efforts on sales and customer engagement.

## Key Features
- **Sales Metrics**:
  - Average Order Value: `AVERAGE(Orders[Units Sold])`
  - Count of Orders: `COUNTROWS(Orders)`
  - Total Units Sold: `COUNT(Orders[Units Sold])`
- **Customer Insights**:
  - Distinct Customers: `DISTINCTCOUNT(Orders[Customer ID])` - Measures the number of unique customers.
- **Product Grouping**:
  - Grouping of Products based on Units Sold:
    ```DAX
    grouping_of_products = SWITCH(
                            TRUE(),
                            Orders[Units Sold] <= 100 , "small_quantity" ,
                            Orders[Units Sold] <= 500 , "medium_quantity",
                            Orders[Units Sold] <= 1000 , "large_quantity",
                            "extra large quantity sold"
                        )
    ```
- **Chocolate Analysis**:
  - Identifies if a product contains chocolate:
    ```DAX
    HAS CHOCOLATE = IF(FIND("Chocolate",Orders[Product],1,0) = 1 ,"Has Chocolate","No Chocolate")
    ```
- **Profitability Metrics**:
  - Profit Calculation: `Profit = Orders[Revenue] - Orders[Cost]`
  - Profit Margin Percentage: `Profit Margin % = [Total Profit]/ SUM(Orders[Revenue])`
  - Total Profit Calculation: `Total Profit = SUM(Orders[Revenue]) - SUM(Orders[Cost])`

## Advanced Analysis
- **Total Profit for Specific Products**:
  - Fortune Cookie Profit in the 6th Week:
    ```DAX
    Total_profit_for_6th_week_fortune_cookie = CALCULATE(sum(Orders[Profit]), Orders[DAY OF WEEK] == 6 , Orders[Product] == "Fortune Cookie")
    ```
  - Total Profit for Chocolate Chip and Fortune Cookie:
    ```DAX
    Total_profit_for_Cc_&_FC = CALCULATE(SUM(Orders[Profit]), (Orders[Product] in {"Chocolate Chip" , "Fortune Cookie"}))
    ```
  - Total Profit Calculation Using SUMX:
    ```DAX
    Total_Profit_sumx = SUMX('Cookie Types',  'Cookie Types'[Units Sold] * ('Cookie Types'[Revenue Per Cookie] - 'Cookie Types'[Cost Per Cookie]))
    ```

## Tools Used
- **Business Intelligence Tool**: Microsoft Power BI
- **Data Analysis Expressions**: DAX for advanced calculations and measures

## Dataset Structure
- **Orders Table**: Contains information on cookie sales, including:
  - Product ID
  - Customer ID
  - Units Sold
  - Revenue
  - Cost
  - Date of Order

## Dashboard Screenshots
![Sweet Stats Bakery Dashboard Screenshot]
https://github.com/patilasmit/Sweet-Stats-Bakery---Power-BI-Dashboard/blob/main/Screenshot%20(700).png
https://github.com/patilasmit/Sweet-Stats-Bakery---Power-BI-Dashboard/blob/main/Screenshot%20(701).png

## Conclusion
The **Sweet Stats Bakery Power BI Dashboard** serves as an effective tool for analyzing cookie sales and customer preferences. By leveraging this dashboard, stakeholders can enhance their decision-making processes and drive business growth through data-driven insights.
