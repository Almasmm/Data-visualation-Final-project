# Final project of making Data Visualation with many tools
PowerBI sales analytics for Final project of the course "Data visualization"

## Project Overview



This Power BI report provides a comprehensive analysis of sales data using four datasets:
- **order_lines.txt**: Contains details about order items (order ID, product ID, price, and quantity).
- **orders.csv**: Contains information about orders (order date, warehouse ID, user ID).
- **products.csv**: Contains product details (product ID, product name, and category).
- **warehouses.csv**: Contains warehouse details (city, warehouse ID, address).

The goal of this project was to gain actionable insights from sales data and create an interactive, user-friendly report for business stakeholders.

## Key Features of the Report

### Page 1: Overview Dashboard
An executive summary providing a high-level view of key performance indicators:

- **KPI Cards**:
  - **Total Sales**: Sum of all sales across all orders.
  - **Total Orders**: Count of unique orders.
  - **Total Quantity Sold**: Total number of products sold.
  - **Average Order Value**: Total sales divided by the number of orders.
- **Line Chart (Total Sales by Day in August)**:
  - Displays the trend of total sales throughout the month of August, helping to identify peak sales days.
- **Bar Chart (Top 10 Products by Total Sales)**:
  - Identifies the top 10 best-selling products based on total sales.
- **Map Visualization (Total Sales by City)**:
  - Visual representation of sales performance across different cities (Moscow and St. Petersburg).

### Page 2: Product Analysis
In-depth analysis focusing on product performance:

- **Donut Chart (Sales Share by Product Category)**:
  - Displays the percentage contribution of each product category to total sales.
- **Clustered Bar Chart (Top Categories Based on Sales)**:
  - Highlights the top-performing product categories based on sales.
- **Table Visualization**:
  - Detailed view of each product, including product name, category, total sales, and quantity sold.

### Page 3: Warehouse Performance
Analysis of sales performance across warehouses:

- **Stacked Bar Chart (Sales by Warehouse with City Comparison)**:
  - Shows total sales by warehouse, differentiated by city for comparison.
- **Matrix Table (Sales Breakdown by Warehouse and City)**:
  - Provides a breakdown of total sales by warehouse ID and city, offering insights into warehouse performance.
- **Heatmap (Quantity Sold by Warehouse)**:
  - Visual heatmap highlighting differences in quantities sold across different warehouses.

### Page 4: Insights & Observations
This page highlights key findings and insights from the analysis, formatted as text boxes with visual support.

#### Example Insights:
- **Seasonal Trend**:
  - "Sales show peaks on weekends, likely due to increased consumer activity during leisure days."
- **Outlier Product**:
  - "Product XYZ showed a sudden spike in sales, indicating a possible successful marketing campaign."
- **Warehouse Efficiency**:
  - "Sales in St. Petersburg are significantly lower compared to Moscow, suggesting potential for market expansion or improved marketing strategies."

## Data Preparation & Transformation
All data preparation and transformations were done within Power BI using Power Query Editor:

- **Data Types**: Ensured that columns have correct data types (e.g., dates, numbers).
- **Merging Datasets**: 
  - Merged `order_lines.txt` with `orders.csv` using `order_id`.
  - Merged the resulting dataset with `products.csv` on `product_id`.
  - Merged with `warehouses.csv` on `warehouse_id` for geographical insights.
- **Calculated Columns and Measures**:
  - Created calculated measures like **Total Sales**, **Total Quantity Sold**, and **Average Order Value**.


## 2 - 3:
-- SELECT DISTINCT o.user_id

FROM order_lines ol

JOIN orders o ON ol.order_id = o.order_id

JOIN products p ON ol.product_id = p.product_id

WHERE o.order_date BETWEEN '2017-08-01' AND '2017-08-15'
  
  AND p.category = 'Animal Feed'
  
  AND p.product NOT LIKE 'Kitekat cat food, with rabbit in sauce, 85 g';



-- SELECT p.product, COUNT(ol.order_id) AS order_count

FROM order_lines ol

JOIN orders o ON ol.order_id = o.order_id

JOIN warehouses w ON o.warehouse_id = w.warehouse_id

JOIN products p ON ol.product_id = p.product_id

WHERE w.city = 'Санкт-Петербург'
  
  AND o.order_date BETWEEN '2017-08-15' AND '2017-08-30'

GROUP BY p.product

ORDER BY order_count DESC

LIMIT 5;

