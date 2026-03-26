# SQL--Phone-Sales-Dataset
# I. Introduction

This project focuses on analyzing sales data from an electronics retail business, specifically centered around phone and accessory transactions. The primary goal is to extract meaningful insights from the data that can help improve sales strategies, understand customer preferences, and enhance product offerings.


## II. The Goal of Creating This Project

This project aims to improve sales performance by analyzing:
- Phone sales data to identify high‑value customer segments  
- Product and brand strategies to enhance upselling opportunities  
- Installment payment policies through data‑driven insights  

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
#### Query 1️:
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
``
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
#### Query 3: Top 3 Phone Brands Preferred by Male and Female Customers (by Orders)

```sql
WITH raw_data AS (
  SELECT
    SexType,
    ProductBrand,
    COUNT(TransactionID) AS so_luong
  FROM `polar-winter-343402.hometest.hackathon_phone_sales`
  GROUP BY 1, 2
),
ranking_so_luong AS (
  SELECT
    SexType,
    ProductBrand,
    so_luong,
    DENSE_RANK() OVER (PARTITION BY SexType ORDER BY so_luong DESC) AS rk
  FROM raw_data
)
SELECT
  SexType,
  ProductBrand,
  so_luong
FROM ranking_so_luong
WHERE rk <= 3
ORDER BY SexType, so_luong DESC;
```

| SexType | ProductBrand | so_luong |
|--------|--------------|----------|
| NAM | SAMSUNG | 15895 |
| NAM | NOKIA | 9869 |
| NAM | Q-SMART | 8395 |
| NU  | SAMSUNG | 18320 |
| NU  | NOKIA | 7715 |
| NU  | Q-SMART | 7136 |
#### Query 4: Which Age Group Buys the Most and Generates the Highest Revenue?

```sql
WITH DT_DS_tuoi AS (
  SELECT
    YearOldRange,
    SUM(Unit) AS Tong_DS,
    SUM(SalesValue) AS Tong_DT
  FROM `polar-winter-343402.hometest.hackathon_phone_sales`
  GROUP BY 1
),
ranking AS (
  SELECT
    YearOldRange,
    Tong_DS,
    DENSE_RANK() OVER (ORDER BY Tong_DS DESC) AS dk_DS,
    Tong_DT,
    DENSE_RANK() OVER (ORDER BY Tong_DT DESC) AS dk_DT
  FROM DT_DS_tuoi
)
SELECT
  YearOldRange,
  Tong_DS,
  Tong_DT
FROM ranking
WHERE dk_DS = 1 OR dk_DT = 1;
```

| YearOldRange | Tong_DS | dk_DS | Tong_DT | dk_DT |
|--------------|--------:|------:|----------------:|------:|
| 26-30 | 57045 | 1 | 250380794600 | 1 |
#### Query 5: Top 3 Products Generating the Highest Revenue by Month

```sql
WITH raw_data AS (
  SELECT
    FORMAT_DATE('%Y%m', PARSE_DATE('%Y %m %d', DatePurchase)) AS month,
    ProductName,
    SUM(SalesValue) AS doanh_thu
  FROM `polar-winter-343402.hometest.hackathon_phone_sales`
  GROUP BY 1, 2
),
ranking_doanhthu AS (
  SELECT
    month,
    ProductName,
    doanh_thu,
    DENSE_RANK() OVER (PARTITION BY month ORDER BY doanh_thu DESC) AS rk
  FROM raw_data
)
SELECT
  month,
  ProductName,
  doanh_thu
FROM ranking_doanhthu
WHERE rk <= 3
ORDER BY month, rk;
```

| month  | ProductName | doanh_thu |
|--------|-------------|-----------:|
| 201501 | Galaxy Note II N7100 Marble White | 6325813000 |
| 201501 | Galaxy Note II N7100 Titan Gray | 4961552500 |
| 201501 | Lumia 620 Black | 3325739500 |
| 201502 | Galaxy Note II N7100 Marble White | 5035073000 |
| 201502 | Galaxy Note II N7100 Titan Gray | 3909001000 |
| 201502 | Lumia 620 Black | 3892467000 |
| 201503 | Galaxy Note II N7100 Marble White | 3578831000 |
| 201503 | Lumia 520 Black | 3306246000 |
| 201503 | S5360(Toroto) White | 2811021000 |
| 201504 | Lumia 520 Black | 7704350000 |
| 201504 | Galaxy S3 Mini I8190 Marble White | 4254747000 |
| 201504 | Lumia 720 Black | 2949279000 |
| 201505 | Lumia 520 Black | 8159257000 |
| 201505 | Galaxy S4 I9500 White | 5415746500 |
| 201505 | Galaxy S3 Mini I8190 Marble White | 3901046000 |

