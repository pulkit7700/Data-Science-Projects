Sure! Here's the conversion of the given queries into a Markdown file:

### TASK 1

```sql
/*
1.1.	Write a query to display customer full name with their title (Mr/Ms), both first name and last name are in upper case, 
customer email id, customer creation date and display customer’s category after applying below categorization rules: 
i) IF customer creation date Year <2005 Then Category A 
ii) IF customer creation date Year >=2005 and <2011 Then Category B 
iii)IF customer creation date Year>= 2011 Then Category C 
Hint: Use CASE statement, no permanent change in table required. 
[NOTE: TABLES to be used - ONLINE_CUSTOMER TABLE]
*/ 

SELECT 
  CASE OC.CUSTOMER_GENDER
    WHEN 'M' THEN UPPER(CONCAT('Mr. ', CUSTOMER_FNAME, " ", CUSTOMER_LNAME))
    WHEN 'F' THEN UPPER(CONCAT('Ms. ', CUSTOMER_FNAME, " ", CUSTOMER_LNAME))
  END AS Full_Name,
  OC.CUSTOMER_EMAIL,
  OC.CUSTOMER_CREATION_DATE,
  CASE
    WHEN OC.CUSTOMER_CREATION_DATE < '2005-01-01' THEN 'Category A'
    WHEN OC.CUSTOMER_CREATION_DATE BETWEEN '2005-01-01' AND '2011-01-01' THEN 'Category B'
    ELSE 'Category C'
  END AS Customer_Category  
FROM orders.online_customer OC;
```

### TASK 2

```sql
/*
2. Write a query to display the following information for the products, which have not been sold: product_id, product_desc, product_quantity_avail, 
product_price, inventory values (product_quantity_avail*product_price), 
New_Price after applying discount as per below criteria. Sort the output with respect to decreasing value of Inventory_Value. 
i) IF Product Price > 20,000 then apply 20% discount 
ii) IF Product Price > 10,000 then apply 15% discount 
iii) IF Product Price =< 10,000 then apply 10% discount 
# Hint: Use CASE statement, no permanent change in table required. 
[NOTE: TABLES to be used - PRODUCT, ORDER_ITEMS TABLE]
*/

SELECT 
  product_id, 
  product_desc, 
  product_quantity_avail, 
  product_price,
  product_quantity_avail * product_price AS Inventory_Value,
  CASE
    WHEN PRODUCT_PRICE > 20000 THEN PRODUCT_PRICE - (0.20 * PRODUCT_PRICE)
    WHEN PRODUCT_PRICE > 10000 THEN PRODUCT_PRICE - (0.15 * PRODUCT_PRICE)
    WHEN PRODUCT_PRICE <= 10000 THEN PRODUCT_PRICE - (0.10 * PRODUCT_PRICE)
  END AS New_Price
FROM orders.product
LEFT JOIN orders.order_items USING (PRODUCT_ID)
WHERE orders.order_items.PRODUCT_ID IS NULL
ORDER BY Inventory_Value DESC;
```

### TASK 3

```sql
/*
3.	Write a query to display Product_class_code, Product_class_description, Count of Product type in each productclass, Inventory Value (product_quantity_avail*product_price). 
Information should be displayed for only those product_class_code which have more than 1,00,000. Inventory Value. Sort the output with respect to decreasing value of Inventory_Value. 
[NOTE: TABLES to be used - PRODUCT_CLASS, PRODUCT_CLASS_CODE]
*/

SELECT 
  P.PRODUCT_CLASS_CODE,
  P.PRODUCT_DESC,
  PC.PRODUCT_CLASS_DESC AS PRODUCT_TYPE,
  (P.PRODUCT_PRICE * P.PRODUCT_QUANTITY_AVAIL) AS INVENTORY_VALUE
FROM orders.product P
JOIN orders.product_class PC ON P.PRODUCT_CLASS_CODE =

 PC.PRODUCT_CLASS_CODE
WHERE (P.PRODUCT_PRICE * P.PRODUCT_QUANTITY_AVAIL) > 100000
ORDER BY INVENTORY_VALUE DESC;
```

### TASK 4

```sql
/*
4.	Write a query to display customer_id, full name, customer_email, customer_phone and country of customers who have cancelled all the orders placed by them (USE SUB-QUERY)
[NOTE: TABLES to be used - ONLINE_CUSTOMER, ADDRESSS, ORDER_HEADER]
*/

SELECT
  CUSTOMER_ID,
  CONCAT(CUSTOMER_FNAME, ' ', CUSTOMER_LNAME) AS Full_Name,
  CUSTOMER_EMAIL,
  CUSTOMER_PHONE,
  COUNTRY
FROM orders.online_customer
JOIN orders.order_header USING (CUSTOMER_ID)
JOIN orders.address USING (ADDRESS_ID)
WHERE ORDER_STATUS = 'Cancelled';
```

