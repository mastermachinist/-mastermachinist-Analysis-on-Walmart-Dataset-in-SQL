# Analysis-on-Walmart-Dataset-in-SQL

By Atif Salam


Part I : Objectives
Food is part and parcel of life and people look for meals, food products, food businesses and
restaurants over internet all the time. Competitors also seek information about each other in
the food industry. This leads to investments in food technology as well. From the given dataset
that we will work on emphasis on the Food sales of a particular company. This food database
facilitates users in accessing information and an additional advantage of these databases is that
the users can manage their health and make healthy eating decisions.
Fields include:
● Item_Identifier - Unique identifier for each product.
● Item_Weight – Product weight.
● Item_Fat_Content – Fat content of the product.
● Item_Type – Product category.
● Item_MRP – List price of the product.
● Outlet_Identifier - Unique identifier for each store.
● Yr_since_Inception - the beginning of an official activity
● Outlet_Size - The size of the store.
● Outlet_Location_Type - The type of city in which the store is located.
● Outlet_Type - Whether the store is a grocery store or a supermarket.
● Item_Outlet_Sales - Sales of the product in each store.
Products are spread across many Outlets which are located in different areas. One factor
affecting a product sales in one area does not affect the product in another area. Customers also
have different qualities that affect their purchasing activities.
I will divide the levels into different categories.
Store Level hypotheses
1. City type: Stores located in large cities are likely to have high sales levels because of the
populations densities there as compared to stores in smaller cities.
2. Location: Stores located in popular market are areas sre likely to have high sales.
3. Economic Growth: Stores located in areas with higher economic growth are expected
to realize higher sales.
4. Store Size: Size of the Outlet will also determine its sales record.
Product level Hypotheses
1. Brand: Branded products are likely to have higher sales volumes as compared to
unbranded products.
2. Utility: Products used daily are highly likely to be purchased.
3. Health Content: Depends on the user’s preference they like.
Other Misc. Objectives:
1. Find out the sales of each product at a particular location.
2. Understand the properties of products and stores which play a key role in increasing
sales.
3. Find out the properties of any store.
Part II: Queries & Insights
● Duplicates:
Code : SELECT First(Food_Manufacturing_Company.[Item_Type]) AS [Item_Type Field],
First(Food_Manufacturing_Company.[Outlet_Size]) AS [Outlet_Size Field],
First(Food_Manufacturing_Company.[Outlet_Location_Type]) AS [Outlet_Location_Type Field],
First(Food_Manufacturing_Company.[Outlet_Type]) AS [Outlet_Type Field],
Count(Food_Manufacturing_Company.[Item_Type]) AS NumberOfDups
FROM Food_Manufacturing_Company
GROUP BY Food_Manufacturing_Company.[Item_Type],
Food_Manufacturing_Company.[Outlet_Size],
Food_Manufacturing_Company.[Outlet_Location_Type],
Food_Manufacturing_Company.[Outlet_Type]
HAVING (((Count(Food_Manufacturing_Company.[Item_Type]))>1) AND
((Count(Food_Manufacturing_Company.[Outlet_Type]))>1));
There are 115 records of duplicate ID’s from 7071 entries
Output: No of duplicates 115 records.
Possible Reason: Same Item_Type can exist in multiple stores.
● Location Wise Sales:
Code : SELECT Outlet_Location_Type,Round(SUM(sales))
FROM Food_Manufacturing_Company
group by Outlet_Location_Type Order By 2 desc;
Insight: Since, Tier 2 contains mostly Supermarket stores hence the sales is highest in it
while grocery stores are mostly found in Tier 3.
● Outlet wise sales :
Code : SELECT Outlet_Type,Round(SUM(sales))
FROM Food_Manufacturing_Company
group by Outlet_type;
Insight : As per the given table, these are the total sales of each super market.
● Outlet Size wise sales :
Code : SELECT Outlet_Size,Round(SUM(sales))
FROM Food_Manufacturing_Company
group by Outlet_Size Order By 2 desc;
Insight : As per the table we can see the the supermarkets and low market types are spread
vastly in medium wise location. Less no. of high outlet type is present
● Item Type Sales :
Code : SELECT Item_Type,Round(SUM(sales))
FROM Food_Manufacturing_Company
group by Item_Type;
Insight : From the given table, it seems that the item type does not have much affect on the location
& outlet type.
Insights Summary:
● Sales of Tier 2> Sales of Tier 1 > Sales of Tier 3
● Item Type does not influence the item sales much.
● Tier 2 & Tier 3 cities have better sales than Tier 1 cities.
● Key factors: Outlet type and Item MRP are the key factors affecting the outlet sales.
