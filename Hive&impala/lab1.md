## big data engineering 2차시 수업 mes o.g 정수현 선임 수업실습


<pre><code>
select * from customers where fname like 'Brid%' and city = 'Kansas City'


 	cust_id	fname	lname	address	city	state	zipcode
1	1139477	Bridget	Burch	1644 East 7th Street	Kansas City	KS	66119






To see live updates on a query's progress, run 'set LIVE_SUMMARY=1;'.
***********************************************************************************
[localhost.localdomain:21000] > SELECT * FROM products order by price DESC limit 3;
Query: select * FROM products order by price DESC limit 3
+---------+------------+-----------------------------------------------+--------+--------+-------------+
| prod_id | brand      | name                                          | price  | cost   | shipping_wt |
+---------+------------+-----------------------------------------------+--------+--------+-------------+
| 1274321 | Byteweasel | Hadoop Cluster, Economy (4-node)              | 975149 | 952934 | 570         |
| 1274308 | Gigabux    | Server (2U rackmount, eight-core, 64GB, 12TB) | 614559 | 556183 | 121         |
| 1274307 | Krustybitz | Server (2U rackmount, eight-core, 64GB, 12TB) | 599319 | 542497 | 121         |
+---------+------------+-----------------------------------------------+--------+--------+-------------+
Fetched 3 row(s) in 0.53s


[training@localhost queries]$ impala-shell -f verify_tablet_order.sql
Starting Impala Shell without Kerberos authentication
Connected to localhost.localdomain:21000
Server version: impalad version 2.6.0-cdh5.8.0 RELEASE (build 8d8652f69461f0dd8d5f474573fb5de7ceb0ee6b)
Query: -- Query to find the order for the
-- tablet (product ID 1274348) from the
-- contest winner (customer ID 1139477)
SELECT o.order_id, fname, lname, o.order_date
FROM customers c
JOIN orders o
   ON (c.cust_id = o.cust_id)
JOIN order_details d
   ON (o.order_id = d.order_id)
WHERE d.prod_id=1274348
  AND c.cust_id=1139477
+----------+---------+-------+---------------------+
| order_id | fname   | lname | order_date          |
+----------+---------+-------+---------------------+
| 6662689  | Bridget | Burch | 2013-05-31 17:31:11 |
| 6621368  | Bridget | Burch | 2013-05-20 21:17:03 |
+----------+---------+-------+---------------------+
Fetched 2 row(s) in 1.56s





0: jdbc:hive2://localhost:10000> select * from products where brand = 'Gigabux' and price > 10 and price < 1000;
INFO  : Compiling command(queryId=hive_20190410215454_1741da81-fecd-4815-9062-d673e959976a): select * from products where brand = 'Gigabux' and price > 10 and price < 1000
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:products.prod_id, type:int, comment:null), FieldSchema(name:products.brand, type:string, comment:null), FieldSchema(name:products.name, type:string, comment:null), FieldSchema(name:products.price, type:int, comment:null), FieldSchema(name:products.cost, type:int, comment:null), FieldSchema(name:products.shipping_wt, type:int, comment:null)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190410215454_1741da81-fecd-4815-9062-d673e959976a); Time taken: 0.1 seconds
INFO  : Executing command(queryId=hive_20190410215454_1741da81-fecd-4815-9062-d673e959976a): select * from products where brand = 'Gigabux' and price > 10 and price < 1000
INFO  : Completed executing command(queryId=hive_20190410215454_1741da81-fecd-4815-9062-d673e959976a); Time taken: 0.002 seconds
INFO  : OK
+-------------------+-----------------+----------------------------------------------------------+-----------------+----------------+-----------------------+--+
| products.prod_id  | products.brand  |                      products.name                       | products.price  | products.cost  | products.shipping_wt  |
+-------------------+-----------------+----------------------------------------------------------+-----------------+----------------+-----------------------+--+
| 1273740           | Gigabux         | Batteries (AA, 4 pack)                                   | 669             | 481            | 2                     |
| 1273759           | Gigabux         | Batteries (D, 2 pack)                                    | 959             | 353            | 2                     |
| 1273904           | Gigabux         | 1/4 in. Standard Phone Female to Female Adapter          | 399             | 397            | 1                     |
| 1273906           | Gigabux         | 1/4 in. Standard Phone Female to Female Adapter          | 399             | 229            | 1                     |
| 1273918           | Gigabux         | RCA Phono Male to Mini Female Adapter                    | 419             | 198            | 1                     |
| 1273920           | Gigabux         | RCA Phono Male to Mini Female Adapter                    | 409             | 404            | 1                     |
| 1273932           | Gigabux         | RCA Phono Male to 1/4 in. Standard Phone Female Adapter  | 629             | 579            | 1                     |
| 1273941           | Gigabux         | 3-Pin XLR Male to Male, Barrel Adapter                   | 749             | 551            | 1                     |
| 1273994           | Gigabux         | Phono Jack to UHF Plug                                   | 619             | 316            | 1                     |
| 1273996           | Gigabux         | Phono Jack to F Plug                                     | 509             | 470            | 1                     |
+-------------------+-----------------+----------------------------------------------------------+-----------------+----------------+-----------------------+--+
10 rows selected (0.206 seconds)
0: jdbc:hive2://localhost:10000>


</code></pre>
