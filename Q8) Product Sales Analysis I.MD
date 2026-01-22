SELECT     P.product_name,S.year,S.price
FROM       Sales AS S
LEFT JOIN Product P
ON         S.product_id=P.product_id



-----

SELECT P.product_name, S.year, S.price
FROM Sales AS S
INNER JOIN Product AS P
ON S.product_id = P.product_id;


---

The problem says:   
   
“for each sale_id in the Sales table”   
   
That just means:  
  
“don’t drop any sales”   

