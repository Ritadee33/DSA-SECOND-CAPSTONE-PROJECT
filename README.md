# DSA-SECOND-CAPSTONE-PROJECT
Second project i worked on given by DSA-INCUBATOR HUB

## PROJECT TOPIC: Kultra Mega STORES INVENTORY ANALYSIS
### PROJECT OVERVIEW
This query and analysis project aims to write queries that can support Abuja division of Kultra Mega Stores and provide valueable insights that can be used to make decisions

#### Data Source 
The primary source of this data is unknown but the secondary source of the data is DSA CAPSTONE PROJECT hence it cannot be downloaded online 
#### Tool used
Microsoft sql server [Download Here]
* For quering and analysis

#### Analysis

  ```
  sql
create database KMS

select * from kms_inventory

select * from Order_Status


alter table kms_inventory
alter column profit decimal (10,3)

alter table kms_inventory
alter column Unit_price decimal (10,3)

alter table kms_inventory
alter column Shipping_cost decimal (10,3)


--------JOIN KMS_INVENTORY TABLE AND ORDER__ID TABLES USING SUBQUERY------

select * from kms_inventory
      select Row_ID, Order_ID, Order_Date, Order_Priority, Order_Quantity, Sales, Discount, Ship_Mode, Profit, Unit_Price, Shipping_Cost, Customer_Name, Province, Region, Customer_Segment
	                from kms_inventory) As kms
join (
     select Order_ID, [Status]
	       from Order_Status) As Ord
on kms.Order_ID = Ord. Order_ID


-----QUESTION 1: WHICH PRODUCT CATEGORY HAD THE HIGHEST SALES-------
---ANS: TECHNOLOGY UNDER PRODUCT CATEGORY HAD THE HIGHEST SALES

select top 1 product_category, sum(sales) as highest_sales 
from kms_inventory
where product_category in ('Office Supplies', 'Technology', 'Furniture')
group by product_category
order by highest_sales desc


-------QUESTION 2: WHAT ARE THE TOP 3 AND BOTTOM 3 REGION IN TERMS OF SALES
 ---ANS: THE TOP 3 REGIONS ARE WEST, ONTARIO, AND PRARIE
 ---ANS: THE BOTTOM 3 REGIONS ARE NUNAVUT, NORTHWEST TERRITORIES, AND YUKON

select top 3 Region, sum(Sales) as total_Sales 
	from kms_inventory
	group by Region
	order by total_Sales desc
	

select top 3 Region, sum(Sales) as Sales 
	from kms_inventory
	group by Region
	order by Sales asc


---------QUESTION 3:WHAT WERE THE TOTAL SALES OF APPLIANCES IN ONTARIO
---ANS: THE TOTAL SALES OF ONTARIO IS 202346.839630127

select Region, Product_Sub_Category, sum(Sales) as Total_Sales
	from kms_inventory
	where Product_Sub_Category = 'Appliances' and Region = 'Ontario'
	group by Region, Product_Sub_Category


-------QUESTION 4: ADVICE THE MANAGEMENT OF KMS ON WHAT TO DO TO INCREASE REVENUE FROM THE BOTTOM 10 CUSTOMERS
---ANS: MANAGEMENT OF KMS SHOULD INVEST MORE IN CUSTOMERS WHOSE REVENUE STILL SUMS UP TO A 100 AND ABOVE 

select top 10 Customer_Name, Customer_segment, sum(Sales) as Revenue 
	from kms_inventory
	group by Customer_Name, Customer_Segment
	order by Revenue desc

------QUESTION 5: KMS INCURRED THE MOST SHIPPING COST USING WHICH SHIPPING METHOD
---ANS: KMS INCURRED THE MOST SHIPPING COST USING THE DELIVERY TRUCK SHIPPING METHOD

----This Analysis reveals the need for KMS to detemine whether this shipping mode is being used efficiently
---If the cost of this shipping mode equals the order priority
---Check whether there are chances of optimizing logistics and reducing cost

select top 1 Ship_Mode, sum(Shipping_Cost) as Shipping_Cost
	  from kms_inventory
	  group by Ship_Mode
	  order by Shipping_Cost desc

-------QUESTION 6:WHO ARE THE MOST VALUABLE CUSTOMERS AND WHAT PRODUCT OR SERVICES DO THEY TYPICALLY PURCHASE


select top 10 Customer_Name, Customer_Segment, Product_Category, Product_Sub_Category, Product_Name,
    sum(Sales) as Total_Spent
	from kms_inventory
	group by Customer_Name, Customer_Segment, Product_Category, Product_Sub_Category, Product_Name
	order by Total_Spent desc


-------QUESTION 7: WHICH SMALL BUSINESS CUSTOMER HAD THE HIGHEST SALES

select top 1 Customer_Name, Customer_Segment, sum(sales) as Total_sales 
from kms_inventory
where Customer_Segment = 'Small Business'
group by Customer_Segment, Customer_Name
order by Total_sales desc


-------QUESTION 8: WHICH CORPORATE CUSTOMER PLACED THE MOST NUMBER OF ORDERS IN 2009-2012

select top 5 Customer_Segment as Customer_Segment, Customer_Name, count(Order_Quantity) as Total_Orders
from kms_inventory
where Customer_Segment = 'Corporate' and year(Order_Date), between '2009' and '2012'
group by Customer_Segment
order by Total_Orders desc


-------QUESTION 9: WHICH CONSUMER CUSTOMER WAS THE MOST PROFITABLE ONE
---ANS: THE CONSUMER CUSTOMER WITH THE MOST HIGHEST PROFIT IS EMILY PHAN 

select top 1* from (
     select Customer_Name, Customer_Segment, Profit
	    from kms_inventory) as Profit
		where Customer_Segment = ('Consumer')
		order by Profit desc



    
