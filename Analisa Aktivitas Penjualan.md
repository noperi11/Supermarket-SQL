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
ORDER BY branch, gender
````
**Result** :
Branch | Gender | Jumlah|
-------|--------|-------|
A      |Female  |161    |
A	   |Male    |179    |
B	   |Female  |162    |
B	   |Male	|170    |
C	   |Female	|178    |
C	   |Male	|150    |

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/bd0cae36-3e0a-4592-b291-809d04c0c58d)

Barang Yang dijual Tiap Cabang
````sql
select
    branch,
    product_line as Jenis_Produk,
    count(product_line) as Jumlah_Produk
from supermarket
group by branch,product_line
````
**Result**:

Branch|Jenis_Produk|  Jumlah_Produk|
------|------------|----------------|
A     |Electronic accessories	 |60|
A     |Fashion accessories	     |51|
A     |Food and beverages	     |58|
A	  |Health and beauty	     |47|
A	  |Home and lifestyle	     |65|
A	  |Sports and travel	     |59|
B	  |Electronic accessories 	 |55|
B	  |Fashion accessories	     |62|
B	  |Food and beverages	     |50|
B	  |Health and beauty	     |53|
B	  |Home and lifestyle	     |50|
B	  |Sports and travel	     |62|
C	  |Electronic accessories	 |55|
C	  |Fashion accessories     	 |65|
C	  |Food and beverages	     |66|
C	  |Health and beauty	     |52|
C	  |Home and lifestyle	     |45|
C	  |Sports and travel         |45|


Perbandingan Jenis Barang yang Dijual Tiap Cabang dan Gender Pembeli
````sql
SELECT
    branch,
    product_line AS Jenis_Produk,
    COUNT(product_line) AS total_pembeli,
    SUM(CASE WHEN gender = 'Female' THEN 1 ELSE 0 END) AS pembeli_perempuan,
    SUM(CASE WHEN gender = 'Male' THEN 1 ELSE 0 END) AS pembeli_pria
FROM supermarket
GROUP BY branch, product_line;
````
**Result** :
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

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/02a7b153-411d-4fc5-b9e7-491dd133e357)



# Korelasi Pembelian Pada Pembeli Member dan Non-Member
Perbandingan Jenis Pembeli ditiap Cabang
````sql
select 
    branch,
    customer_type as Jenis_Customer,
    count(customer_type) as Jumlah_Customer
from supermarket
group by branch,customer_type
order by branch,customer_type
````
**Result** :
Branch | Jenis_Customer | Jumlah_Customer |
-------|----------------|---------------- |
A	   |Member	        |167              |
A      |Normal	        |173              |
B	   |Member	        |165              |
B	   |Normal	        |167              |
C	   |Member	        |169              |  
C	   |Normal	        |159              |

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/8de378e5-851e-4cf0-b39b-f6df8c693a7e)


Perbandingan Berapa Jumlah barang yang dibeli dari Member dan Non-Member dan juga keuntungan nya
````sql
Select 
    branch,
    customer_type as Jenis_Pembeli,
    sum(quantity) Jumlah_Quantity ,
    round(sum(gross_income)) as Jumlah_Keuntungan
from supermarket
group by customer_type,branch
order by customer_type
````
**Result** :
Cabang |Jenis Pembeli    |Quantity     |Jumlah Keuntungan     |
-------|-----------------|------------------|-----------------|
A	|Member	|964	|2554|
B	|Member	|924	|2557|
C	|Member	|897	|2709|
A	|Normal	|895	|2503|
B	|Normal	|896	|2500|
C	|Normal	|934	|2557|

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/3c0160da-3319-49c1-aee1-9dcecebef7d0)

Penjualan Jenis Produk antara Member dan Non-Member
````sql
select 
customer_type,product_line,count(product_line) as jumlah_penjualan
from supermarket
group by customer_type,product_line
````
**Result** :
Branch|Product Line | Jumlah Penjualan|
------|-------------|-----------------|
Member	|Electronic accessories|	78|
Member	|Fashion accessories   |	86|
Member	|Food and beverages    |    94|
Member	|Health and beauty     |    73|
Member	|Home and lifestyle    |    83|
Member	|Sports and travel     |    87|
Normal	|Electronic accessories|	92|
Normal	|Fashion accessories   |    92|
Normal	|Food and beverages    |    80|
Normal	|Health and beauty     |    79|
Normal	|Home and lifestyle    |    77|
Normal	|Sports and travel     |    79|

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/74029340-09ea-429d-9c1b-6acf2099e45a)


# Korelasi waktu pembelian terhadap penjualan
Waktu Pembelian 
````sql
SELECT
    time_classification as Time,
    COUNT(time_classification) AS jumlah_Pembeli,avg(quantity)
