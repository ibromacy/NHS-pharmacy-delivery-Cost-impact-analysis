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

-2.Standardize the data by checking through the key columns to correct and update uneven data and changing the date datatype into the standard date, for example
SELECT transaction_id,supplier_name
FROM nhs_pharma2
WHERE supplier_name LIKE 'Gl%'; 

SELECT transaction_id,supplier_name
FROM nhs_pharma2
WHERE supplier_name LIKE 'He%'; 

SELECT transaction_id,supplier_name
FROM nhs_pharma2
WHERE supplier_name LIKE 'Me%'; 

SELECT transaction_id,supplier_name
FROM nhs_pharma2
WHERE supplier_name LIKE 'NHS%'; 

SELECT transaction_id,supplier_name
FROM nhs_pharma2
WHERE supplier_name LIKE 'UK%'; 

UPDATE nhs_pharma2
SET product_name = CASE
    WHEN product_name IN ('GlobalMeds', 'GLOBALMEDS') THEN 'GlobalMeds'
    WHEN product_name IN ('HealQuick','HEALQUICK') THEN 'HealQuick'
    WHEN product_name IN ('MediSupply Ltd','MEDISUPPLY LTD')THEN 'MediSupply Ltd'
    WHEN product_name IN ('NHS Supply Chain','NHS SUPPLY CHAIN')THEN 'NHS Supply Chain'
    WHEN Product_name IN ('UKPharma Dist','UKPHARMA DIST')THEN 'UkPharma Dist'
    ELSE product_name
END;

SELECT 
  `order_date` AS original_date,
  CASE
    WHEN `order_date` LIKE '____.__.__' THEN STR_TO_DATE(`order_date`, '%Y.%m.%d')
    WHEN `order_date` LIKE '__-___-____' THEN STR_TO_DATE(`order_date`, '%d-%b-%Y')
    WHEN `order_date` LIKE '__/__/____' THEN STR_TO_DATE(`order_date`, '%d/%m/%Y')
    WHEN `order_date` LIKE '____/__/__' THEN STR_TO_DATE(`order_date`, '%Y/%m/%d')
    WHEN `order_date` LIKE '____-__-__' THEN STR_TO_DATE(`order_date`, '%Y-%m-%d')
     ELSE CAST(TRIM(`order_date`) AS CHAR)
  END AS standardized_date
FROM nhs_pharma2;

UPDATE nhs_pharma2
SET `order_date`= CASE
					WHEN `order_date` LIKE '____.__.__' THEN STR_TO_DATE(`order_date`, '%Y.%m.%d')
					WHEN `order_date` LIKE '__-___-____' THEN STR_TO_DATE(`order_date`, '%d-%b-%Y')
					WHEN `order_date` LIKE '__/__/____' THEN STR_TO_DATE(`order_date`, '%d/%m/%Y')
					WHEN `order_date` LIKE '____/__/__' THEN STR_TO_DATE(`order_date`, '%Y/%m/%d')
					WHEN `order_date` LIKE '____-__-__' THEN STR_TO_DATE(`order_date`, '%Y-%m-%d')
						ELSE NULL
					END ;

SELECT `order_date`
FROM nhs_pharma2
LiMIT 20;

-3. Remove null or blank values from key columns
SELECT *
FROM nhs_pharma2
WHERE transaction_id IS NULL
OR transaction_id=''
ORDER BY 1;

UPDATE nhs_pharma2
SET `transaction_id`=''
WHERE transaction_id IS NULL;

DELETE FROM nhs_pharma2
WHERE transaction_id IS NULL;

-4.Remove any redunctant columns
ALTER TABLE nhs_pharma2
DROP COLUMN row_num; 


