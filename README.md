# MY-LITA-PROJECT-2-CUSTOMERSDATA

### Data Description

The dataset includes the following fields;

- Customer ID: Unique customer identifier
- Subscription Type: Basic, Premium and Standard
- Subscription Start/End Dates
- Cancellation Date
- Demographics: Region
- Subscription Duration
- Revenue

  ![CustomerData Table](https://github.com/user-attachments/assets/a485c480-fa55-4eea-8f78-3c5e548dc3f5)

  
Instructions:
1. Excel:
o Analyze customer data using pivot tables to find subscription patterns.

Using PivotTables to analyze customer data for subscription pattern is an effective way to uncover trends and insights.

a. Analyze Subscription Patterns: This analysis helps to understand how many customers are subscribed to each subscription type or plan
Pivort Charts for Visualization
To make analysis more visualluy appealing and easier to understand, I create a Pivot Charts from the PivotTable data

![CD Pivot Table](https://github.com/user-attachments/assets/f2f656ef-b74e-4302-88a4-b10deacd21f0)

### 2. SQL
Load the dataset into SQL Server environment to writ and validate the wueries
```
  CREATE database LITA_Capstone_Project_2
  select *from [dbo].[LITA Capstone CustomerData]
```

- retrieve the total number of customers from each region
  
``` 
  SELECT Region,
  COUNT(distinct CustomerID) AS Totalcustomers
  FROM [dbo].[LITA Capstone CustomerData]
  GROUP BY Region
  ORDER BY TotalCustomers;
```

- find the most popular subscription type by the number of customers

```
  SELECT TOP 1 SubscriptionType,
  COUNT (CustomerID) AS NumberOfCustomers
  FROM [dbo].[LITA Capstone CustomerData]
  GROUP BY SubscriptionType
  ORDER BY NumberOfCustomers DESC;
```

- find customers who canceled their subscription within 6 months

```
  SELECT CustomerID, SubscriptionStart, SubscriptionEnd, 
  DATEDIFF(month,SubscriptionStart, SubscriptionEnd)
  AS SubscriptionDuration
  FROM [dbo].[LITA Capstone CustomerData]
  WHERE DATEDIFF(month,SubscriptionStart, SubscriptionEnd) <= 6
  ORDER BY SubscriptionDuration ASC;
```

- calculate the average subscription duration for all customers

```
  SELECT SubscriptionType,
  AVG(DATEDIFF(month, SubscriptionStart, SubscriptionEnd))
  AS AverageSubscriptionDuration
  FROM [dbo].[LITA Capstone CustomerData]
  GROUP BY SubscriptionType;
```
		
- find customers with subscriptions longer than 12 months

```
  SELECT CustomerID, SubscriptionType, SubscriptionStart, SubscriptionEnd, 
  DATEDIFF (month, SubscriptionStart, SubscriptionEnd) 
  AS SubscriptionDuration
  FROM [dbo].[LITA Capstone CustomerData]
  WHERE DATEDIFF(month,SubscriptionStart, SubscriptionEnd) > 12
  ORDER BY SubscriptionDuration DESC;
```
		
- calculate total revenue by subscription type
```
  SELECT SubscriptionType, SUM(Revenue) AS TotalRevenue
  FROM [dbo].[LITA Capstone CustomerData]
  GROUP BY SubscriptionType 
  ORDER BY TotalRevenue DESC;
```
		
		
- find the top 3 regions by subscription cancellations

```
  SELECT TOP 3 Region, 
  COUNT(CustomerID) AS CancellationCount
  FROM [dbo].[LITA Capstone CustomerData]
  WHERE SubscriptionEnd IS NOT NULL
  GROUP BY Region	
  ORDER BY CancellationCount DESC;
```
		
- find the total number of active and canceled subscriptions
  ```
  SELECT Canceled, 	
  COUNT(CustomerID) AS SubscriptionCount
  FROM [dbo].[LITA Capstone CustomerData]
  GROUP BY Canceled;
  ```
