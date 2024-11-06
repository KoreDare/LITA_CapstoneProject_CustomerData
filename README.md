# LITA_CapstoneProject_CustomerData

### Project Objective
This project aims to analyze the customer data for a subscription service in order to understand customer behaviour, track subscription types, and identify key trends in cancellations and renewals. 

### Data Sources
The primary data source used here is CustomerData from the LITA Capstone Project. [Customer Data.xlsx](https://github.com/user-attachments/files/17645907/Customer.Data.xlsx)
The dataset contains information about customers' subscription patterns, types, revenue generated across regions, and their active status.

### Data Tools
- Microsoft Excel for Data Cleaning, Analysis, and Visualization
- Structured Query Language (SQL) for Querying of Data
- GitHub for Portfolio Building
- Microsoft Power BI for Data Summarization and Visualization

### Data Analysis using Excel PivotTables and Dashboard
Using the PivotTables in Excel, I retrieved the parameters itemized below:
- Total Revenue by Region
- Total Revenue by Subscription Type
- Number of Customers by Region
- Number of Customers by Subscription Type
- Percentage Revenue by Region
- Percentage Revenue by Subscription Type

I gathered that the region with the highest number of subscribers is the Eastern Region although the difference in subscriber count between the regions is negligible.

The subscribers favoured the Basic bouquet more than the other subscription types. This may imply that most of the subscribers are satisfied with the features offered in the Basic bouquet and cannot be bothered to upgrade their subscription.

Another thing worthy of note is that the Eastern region had 100% retention of subscribers. No one canceled their subscription, unlike the other regions which had 60% more cancellations than active subscribers.

<img width="485" alt="Customer Data PivotTables" src="https://github.com/user-attachments/assets/2234c3ad-c48b-4a19-9df7-536af1652938">

<img width="511" alt="Customer Data Dashboard" src="https://github.com/user-attachments/assets/019de670-d84e-4dd9-a2d8-b565a9ee5657">


### Data Analysis using SQL
I imported the dataset which I had saved as a .csv file from Excel after creating the database in the SQL interface. After cleaning the data, I used the following queries to extract the various information as detailed below:

- Total Number of Customers from each Region

> ```SQL
> select Region, count(CustomerID) as [Total Customer]
> from [dbo].[CustomerData_Capstone_Project]
> group by Region
> order by 2 desc
> ```

- Most Popular Subscription Type by Number of Customers

> ```SQL
> select Top 1 SubscriptionType, count(CustomerID) as [Total Customer]
> from [dbo].[CustomerData_Capstone_Project]
> group by SubscriptionType
> ```

- Customers who canceled their subscription within 6 months

> ```SQL
> select CustomerName from [dbo].[CustomerData_Capstone_Project]
> where canceled = 'true' and datediff(month,SubscriptionStart,SubscriptionEnd)<=6
> ```

- Average Subscription Duration for all Customers

> ```SQL
> select AVG(Duration) as Average_Subscription_Duration
> from [dbo].[CustomerData_Capstone_Project]
> ```

- Customers with Subscription Longer than 12 months

> ```SQL
> select * from [dbo].[CustomerData_Capstone_Project]
> where datediff(month, SubscriptionStart, SubscriptionEnd) > 12
> ```

- Total Revenue by Subscription Type

> ```SQL
> select SubscriptionType, sum(Revenue) as [Total Revenue]
> from [dbo].[CustomerData_Capstone_Project]
> group by SubscriptionType
> order by 2 desc
> ```

- Top 3 Regions by Subscription Cancellation

> ```SQL
> select Top 3 Region, count(CustomerID) as [Canceled Subscription]
> from [dbo].[CustomerData_Capstone_Project]
> where canceled = 'true'
> group by Region
> order by 2 desc
> ```

- Total Number of Active and Canceled Subscriptions

> ```SQL
> select count(case when Canceled = 'False' then 1 end) as Active_subscription,
>        count(case when Canceled = 'True' then 1 end) as Canceled_subscription
> 	   from [dbo].[CustomerData_Capstone_Project]
> ```