### TASK 5

```sql
/*
5. Write a query to display Shipper name, City to which it is catering, 
number of customer catered by the shipper in the city and number of consignments delivered to that city for Shipper DHL 
[NOTE: TABLES to be used - SHIPPER,ONLINE_CUSTOMER, ADDRESSS, ORDER_ITEMS]
*/

SELECT
  S.SHIPPER_NAME,
  A.CITY,
  COUNT(DISTINCT OC.CUSTOMER_ID) AS CUSTOMER_COUNT,
  COUNT(DISTINCT O.ORDER_ID) AS CONSIGNMENT_COUNT
FROM
  SHIPPER S
  LEFT JOIN ADDRESS A ON S.SHIPPER_ADDRESS = A.ADDRESS_ID
  LEFT JOIN ONLINE_CUSTOMER OC ON OC.ADDRESS_ID = A.ADDRESS_ID
  LEFT JOIN ORDER_HEADER O ON O.CUSTOMER_ID = OC.CUSTOMER_ID
WHERE
  S.SHIPPER_NAME = 'DHL'
GROUP BY
  S.SHIPPER_NAME,
  A.CITY;

```

### TASK 6

```sql
/*
6.	Write a query to display product_id, product_desc, product_quantity_avail, quantity sold and show inventory Status of products as below as per below condition: 
a. For Electronics and Computer categories, if sales till date is Zero then show 'No Sales in past, give discount to reduce inventory', 
if inventory quantity is less than 10% of quantity sold,show 'Low inventory, need to add inventory', if inventory quantity is less 
than 50% of quantity sold, show 'Medium inventory, need to add some inventory', if inventory quantity is more or equal to 50% of quantity sold, show 'Sufficient inventory' 
b. For Mobiles and Watches categories, if sales till date is Zero then show 'No Sales in past, give discount to reduce inventory', if inventory quantity is less than 20% 
of quantity sold, show 'Low inventory, need to add inventory', if inventory quantity is less than 60% of quantity sold, show 'Medium inventory, need to add some inventory',
 if inventory quantity is more or equal to 60% of quantity sold, show 'Sufficient inventory' c. Rest of the categories, if sales till date is Zero then show 'No Sales in past,
 give discount to reduce inventory', if inventory quantity is less than 30% of quantity sold, show 'Low inventory, need to add inventory', if inventory quantity is less than 
 70% of quantity sold, show 'Medium inventory, need to add some inventory', if inventory quantity is more or equal to 70% of quantity sold, show 'Sufficient inventory' 
 -- (USE SUB-QUERY) -- [NOTE: TABLES to be used - PRODUCT, PRODUCT_CLASS, ORDER_ITEMS]

*/

SELECT 
  orders.product.PRODUCT_ID,
  orders.product_class.PRODUCT_CLASS_DESC,
  orders.product.PRODUCT_DESC,
  orders.product_class.PRODUCT_CLASS_CODE,
  PRODUCT_QUANTITY_AVAIL,
  PRODUCT_QUANTITY AS QUANTITY_SOLD,
  CASE 
    WHEN PRODUCT_CLASS_DESC IN ('Electronics', 'Computer') THEN 
      CASE
        WHEN PRODUCT_QUANTITY_AVAIL < 10 THEN 'Low inventory, need to add inventory'
        WHEN PRODUCT_QUANTITY_AVAIL <= 50 THEN 'Medium inventory, need to add some inventory'
        ELSE 'Sufficient inventory' 
      END
    WHEN PRODUCT_CLASS_DESC IN ('Mobiles', 'Watches') THEN
      CASE
        WHEN PRODUCT_QUANTITY

_AVAIL < 20 THEN 'Low inventory, need to add inventory'
        WHEN PRODUCT_QUANTITY_AVAIL <= 60 THEN 'Medium inventory, need to add some inventory'
        ELSE 'Sufficient inventory' 
      END
    WHEN PRODUCT_QUANTITY_AVAIL < 30 THEN 'Low inventory, need to add inventory'
    WHEN PRODUCT_QUANTITY_AVAIL <= 70 THEN 'Medium inventory, need to add some inventory'
    ELSE 'Sufficient inventory' 
  END AS INVENTORY_STATS
FROM orders.product
JOIN orders.product_class ON orders.product.PRODUCT_CLASS_CODE = orders.product_class.PRODUCT_CLASS_CODE
JOIN orders.order_items ON orders.product.PRODUCT_ID = orders.order_items.PRODUCT_ID;
```

