
````sql
SELECT
    branch,
    gender,
    COUNT(gender) AS Jumlah
FROM baru
GROUP BY branch, gender
ORDER BY branch, gender;

````
