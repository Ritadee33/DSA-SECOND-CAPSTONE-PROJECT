# DSA-SECOND-CAPSTONE-PROJECT
Second project i worked on given by DSA-INCUBATOR HUB

## PROJECT TOPIC: Kultra Mega STORES INVENTORY ANALYSIS
### PROJECT OVERVIEW
This query and analysis project aims to write queries that can support Abuja division of Kultra Mega Stores and provide valueable insights that can be used to make decisions

#### Data Source 
The primary source of this data is unknown but the secondary source of the data is DSA CAPSTONE PROJECT hence it cannot be downloaded online 
#### Tool used
Microsoft sql server
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

select * from (
      select Row_ID, Order_ID, Order_Date, Order_Priority, Order_Quantity, Sales, Discount, Ship_Mode, Profit, Unit_Price, Shipping_Cost, Customer_Name, Province, Region, Customer_Segment
	                from kms_inventory) As kms
join (
     select Order_ID, [Status]
	       from Order_Status) As Ord
on kms.Order_ID = Ord. Order_ID


-----QUESTION 1: WHICH PRODUCT CATEGORY HAD THE HIGHEST SALES-------
---ANS: TECHNOLOGY UNDER PRODUCT CATEGORY HAD THE HIGHEST SALES

select product_category,max(sales) as highest_sales from kms_inventory
where product_category in('Office Supplies','Technology','Furniture')
group by product_category;


-------QUESTION 2: WHAT ARE THE TOP 3 AND BOTTOM 3 REGION IN TERMS OF SALES
 ---ANS: THE TOP 3 REGIONS ARE ATLANTIC, QUEBEC, AND PRARIE
 ---ANS: THE BOTTOM 3 REGIONS ARE WEST, WEST, AND YUKON

select top 3 Region,
    sum(Sales) as Sales 
	from kms_inventory
	group by Region, Sales
	order by Sales desc

select top 3 Region,
    sum(Sales) as Sales 
	from kms_inventory
	group by Region, Sales
	order by Sales asc


---------QUESTION 3:WHAT WERE THE TOTAL SALES OF APPLIANCES IN ONTARIO
---ANS: THE TOTAL SALES OF ONTARIO IS 202346.839630127

select Product_Sub_Category,Region,
    sum(Sales) as Total_Sales
	from kms_inventory
	where Product_Sub_Category = 'Appliances' and Region = 'Ontario'
	group by Product_Sub_Category,Region


-------QUESTION 4: ADVICE THE MANAGEMENT OF KMS ON WHAT TO DO TO INCREASE REVENUE FROM THE BOTTOM 10 CUSTOMERS
---ANS: MANAGEMENT OF KMS SHOULD INVEST MORE IN CUSTOMERS WHOSE REVENUE STILL SUMS UP TO A 100 AND ABOVE 

select top 10 Customer_Name, Customer_Segment,
    sum(Sales) as Revenue 
	from kms_inventory
	group by Customer_Name, Customer_Segment
	order by Revenue

------QUESTION 5: KMS INCURRED THE MOST SHIPPING COST USING WHICH SHIPPING METHOD
---ANS: KMS INCURRED THE MOST SHIPPING COST USING THE DELIVERY TRUCK SHIPPING METHOD

select top 1 Ship_Mode,
      sum(Shipping_Cost) as Shipping_Cost
	  from kms_inventory
	  group by Ship_Mode
	  order by Shipping_Cost desc

-------QUESTION 6:



-------QUESTION 7: WHICH SMALL BUSINESS CUSTOMER HAD THE HIGHEST SALES
---ANS: THE SMALL BUSINESS CUSTOMER WITH THE HIGHEST SALES IS DENNIS KANE

select top 1* from (
     select Customer_Name, Customer_Segment, Sales
	    from kms_inventory) as Sales
		where Customer_Segment = ('Small Business')
		order by Sales desc

-------QUESTION 8:


-------QUESTION 9: WHICH CONSUMER CUSTOMER WAS THE MOST PROFITABLE ONE
---ANS: THE CONSUMER CUSTOMER WITH THE MOST HIGHEST PROFIT IS EMILY PHAN 

select top 1* from (
     select Customer_Name, Customer_Segment, Profit
	    from kms_inventory) as Profit
		where Customer_Segment = ('Consumer')
		order by Profit desc

-----QUESTION 10: WHICH CUSTOMER RETURNED ITEMS AND WHAT SEGMENT DO THEY BELONG TO
---ANS:

select * from (
     select Customer_Name, Customer_Segment, "Status"
	    from kms_inventory) as "Status"
		order by "Status" desc


    
