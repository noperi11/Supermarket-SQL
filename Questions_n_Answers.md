# Analisa Aktivitas Penjualan Pada Supermarket
Author : M Ilham Nofriansyah <br/>
Instagram : @nofriansyah_i <br/>
Email : ilhamnofriansyah02@gmail.com <br/>

# Korelasi Dari Gender ke Pola Penjualan
Perbandingan Gender Pembeli di Tiap Cabang
````sql
SELECT
    branch,
    gender,
    COUNT(gender) AS Jumlah
FROM Supermarket
GROUP BY branch, gender
ORDER BY branch, gender;
````
**Result**
Branch | Gender | Jumlah|
-------|--------|-------|
A      |Female  |161    |
A	   |Male    |179    |
B	   |Female  |162    |
B	   |Male	|170    |
C	   |Female	|178    |
C	   |Male	|150    |

Barang yang dijual ditiap Cabang
````sql
select
    branch,
    product_line as Jenis_Barang,
    count(product_line) as Jumlah_barang
from supermarket
group by branch,product_line
````
**Result**

Branch|Jenis_Produk|  Jumlah_Pembeli|
------|------------|---------------|
A     |Electronic accessories	|60|
A     |Fashion accessories	    |51|
A     |Food and beverages	    |58|
A	  |Health and beauty	    |47|
A	  |Home and lifestyle	    |65|
A	  |Sports and travel	    |59|
B	  |Electronic accessories	|55|
B	  |Fashion accessories	    |62|
B	  |Food and beverages	    |50|
B	  |Health and beauty	    |53|
B	  |Home and lifestyle	    |50|
B	  |Sports and travel	    |62|
C	  |Electronic accessories	|55|
C	  |Fashion accessories    	|65|
C	  |Food and beverages	    |66|
C	  |Health and beauty	    |52|
C	  |Home and lifestyle	    |45|
C	  |Sports and travel        |45|


Perbandingan Jenis Barang yang Dijual Tiap Cabang dan Gender Pembeli
````sql
SELECT
    branch,
    product_line AS Jenis_Produk,
    COUNT(product_line) AS total_product,
    SUM(CASE WHEN gender = 'Female' THEN 1 ELSE 0 END) AS total_female,
    SUM(CASE WHEN gender = 'Male' THEN 1 ELSE 0 END) AS total_male
FROM supermarket
GROUP BY branch, product_line;
````
Branch  |Jenis_Produk             |Total_Pembeli   |Pembeli_Perempuan|Pembeli_Pria      |
--------|-------------------------|----------------|-----------------|------------------|
A	    |Electronic accessories	  |  60	           |  28             |	32              |
A	    |Fashion accessories	  |  51	           |  28             |	23              |
A	    |Food and beverages	      |  58	           |  23             |	35              |
A	    |Health and beauty	      |  47	           |  21             |	26              |
A	    |Home and lifestyle	      |  65	           |  32             |	33              |
A	    |Sports and travel	      |  59	           |  29             |	30              |
B	    |Electronic accessories	  |  55	           |  28             |	27              |
B	    |Fashion accessories	  |  62	           |  33             |	29              |
B	    |Food and beverages	      |  50	           |  29             |	21              |
B	    |Health and beauty	      |  53	           |  20             |	33              |
B	    |Home and lifestyle	      |  50	           |  22             |	28              |
B	    |Sports and travel	      |  62	           |  30             |	32              |
C	    |Electronic accessories	  |  55	           |  28             |	27              |
C	    |Fashion accessories	  |  65	           |  35             |	30              |
C	    |Food and beverages	      |  66	           |  38             |	28              |
C	    |Health and beauty	      |  52	           |  23             |	29              |
C	    |Home and lifestyle	      |  45	           |  25             |	20              |
C	    |Sports and travel	      |  45	           |  29             |	16              |

# Korelasi Pembelian Pada Pembeli Member dan Non-Member
Perbandingan Jenis Pembeli ditiap Cabang
````sql
select 
    branch,
    customer_type,
    count(customer_type) as Jumlah_Customer
from supermarket
group by branch,customer_type
order by branch,customer_type
````
Branch | Jenis_Customer | Jumlah_Customer |
-------|----------------|---------------- |
A	   |Member	        |167              |
A      |Normal	        |173              |
B	   |Member	        |165              |
B	   |Normal	        |167              |
C	   |Member	        |169              |  
C	   |Normal	        |159              |


Perbandingan Berapa Jumlah barang yang dibeli dari Member dan Non-Member + keuntungan
````sql
Select 
    branch,
    customer_type,
    avg(quantity) as banyak,
    avg(gross_income)
from supermarket
group by customer_type,branch
order by branch
````
Cabang |Jenis Pembeli    |Banyak            |Gross Income     |
-------|-----------------|------------------|-----------------|
A	   |Member	         |5.77245508982036	|15.29440419161676|
A	   |Normal	         |5.17341040462428	|14.46817919075145|
B	   |Member	         |5.6	            |15.49918787878788|
B	   |Normal	         |5.36526946107784	|14.96805988023952|
C	   |Member	         |5.30769230769231	|16.02741124260355|
C	   |Normal	         |5.87421383647799	|16.078893081761  |

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
    FROM supermarket
) AS classified_data,supermarket
GROUP BY time_classification,gender,branch
````
Rating per products
````sql
select
    branch, 
    product_line,
    avg(rating)
from supermarket
group by branch,product_line
````
Gross income per product
````sql
select
    branch,
    gender,
    product_line,
    avg(gross_income)
from supermarket
group by branch,product_line,gender
````
pengaruh cara pembayaran ke jumlah yang dijual dan gross_income
````sql
Select
    count(payment),
    payment,
    branch,
    avg(gross_income)
from supermarket
group by payment,branch
order by branch
````
