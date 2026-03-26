# SQL--Phone-Sales-Dataset
# I. Introduction

This project focuses on analyzing sales data from an electronics retail business, specifically centered around phone and accessory transactions. The primary goal is to extract meaningful insights from the data that can help improve sales strategies, understand customer preferences, and enhance product offerings.


## II. The Goal of Creating This Project

- Analyze phone sales performance using SQL  
- Identify top products, customers, and trends  
- Extract business insights by brand, age group, and purchase behavior


## III. Dataset description table 


### accessories_sale

| Column Name         | Data Type | Description |
|---------------------|----------|-------------|
| TransactionID       | STRING   | Unique transaction identifier |
| CustomerCode        | STRING   | Unique customer code |
| Accessories_name    | STRING   | Accessories category name |
| Accessories_subname | STRING   | Accessories sub-category name |
| Unitprice           | INTEGER  | Price per unit of accessory |
| Unit                | INTEGER  | Quantity purchased |
| SalesValue          | INTEGER  | Total sales value (Unit × Unitprice) |


### hackathon_phonesales

| Column Name      | Data Type | Description |
|------------------|----------|-------------|
| TransactionID    | STRING   | Unique transaction identifier |
| CustomerCode     | STRING   | Unique customer code |
| ProductName      | STRING   | Phone model name |
| ProductBrand     | STRING   | Phone brand |
| DatePurchase     | STRING   | Purchase date |
| GeographicalArea | STRING   | Customer geographical area |
| Payment_method   | STRING   | Payment method (Cash / Installment) |
| Bank             | STRING   | Bank used for installment payment |
| Color            | STRING   | Phone color |
| Carrier          | STRING   | Mobile network carrier |
| SexType          | STRING   | Customer gender |
| YearOldRange     | STRING   | Customer age range |
| Unitprice        | INTEGER  | Price per unit |
| SalesValue       | INTEGER  | Total sales value |
| Unit             | INTEGER  | Quantity purchased |
## IV. Explore the Dataset
#### Query 1️⃣:
```
select
  format_date('%Y %m',parse_date('%Y %m %d',DatePurchase)) month
  ,count(distinct TransactionID) so_don_hang
from `polar-winter-343402.hometest.hackathon_phone_sales`
group by 1
order by 1;
```

 | month  | so_don_hang |
|--------|-------------|
| 201501 | 16963 |
| 201502 | 19999 |
| 201503 | 17944 |
| 201504 | 19570 |
| 201505 | 20830 |


#### Query 2: Number of Customers by Month

SELECT
  FORMAT_DATE('%Y%m', PARSE_DATE('%Y %m %d', DatePurchase)) AS month,
  COUNT(DISTINCT CustomerCode) AS so_khach_hang
FROM `polar-winter-343402.hometest.hackathon_phone_sales`
GROUP BY 1
ORDER BY 1;
``

| Row | month  | so_khach_hang |
|-----|--------|---------------|
| 1   | 201501 | 16130 |
| 2   | 201502 | 19217 |
| 3   | 201503 | 17132 |
| 4   | 201504 | 18828 |
| 5   | 201505 | 19934 |
``