#### Query 6: Which Phone Brands Are Preferred by Customers Aged 26–30?

```sql
WITH raw_data AS (
  SELECT
    YearOldRange,
    ProductBrand,
    COUNT(TransactionID) AS so_luong
  FROM `polar-winter-343402.hometest.hackathon_phone_sales`
  WHERE YearOldRange = '26-30'
  GROUP BY 1, 2
)
SELECT
  YearOldRange,
  ProductBrand,
  so_luong,
  DENSE_RANK() OVER (ORDER BY so_luong DESC) AS rk
FROM raw_data
ORDER BY rk;
```

| YearOldRange | ProductBrand | so_luong | rk |
|--------------|--------------|---------:|---:|
| 26-30 | SAMSUNG | 20656 | 1 |
| 26-30 | Q-SMART | 9927 | 2 |
| 26-30 | NOKIA | 9092 | 3 |
| 26-30 | Mobistar | 5547 | 4 |
| 26-30 | LENOVO | 3075 | 5 |
| 26-30 | SONY | 2781 | 6 |
| 26-30 | LG | 1830 | 7 |
| 26-30 | HTC | 1744 | 8 |
| 26-30 | Q-MOBILE | 800 | 9 |
| 26-30 | APPLE | 780 | 10 |
| 26-30 | BLACKBERRY | 55 | 11 |
| 26-30 | HUAWEI | 15 | 12 |
| 26-30 | F-MOBILE | 6 | 13 |
| 26-30 | ALCATEL | 1 | 14 |
#### Query 7: Are Customers Aged 26–30 Willing to Buy Accessories?

```sql
WITH raw_data AS (
  SELECT
    a.TransactionID,
    a.YearOldRange,
    b.Accessories_name
  FROM `polar-winter-343402.hometest.hackathon_phone_sales` a
  LEFT JOIN `polar-winter-343402.hometest.hackathon_accessories_sales` b
    USING (TransactionID)
)
SELECT
  YearOldRange,
  COUNT(Accessories_name) AS accessories_sale,
  COUNT(*) AS total,
  COUNT(Accessories_name) / COUNT(*) AS ti_le_mua_phu_kien
FROM raw_data
GROUP BY 1
ORDER BY 1;
```

| YearOldRange | accessories_sale | total | ti_le_mua_phu_kien |
|--------------|-----------------:|------:|-------------------:|
| Duoi 21 | 1159 | 3175 | 0.3650 |
| 21-25 | 725 | 1929 | 0.3758 |
| 26-30 | 21491 | 56309 | 0.3817 |
| 31-35 | 7107 | 19621 | 0.3622 |
| 36-40 | 4428 | 12361 | 0.3582 |
| Tren 40 | 731 | 1911 | 0.3825 |
``
#### Query 8: Do Customers of Each Brand Buy Accessories or Insurance?

```sql
WITH raw_data AS (
  SELECT
    a.TransactionID,
    a.ProductBrand,
    b.Accessories_name
  FROM `polar-winter-343402.hometest.hackathon_phone_sales` a
  LEFT JOIN `polar-winter-343402.hometest.hackathon_accessories_sales` b
    USING (TransactionID)
)
SELECT
  ProductBrand,
  COUNT(Accessories_name) AS accessories_sale,
  COUNT(*) AS total,
  COUNT(Accessories_name) / COUNT(*) AS ti_le_mua_phu_kien
FROM raw_data
GROUP BY 1
ORDER BY 1;
```

