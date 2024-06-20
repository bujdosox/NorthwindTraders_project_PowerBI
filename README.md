## Northwind Traders project
### Sales of fictive gourmet food supplier 
The analysis can help the company understand it’s overall performance better. Based on trend by transactions further decisions can be made if necessary. By defining worst selling products there is an opportunity to rethink the product portfolio in order to provide better service to customers (looking for alternative products etc.). Revenue by customer matrix and map visualization can show improvement areas to Sales/Marketing Department (keeping top customers and improving cooperation with lower level partners). Investigation of shipping fees can help to improve the service and can be the base of further negotiation with suppliers.

![Northwind Traders_dashboard](https://github.com/bujdosox/LEGO_project_PowerBI/assets/173184545/c18efdc6-34d2-455e-8ae8-9f4cb88da621)

![Northwind Traders_map](https://github.com/bujdosox/LEGO_project_PowerBI/assets/173184545/c1917464-52e5-403b-8769-fa160239a96c)

### Goal
-   Looking for trends by temporal distribution of transactions
-   Defining best and worst selling products
-   Looking for Top 5 customer based on revenue
-   Comparing price level of shipers according considering shipping locations
### Outcome
-   Orders and revenue show slight increase in the investigation period (04.2013 – 06.2015)
-   2 highest and lowest total ordered value by country

        o   USA: $ 245.585
        o   Germany: $ 230.285
        o   Poland: $ 3.532
        o   Norway: $ 5.735
-   Revenue from top 3 customer is almost double ($ 100.000), than revenue from the 4th company ($ 50.000)
-   United Package and Federal Shipping have almost the same shipping rate (5.29% and 5.35%), but Speedy Express can provide a more favorable conditon (4.64%)
### Methods and steps
-   Load multiple CSV files into Power BI Desktop
-   Check coloumn quality, coloumn distribution and coloumn profile regarding the whole data set in Power Query editor
-   Check data types in Power Query editor
-   Transform data in Power Query editor

        o   Promoted first row as header in each tables
        o   Change data type in each tables from text to whole number, date, currency (changed type with locale) and percentage where necessary
        o   Add new coloumn named „year” to „order” table based on date of order
-   Create data model in Model view

        o   connecting data/fact tables (orders, orderdetail) to each other and to dimension/lookup tables based on common ID’s
        o   organizing dimension tables above fact tables in order to vizualize filter flow from up to down and highliht the snowflake scema
        o   Setting one-to-many cardinality and one-way filters
        o   Hiding all foreign keys from Report view prevent to use them for filtering

![Northwind Traders_model](https://github.com/bujdosox/LEGO_project_PowerBI/assets/173184545/17ad1a9f-4ed1-4d27-b7b6-ffe96f194f88)

-   Create a separate table for measures in Table view + create DAX measures

        o       Total Orders = DISTINCTCOUNT(order_details[orderID])
        o       Total Customers = DISTINCTCOUNT(customers[customerID])
        o       Total Revenue = SUMX(order_details, order_details[quantity] * order_details[unitPrice] * (1 - order_details[discount]))
        o       Total Shipping Cost = SUM(orders[freight]) 
        o       Shipping Rate = [Total Shipping Cost] / [Total Revenue]
        o       Quantity Sold = SUM(order_details[quantity])
        o       Average Shiping Cost = AVERAGE(orders[freight])
-   Visualize data in Report view

        o   New card: highlighting Total Orders, Quantity Sold and Total Revenue
        o   Area chart: Orders Trend by temporal distribution
        o   Matrix: Quantity Sold by Product (highlighting the quantity by data bar color)
        o   Slicer with years
        o   Card: display most ordered product, less ordered product and top1 customer
        o   Matrix: Shipping Rate by Suppliers and locations
        o   Map visualization on separate page: highlighting Total Revenue by bubble size
        o   Checking interactions: turn out filtering of any charts/matrixes to most ordered product, less ordered product and top1 customer
        o   Summarize outcomes on a separate page
        o   Create a fix panel with buttons: change between pages + clear all filters
        o   Add a new page with map visualization to show total revenue by countries + add slicers by countries
