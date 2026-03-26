# SQL--Phone-Sales-Dataset
# [SQL] How to Improve Sales Performance? – Retail Analytics

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/5f25109b-0b96-4b92-ae7c-ea2b2e8a8849" />

## Table of Contents
I. [📌 Introduction](#I.-Introduction)

II. [📂 Dataset](#II.-Dataset)

III. [🧠 Main Process](#III.-Main-Process)

IV. [📊 Exploring the Dataset](#IV.-Exploring-the-Dataset)

V. [🔎 Final Conclusion](#V.-Conclusion)

## I. Introduction
This project focuses on analyzing sales data from an electronics retail business, specifically centered around phone and accessory transactions. The primary goal is to extract meaningful insights from the data that can help improve sales strategies, understand customer preferences, and enhance product offerings.

## II. Dataset
The analysis is based on two datasets:

📂 Phone_Sales: Contains transactions with detailed information about phone purchases, including customer demographics (gender, age range), product specifications (brand, color, carrier), payment method, and geographic location.

📂 Accessories_Sales: Includes records of accessory purchases, capturing product type, subcategory, and sales information. It links customer codes and transaction IDs with unit prices and sales values.

## III. Main Process
The project followed a structured data analysis process:
* Data Extraction: Data was extracted from Excel sheets into structured tables.
* Data Cleaning: Null values and inconsistencies (e.g., missing bank names) were reviewed.
* Data Exploration: Key fields such as unit price, product brand, customer demographics, and geographic area were examined.
* Data Insights: Patterns in sales performance, product preference, and customer segments were identified using SQL queries.

## IV. Exploring the Dataset
### Query 01: How many orders are there in each month? (transactionID)
[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:b5b679bf63d74a3cb8e87c4658323a87)
* SQL code

![image](https://github.com/user-attachments/assets/0e57a657-027f-476d-a073-e3a7b9b12de0)

* Query results

![image](https://github.com/user-attachments/assets/af7df9eb-7e4a-410d-b24c-a99196bf2dfc)

### Query 02: How many customers made purchases each month? (customer_code)
[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:454b35ae089f4c2b82563acf8bf92db7)
* SQL code

![image](https://github.com/user-attachments/assets/c96ebfbc-7bba-44ce-ab4f-74887d21dfdf)

* Query results

![image](https://github.com/user-attachments/assets/428c52b2-c356-405d-b632-95bc0f6b343d)

### Query 03: Among male and female customers, which phone brands are the most popular? List the top 3 based on transactionID count
[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:47247fb770f2435c874275db81d007da)
* SQL code

![image](https://github.com/user-attachments/assets/939bc402-da07-4375-9aee-1e4d35abaed7)

* Query results

![image](https://github.com/user-attachments/assets/be168214-cbcc-4530-896a-967b43970867)

### Query 04: Which age group buys the most, and which age group generates the highest revenue? What conclusions can you draw? 
(Use the Unit field to calculate quantity purchased, or use transaction count)

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:28a05cc7dea647c3ab875203a89f98e8)
* SQL code

![image](https://github.com/user-attachments/assets/8cf57cda-3037-4c8f-9149-dfa695e75fad)

* Query results

![image](https://github.com/user-attachments/assets/b66f11d6-58e1-4668-a39f-c238a1087098)

![image](https://github.com/user-attachments/assets/45211763-da5c-4ba0-a4ff-e2090e7a166f)

### Query 05: What are the top 3 phone products generating the highest revenue each month? Provide business insights if any (SalesValue)
[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:134fa0360cf04d869d16635d70432076)
* SQL code

![image](https://github.com/user-attachments/assets/a311c758-f6a9-4ff7-a521-c9bbf218477b)

* Query results

![image](https://github.com/user-attachments/assets/0d7b168e-0214-4489-ac6f-01f86f4f7fba)

### Query 06: Which brand is most preferred by customers aged 26–30? (transactionID)
[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:974602a6f4ab423c8aa814873a458c7d)
* SQL code

![image](https://github.com/user-attachments/assets/4479c5fb-1e1c-46b9-8e53-4389a7a19e0b)

* Query results

![image](https://github.com/user-attachments/assets/9c9d7671-3852-4fd0-9779-631565986839)

### Query 07: Are customers aged 26–30 willing to make additional purchases for accessories and insurance? 
(Combine accessories and insurance together)

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:5508d077db6146bb81fd7efb50fd6b17)
* SQL code

![image](https://github.com/user-attachments/assets/a6196848-b75a-41f1-8a38-caffc3cc87ea)

* Query results

![image](https://github.com/user-attachments/assets/70800feb-73e5-49d4-aace-49af70c04606)

### Query 08: Do customer groups of each brand buy accessories and insurance? 
Provide insights. (Combine accessories and insurance together)

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:94f7ea8844cc4a10be3580ce918bffa0)
* SQL code

![image](https://github.com/user-attachments/assets/1a5f09ca-3cdd-47ef-b82b-b787b4ee7055)

* Query results

![image](https://github.com/user-attachments/assets/da642af7-b997-40c0-aa98-c69543fc0fe9)

### Query 09: Which age group shows the highest tendency to buy on installment plans? (based on transactionID count)
[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:7685860ff9194c49acbb01fa0d816d3e)
* SQL code

![image](https://github.com/user-attachments/assets/da1a3104-ae95-4258-b529-4631b9045e50)

* Query results

![image](https://github.com/user-attachments/assets/c8ee5a32-8c14-46bd-90c6-46fb3a05b559)

### Query 10: Which phone brand is most frequently purchased via installment plans? (based on transactionID count)
[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:889e2cb87b8046cca8e97e44b022a6ac)
* SQL code

![image](https://github.com/user-attachments/assets/a1ea22d7-aa80-4a99-b5a7-a6dfc29fd6bc)

* Query results

![image](https://github.com/user-attachments/assets/bac0fc35-e7f3-4c39-bea2-dc2b5e4c3dee)

## V. Conclusion
This project demonstrates how sales and customer data can be utilized to better understand market behavior and business performance. Through SQL-driven analysis on phone and accessories sales, valuable insights into customer demographics, product trends, and pricing strategies were uncovered. These findings can help inform marketing campaigns, inventory planning, and overall strategic decision-making for the business.