FROM (
    SELECT
        time,quantity,
        CASE
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 0 AND CAST(substr(time, 1, 2) AS INTEGER) < 6 THEN 'Night'
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 6 AND CAST(substr(time, 1, 2) AS INTEGER) < 12 THEN 'Morning'
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 12 AND CAST(substr(time, 1, 2) AS INTEGER) < 18 THEN 'Afternoon'
            ELSE 'Evening'
        END AS time_classification
    FROM supermarket
) AS classified_data 
GROUP BY time_classification

````
**Result**:
Time       |Jumlah_Pembeli|avg(quantity)     |
-----------|--------------|-----------------|
Afternoon  |	528       |	5.57954545454545|
Evening    |	281       |	5.43060498220641|
Morning    |	191       |	5.43455497382199|

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/de7051ab-cd82-4364-9d83-7c2ed2c4778a)

Penjualan Jenis Produk Berdasarkan Waktu
````sql
SELECT
    time_classification as Time,
    COUNT(time_classification) AS jumlah_pembeli,avg(quantity),
    product_line
FROM (
    SELECT
        time,quantity,product_line,
        CASE
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 0 AND CAST(substr(time, 1, 2) AS INTEGER) < 6 THEN 'Night'
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 6 AND CAST(substr(time, 1, 2) AS INTEGER) < 12 THEN 'Morning'
            WHEN CAST(substr(time, 1, 2) AS INTEGER) >= 12 AND CAST(substr(time, 1, 2) AS INTEGER) < 18 THEN 'Afternoon'
            ELSE 'Evening'
        END AS time_classification
    FROM supermarket
) AS classified_data 
GROUP BY time_classification,product_line
````
**Result** :
Time        |Jumlah Pembeli|Product Line          |
------------|--------------|----------------------|
Afternoon	|83	           |Electronic accessories|
Afternoon	|96	           |Fashion accessories   |
Afternoon	|80	           |Food and beverages    |
Afternoon	|83	           |Health and beauty     |
Afternoon	|87	           |Home and lifestyle    |
Afternoon	|99    	       |Sports and travel     |
Evening	    |52	           |Electronic accessories|
Evening	    |54	           |Fashion accessories   |
Evening	    |63	           |Food and beverages    |
Evening	    |42	           |Health and beauty     |
Evening	    |34	           |Home and lifestyle    |
Evening	    |36	           |Sports and travel     |
Morning	    |35	           |Electronic accessories|
Morning	    |28	           |Fashion accessories   |
Morning	    |31	           |Food and beverages    |
Morning	    |27	           |Health and beauty     |
Morning	    |39	           |Home and lifestyle    |
Morning	    |31	           |Sports and travel     |

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/a1904069-de57-46d4-988f-056067f1423b)


# Pola penjualan perbulan
Penjualan Perbulan
````sql
SELECT
    time_classification,count(time_classification)
FROM (
    SELECT
        date,product_line,
        CASE
            WHEN CAST(substr(date, 1) AS INTEGER) = 1 THEN 'January'
            WHEN CAST(substr(date, 1) AS INTEGER) = 2 THEN 'February'
            WHEN CAST(substr(date, 1) AS INTEGER) = 3 THEN 'Maret'
            else 'april'
        END AS time_classification
    FROM supermarket
) AS classified_data 
GROUP BY time_classification
order by substr(date,1)
````
Bulan       |Jumlah Pembeli|
------------|--------------|
January	    |352           |
February	|303           |
Maret	    |345           |

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/192831fa-ce39-43a8-a3fe-e7ed5d1523a4)

Penjualan Jenis Produk Perbulan

````sql
SELECT
    time_classification,count(time_classification),product_line
FROM (
    SELECT
        date,product_line,
        CASE
            WHEN CAST(substr(date, 1) AS INTEGER) = 1 THEN 'January'
            WHEN CAST(substr(date, 1) AS INTEGER) = 2 THEN 'February'
            WHEN CAST(substr(date, 1) AS INTEGER) = 3 THEN 'Maret'
            else 'april'
        END AS time_classification
    FROM supermarket
) AS classified_data 
GROUP BY time_classification,product_line
order by substr(date,1)
````

Bulan       |Jumlah Pembeli |Product Line|
------------|---------------|------------|
January	    |54	|Electronic accessories  |
January	    |70	|Sports and travel       |
January    	|59	|Home and lifestyle      |
January	    |56	|Food and beverages      |
January	    |64	|Fashion accessories     |
January	    |49	|Health and beauty       |
February	|62	|Food and beverages      |
February	|38	|Home and lifestyle      |
February	|54	|Electronic accessories  |
February	|46	|Health and beauty       |
February	|60	|Fashion accessories     |
February	|43	|Sports and travel       |
Maret	    |54	|Fashion accessories     |
Maret	    |53	|Sports and travel       |
Maret	    |57	|Health and beauty       |
Maret	    |63	|Home and lifestyle      |
Maret	    |56	|Food and beverages      |
Maret	    |62	|Electronic accessories  |

![image](https://github.com/noperi11/Supermarket-SQL/assets/126463961/2635357d-9f85-4ead-872c-13c67d515e5e)

