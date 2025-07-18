# DSA-SECOND-CAPSTONE-PROJECT

## PROJECT TOPIC: Kultra Mega STORES INVENTORY ANALYSIS
### PROJECT OVERVIEW
This query and analysis project aims to develop SQL-based analytics that can support Abuja division of Kultra Mega Stores and provide valueable insights and findings which can be used to make decisions

#### Data Source 
The primary source of this data is unknown but the secondary source of the data is DSA CAPSTONE PROJECT hence it cannot be downloaded online 

#### Tool used
Microsoft sql server [Download Here]

#### Data Cleaning and preparation
The following action was performed
* create database
* import  two data csv files and preparation
* cleaning and formatting
* altered the datatype of some columns
* Joined the the two data csv files

#### Exploratory Data Analysis
This process involves the exploring of data to answer some questions such as:

* Which product category had the highest sales?
* What are the Top 3 and Bottom 3 regions in terms of sales?
* What were the total sales of appliances in Ontario?
* Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
* KMS incurred the most shipping cost using which shipping method?Case Scenario II
* Who are the most valuable customers, and what products or services do they typicallypurchase?
* Which small business customer had the highest sales?
* Which Corporate Customer placed the most number of orders in 2009 – 2012?
* Which consumer customer was the most profitable one?
* Which customer returned items, and what segment do they belong to?
* If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer

#### Result Findings
* Technology is the Best Selling Category
* West, Ontario and prarie are the top regions in sales
* Nunavut, Northwest, and Yukan are the regions with the least sales respectively
* Emily Phan is the consumer customer with the most profit
* Dennis Kane is the higest small business owner
* Delivery Truck is the shipping mode witrh the most shipping cost

#### Recommendation
* KMS should improve services in the top 3 regions
* Marketing strategy should be applied more in regions with the least sales
* The shipping mode where more cost was incurred should be evaluated in line with he order priority
* More production and sales for the best selling product category


#### Query and Analysis

  ``` SQL
create database KMS
```
``` SQL				
select * from kms_inventory
```
``` SQL
select * from Order_Status
```
``` SQL
alter table kms_inventory
alter column profit decimal (10,3)
```
``` SQL
alter table kms_inventory
alter column Unit_price decimal (10,3)
```
``` SQL
alter table kms_inventory
alter column Shipping_cost decimal (10,3)
```


--------JOIN KMS_INVENTORY TABLE AND ORDER__ID TABLES USING SUBQUERY------
``` SQL
select * from kms_inventory
      select Row_ID, Order_ID, Order_Date, Order_Priority, Order_Quantity, Sales, Discount, Ship_Mode, Profit, Unit_Price, Shipping_Cost, Customer_Name, Province, Region, Customer_Segment
	                from kms_inventory) As kms
join (
     select Order_ID, [Status]
	       from Order_Status) As Ord
on kms.Order_ID = Ord. Order_ID
```


-----QUESTION 1: WHICH PRODUCT CATEGORY HAD THE HIGHEST SALES-------
* Under the product category Technology had the highest sales
``` SQL
select top 1 product_category, sum(sales) as highest_sales 
from kms_inventory
where product_category in ('Office Supplies', 'Technology', 'Furniture')
group by product_category
order by highest_sales desc
```

-------QUESTION 2: WHAT ARE THE TOP 3 AND BOTTOM 3 REGION IN TERMS OF SALES
* West, Ontario, and Prarie are the 3 top regions performing well in sales
* Nunavut, Northwest territories, and Yukon are the 3 least performing regiond in sales
``` SQL
select top 3 Region, sum(Sales) as total_Sales 
	from kms_inventory
	group by Region
	order by total_Sales desc
```
	
````SQL
select top 3 Region, sum(Sales) as Sales 
	from kms_inventory
	group by Region
	order by Sales asc
````


---------QUESTION 3:WHAT WERE THE TOTAL SALES OF APPLIANCES IN ONTARIO
* The total sales of appliances in ontario is 202346.839630127

````SQL
select Region, Product_Sub_Category, sum(Sales) as Total_Sales
	from kms_inventory
	where Product_Sub_Category = 'Appliances' and Region = 'Ontario'
	group by Region, Product_Sub_Category
````


-------QUESTION 4: ADVICE THE MANAGEMENT OF KMS ON WHAT TO DO TO INCREASE REVENUE FROM THE BOTTOM 10 CUSTOMERS
* The Management of KMS  

````SQL
select top 10 Customer_Name, Customer_segment, sum(Sales) as Revenue 
	from kms_inventory
	group by Customer_Name, Customer_Segment
	order by Revenue asc
````

------QUESTION 5: KMS INCURRED THE MOST SHIPPING COST USING WHICH SHIPPING METHOD
* KMS incurred the most shipping mode using Delivery truck method 
* This Analysis reveals the need for KMS to detemine whether this shipping mode is being used efficiently
* If the cost of this shipping mode equals the order priority
* Check whether there are chances of optimizing logistics and reducing cost

````SQL
select top 1 Ship_Mode, sum(Shipping_Cost) as Shipping_Cost
	  from kms_inventory
	  group by Ship_Mode
	  order by Shipping_Cost desc
````

-------QUESTION 6:WHO ARE THE MOST VALUABLE CUSTOMERS AND WHAT PRODUCT OR SERVICES DO THEY TYPICALLY PURCHASE

````SQL
select top 10 Customer_Name, Customer_Segment, Product_Category, Product_Sub_Category, Product_Name,
    sum(Sales) as Total_Spent
	from kms_inventory
	group by Customer_Name, Customer_Segment, Product_Category, Product_Sub_Category, Product_Name
	order by Total_Spent desc
`````


-------QUESTION 7: WHICH SMALL BUSINESS CUSTOMER HAD THE HIGHEST SALES
* The small business owner with the highest sales is Dennis Kane

````SQL
select top 1 Customer_Name, Customer_Segment, sum(sales) as Total_sales 
from kms_inventory
where Customer_Segment = 'Small Business'
group by Customer_Segment, Customer_Name
order by Total_sales desc
````


-------QUESTION 8: WHICH CORPORATE CUSTOMER PLACED THE MOST NUMBER OF ORDERS IN 2009-2012

````SQL
select top 5 Customer_Segment as Customer_Segment, Customer_Name, count(Order_Quantity) as Total_Orders
from kms_inventory
where Customer_Segment = 'Corporate' and year(Order_Date), between '2009' and '2012'
group by Customer_Segment
order by Total_Orders desc
````


-------QUESTION 9: WHICH CONSUMER CUSTOMER WAS THE MOST PROFITABLE ONE
* Consumer customer with the most profit is Emily Phan

````SQL
select top 1* from (
     select Customer_Name, Customer_Segment, Profit
	    from kms_inventory) as Profit
		where Customer_Segment = ('Consumer')
		order by Profit desc
````

#### Result Findings
* Technology is the Best Selling Category
* West, Ontario and prarie are the top regions in sales
* Nunavut, Northwest, and Yukan are the regions with the least sales respectively
* Emily Phan is the consumer customer with the most profit
* Dennis Kane is the higest small business owner
* Delivery Truck is the shipping mode witrh the most shipping cost

#### Recommendation
* KMS should improve services in the top 3 regions
* Marketing strategy should be applied more in regions with the least sales
* The shipping mode where more cost was incurred should be evaluated in line with he order priority
* More production and sales for the best selling product category