| ProductBrand | accessories_sale | total | ti_le_mua_phu_kien |
|--------------|-----------------:|------:|-------------------:|
| ALCATEL | 0 | 1 | 0.0 |
| APPLE | 1318 | 1318 | 1.0 |
| BLACKBERRY | 108 | 108 | 1.0 |
| F-MOBILE | 0 | 13 | 0.0 |
| HTC | 0 | 2987 | 0.0 |
| HUAWEI | 0 | 24 | 0.0 |
| LENOVO | 0 | 5410 | 0.0 |
| LG | 0 | 3155 | 0.0 |
| Mobistar | 0 | 8986 | 0.0 |
| NOKIA | 0 | 17584 | 0.0 |
| Q-MOBILE | 0 | 1332 | 0.0 |
| Q-SMART | 0 | 15531 | 0.0 |
| SAMSUNG | 34215 | 34215 | 1.0 |
| SONY | 0 | 4642 | 0.0 |
``
#### Query 9: Which Age Group Has the Highest Installment Purchase Behavior?

```sql
SELECT
  YearOldRange,
  COUNT(Bank) AS installments,
  COUNT(*) AS total_orders,
  COUNT(Bank) / COUNT(*) AS ti_le_installments
FROM `polar-winter-343402.hometest.hackathon_phone_sales`
GROUP BY 1
ORDER BY ti_le_installments DESC;
```

| YearOldRange | installments | total_orders | ti_le_installments |
|--------------|-------------:|-------------:|-------------------:|
| 31-35 | 1553 | 19621 | 0.0791 |
| Duoi 21 | 218 | 3175 | 0.0687 |
| 26-30 | 3626 | 56309 | 0.0644 |
| 21-25 | 122 | 1929 | 0.0632 |
| Tren 40 | 119 | 1911 | 0.0623 |
| 36-40 | 762 | 12361 | 0.0616 |
#### Query 10: Which Phone Brands Are Most Frequently Purchased via Installments?

```sql
SELECT
  ProductBrand,
  COUNT(Bank) AS installments,
  COUNT(*) AS total_orders,
  COUNT(Bank) / COUNT(*) AS ti_le_installments
FROM `polar-winter-343402.hometest.hackathon_phone_sales`
GROUP BY 1
ORDER BY ti_le_installments DESC;
```

| ProductBrand | installments | total_orders | ti_le_installments |
|--------------|-------------:|-------------:|-------------------:|
| APPLE | 169 | 1318 | 0.1282 |
| SONY | 587 | 4642 | 0.1265 |
| HTC | 323 | 2987 | 0.1081 |
| NOKIA | 1859 | 17584 | 0.1057 |
| LG | 285 | 3155 | 0.0903 |
| LENOVO | 355 | 5410 | 0.0656 |
| SAMSUNG | 2235 | 34215 | 0.0653 |
| BLACKBERRY | 4 | 108 | 0.0370 |
| Q-SMART | 468 | 15531 | 0.0301 |
| Mobistar | 115 | 8986 | 0.0128 |
| Q-MOBILE | 0 | 1332 | 0.0 |
| F-MOBILE | 0 | 13 | 0.0 |
| HUAWEI | 0 | 24 | 0.0 |
| ALCATEL | 0 | 1 | 0.0 |

## V. Conclusion & Key Insights

Based on the SQL analysis of the phone sales dataset, the following key insights were identified:

### 🔹 Sales & Customer Trends
- Monthly sales volume shows a generally increasing trend, indicating stable and growing demand.
- The **26–30 age group** is the most valuable segment, contributing the **highest sales volume and revenue**.

### 🔹 Brand & Product Performance
- **Samsung** is the most popular brand across both male and female customers and dominates overall sales volume.
- Certain products (e.g., Samsung Galaxy and Nokia Lumia models) consistently rank among the **top revenue-generating products** across multiple months.
- **Apple, Sony, and HTC** have the **highest installment purchase ratios**, indicating stronger appeal for high-priced or premium products.

### 🔹 Customer Behavior Insights
- Customers aged **26–30** show strong willingness to buy **accessories**, with one of the highest accessory attachment rates.
- Accessory and insurance purchases are highly concentrated in a few brands (notably **Samsung and Apple**), while many brands show untapped cross-selling potential.
- Installment purchases are most common among customers aged **31–35**, suggesting financial flexibility combined with value-conscious behavior.

### 🔹 Business Implications
- Focus marketing and upselling strategies on the **26–30 and 31–35** age groups.
- Expand **accessory and insurance bundling** beyond top brands to increase average order value.
- Promote installment payment options for **premium brands** to improve conversion rates.

Overall, this project demonstrates how SQL can be effectively used to transform raw sales data into actionable business insights, supporting strategic decision-making in sales, pricing, and customer targeting.