### TASK 7 

```sql
/*
7.	Write a query to display order_id and volume of the biggest order (in terms of volume) that can fit in carton id 10 -- [NOTE: TABLES to be used - CARTON, ORDER_ITEMS, PRODUCT]
*/

SELECT 
  OH.ORDER_ID,
  (orders.product.LEN * orders.product.WEIGHT * orders.product.HEIGHT) AS Volume
FROM orders.order_items
JOIN orders.product USING (PRODUCT_ID)
WHERE (orders.product.LEN * orders.product.WEIGHT * orders.product.HEIGHT) < 18000000
ORDER BY (orders.product.LEN * orders.product.WEIGHT * orders.product.HEIGHT) DESC;
```

### TASK 8 

```sql
/*
8.	Write a query to display customer id, customer full name, total quantity and total value (quantity * price) shipped where mode of payment is Cash 
and customer last name starts with 'A' -- WE TOOK A AS THERE WAS NOBODY WITH NAME 'G'
--[NOTE: TABLES to be used - ONLINE_CUSTOMER, ORDER_ITEMS, PRODUCT, ORDER_HEADER]
*/

SELECT
  OC.CUSTOMER_ID AS Customer_ID,
  CONCAT(CUSTOMER_FNAME, ' ', CUSTOMER_LNAME) AS Customer_FullName,
  OH.ORDER_ID AS Order_ID,
  P.PRODUCT_PRICE * OI.PRODUCT_QUANTITY AS Total_Value
FROM orders.online_customer OC
JOIN orders.order_header OH ON OH.CUSTOMER_ID = OC.CUSTOMER_ID
JOIN orders.order_items OI ON OI.ORDER_ID = OH.ORDER_ID
JOIN orders.product P ON P.PRODUCT_ID = OI.PRODUCT_ID
WHERE OH.PAYMENT_MODE = 'Cash' AND LEFT(CUSTOMER_LNAME, 1) = 'A'
GROUP BY OH.ORDER_ID
ORDER BY Customer_ID;
```

### TASK 9

```sql
/*
9.	Write a query to display product_id, product_desc and total quantity of products which are sold together with product id 201 and are not shipped to city Bangalore and New Delhi. 
Display the output in descending order with respect to the tot_qty. 
-- (USE SUB-QUERY) -- [NOTE: TABLES to be used - order_items, product, order_head, online_customer, address]
*/

SELECT
  P.PRODUCT_ID,
  P.PRODUCT_DESC,
  SUM(OI.PRODUCT_QUANTITY) AS Total_Quantity
FROM orders.order_items OI
JOIN orders.product P ON P.PRODUCT_ID = OI.PRODUCT_ID
JOIN orders.order_header OH ON OH.ORDER_ID = OI.ORDER_ID
JOIN orders.online_customer OC ON OC.CUSTOMER_ID = OH.CUSTOMER_ID
JOIN orders.address A ON A.ADDRESS_ID = OC.ADDRESS_ID
WHERE OH.ORDER_STATUS = 'Shipped'
  AND A.CITY NOT IN ('Bangalore', 'New Delhi')
  AND OI.ORDER_ID IN (
    SELECT ORDER_ID
    FROM orders.order_items
    WHERE PRODUCT_ID

 = 201
  )
GROUP BY P.PRODUCT_ID, P.PRODUCT_DESC
ORDER BY Total_Quantity DESC;
```

### TASK 10

```sql
/*
10.	Write a query to display the total value (quantity*price) of shipped orders for each mode of payment where payment received date is after 01st Jan 2007 
and shipment date is after 01st May 2008 -- [NOTE: TABLES to be used - order_items, product, order_head]
*/

SELECT
  OH.PAYMENT_MODE AS Payment_Mode,
  SUM(OI.PRODUCT_QUANTITY * P.PRODUCT_PRICE) AS Total_Value
FROM orders.order_items OI
JOIN orders.product P ON P.PRODUCT_ID = OI.PRODUCT_ID
JOIN orders.order_header OH ON OH.ORDER_ID = OI.ORDER_ID
WHERE OH.PAYMENT_RECEIVED_DATE > '2007-01-01'
  AND OH.SHIPMENT_DATE > '2008-05-01'
  AND OH.ORDER_STATUS = 'Shipped'
GROUP BY OH.PAYMENT_MODE;
```

