# Shopify_data_science
Shopify data science internship assessment

## Question 1: 

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

A.Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 
  
  ### Ans: 
  Mean of column 'order_amount' is 3145.128000. It can be rounded to two decimal places then the answer is 3145.13. AOV of this dataset is wrongly calculated as $3145.13 as they took      the mean of the column 'order_amount'.Another reason why we should not take mean as the AOV value in this case is because 
  
  Minimum value of an order = $90,
  
  Maximun value of an order = $704000 and 
  
  Standard deviation =41282.539. 
  
  This means that on average, the values of column 'order_amount' vary 41282.539 from the mean value. The high values like 704000 might be the reason for mean of the order_column is high. So there are outliers in the data.
  
B.What metric would you report for this dataset?

  ### Ans: 
  The metric I choose for this report is Mode. Since there are outliers in the data and I would prefer the mode value over the mean because most customers placed that order and bulk order which resulted in the high mean is not accurate representation of the AOV. Another reason I chose Mode is that median value of the order_amount is 284 which is close to the mode value than the mean value of the column.

C.What is its value?

### Ans: 
The mode value of the column 'order_amount' is 153.

## Question 2: 

For this question you’ll need to use SQL. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

A. How many orders were shipped by Speedy Express in total?

  ### Ans: 54
  
  SQL Query:
  
  """SELECT COUNT(Orders.OrderID) FROM Orders
  INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
  WHERE Shippers.ShipperName = "Speedy Express";"""

  
B.What is the last name of the employee with the most orders?

  ### Ans: Peacock, 40 Orders
  
  SQL Query:
  
  """SELECT LastName, MAX(Total_Orders), Total.EmployeeID FROM (SELECT COUNT(OrderID) AS Total_Orders,EmployeeID FROM Orders
  GROUP BY EmployeeID) AS Total
  INNER JOIN Employees ON Total.EmployeeID= Employees.EmployeeID;"""

What product was ordered the most by customers in Germany?
  
  ### Ans: Boston Crab Meat
  
  SQL Query:
  
  """SELECT Products.ProductID, ProductName, MAX(Total), Country 
  FROM (SELECT OrderDetails.OrderID, ProductID, SUM(Quantity) AS Total, Country 
  FROM (SELECT OrderID, Orders.CustomerID, Country 
  FROM Orders
  JOIN Customers ON Orders.CustomerID = Customers.CustomerID
  WHERE Country ='Germany') AS German
  JOIN OrderDetails ON OrderDetails.OrderID = German.OrderID
  GROUP BY ProductID) AS Final
  JOIN Products ON Products.ProductID = Final.ProductID;"""






