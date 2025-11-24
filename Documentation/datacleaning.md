### **Data Cleaning SQL Checks Used**
```sql
-Created a staging table not to work directly on the original datasets
 CREATE TABLE nhs_pharma
LIKE nhs_pharma_messy;

INSERT nhs_pharma 
SELECT *
FROM nhs_pharma_messy;

- 1.Remove duplicates by assigning row numbers to identify duplicate rows
SELECT *,
row_number()over(Partition by transaction_id,product_code,order_date) as row_num
FROM nhs_pharma;

WITH duplicate_cte AS
(SELECT *,
row_number()over(Partition by transaction_id,product_code,order_date) as row_num
FROM nhs_pharma
)
SELECT *
FROM duplicate_cte
WHERE row_num >1 ;

DELETE
FROM nhs_pharma2
WHERE row_num>1;

-2.Standardize the data
