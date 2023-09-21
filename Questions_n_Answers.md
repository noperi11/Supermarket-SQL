Perbandingan Gender Pembeli di Tiap Cabang
````sql
SELECT
    branch,
    gender,
    COUNT(gender) AS Jumlah
FROM sss
GROUP BY branch, gender
ORDER BY branch, gender;
````
branch | Gender | Jumlah|
-------|--------|-------|
A   |Female |161 |
A	|Male   |179 |
B	|Female |162 |
B	|Male	|170 |
C	|Female	|178 |
C	|Male	|150 |

Perbandingan Jenis Pembeli ditiap Cabang
````sql
select 
    branch,
    customer_type,
    count(customer_type)
from sss
group by branch,customer_type
order by branch,customer_type
````
Perbandingan Jenis Barang yang dijual ditiap cabang

````sql
SELECT
    branch,
    product_line,
    COUNT(product_line) AS total_product,
    SUM(CASE WHEN gender = 'Female' THEN 1 ELSE 0 END) AS total_female,
    SUM(CASE WHEN gender = 'Male' THEN 1 ELSE 0 END) AS total_male
FROM sss
GROUP BY branch, product_line;
````

Perbandingan Berapa Jumlah barang yang dibeli dari Member dan Non-Member
````sql
Select 
    sum(quantity) as banyak,
    customer_type,
    branch
from sss
group by customer_type,branch
order by branch
````
Perbandingan cara pembayaran
````sql
Select
    count(payment),
    payment,
    branch
from sss
group by payment,branch
order by branch
````
waktu pembelian
````sql
SELECT
    time_classification,
    COUNT(*) AS jumlah_data,
    gender,branch
FROM (
    SELECT
        time,
        CASE
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 0 AND CAST(substr(time, 1, 2) AS INTEGER) < 6 THEN 'Night'
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 6 AND CAST(substr(time, 1, 2) AS INTEGER) < 12 THEN 'Morning'
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 12 AND CAST(substr(time, 1, 2) AS INTEGER) < 18 THEN 'Afternoon'
            ELSE 'Evening'
        END AS time_classification
    FROM sss
) AS classified_data,sss
GROUP BY time_classification,gender,branch
````
Rating per products
````sql
select
    branch, 
    product_line,
    avg(rating)
from sss
group by branch,product_line
````
Gross income per product
````sql
select
    branch,
    gender,
    product_line,
    avg(gross_income)
from sss
group by branch,product_line,gender
````
pengaruh cara pembayaran ke jumlah yang dijual dan gross_income
````sql
Select
    count(payment),
    payment,
    branch,
    avg(gross_income)
from sss
group by payment,branch
order by branch
````
