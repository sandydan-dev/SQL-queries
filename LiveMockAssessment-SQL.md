-- Create 'products' table
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name TEXT,
    category TEXT,
    price DECIMAL,
    supplier_id INTEGER
);

-- Insert data into 'products' table
INSERT INTO products (product_id, product_name, category, price, supplier_id) VALUES
(1, 'Mobile Phone', 'Electronics', 25000, 1),
(2, 'Laptop', 'Electronics', 50000, 2),
(3, 'Washing Machine', 'Appliances', 15000, 3),
(4, 'Air Conditioner', 'Appliances', 40000, 2),
(5, 'Headphones', 'Electronics', 2000, 4),
(6, 'Refrigerator', 'Appliances', 30000, 5),
(7, 'Microwave Oven', 'Appliances', 12000, 3),
(8, 'Smart TV', 'Electronics', 45000, 1),
(9, 'Bluetooth Speaker', 'Electronics', 8000, 4),
(10, 'Vacuum Cleaner', 'Appliances', 10000, 6),
(11, 'Tablet', 'Electronics', 22000, 2),
(12, 'Water Purifier', 'Appliances', 12000, 6),
(13, 'Smart Watch', 'Electronics', 15000, 1),
(14, 'DSLR Camera', 'Electronics', 60000, 5),
(15, 'Mixer Grinder', 'Appliances', 3500, 3);

-- Create 'suppliers' table
CREATE TABLE suppliers (
    supplier_id INTEGER PRIMARY KEY,
    supplier_name TEXT,
    city TEXT,
    rating DECIMAL,
    contact_number TEXT
);

-- Insert data into 'suppliers' table
INSERT INTO suppliers (supplier_id, supplier_name, city, rating, contact_number) VALUES
(1, 'Reliance Digital', 'Mumbai', 4.5, '9876543210'),
(2, 'Croma', 'Delhi', 4.2, '9876543211'),
(3, 'Vijay Sales', 'Pune', 4.0, '9876543212'),
(4, 'Bajaj Electronics', 'Hyderabad', 4.3, '9876543213'),
(5, 'Flipkart', 'Bengaluru', 4.7, '9876543214'),
(6, 'Amazon India', 'Chennai', 4.8, '9876543215');

SELECT * FROM products;

SELECT * FROM suppliers;

/* 1 : Write a query to retrieve the product_name of all products.*/
SELECT p.product_name
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/* 2 : Write a query to retrieve the product_name and price of all products.*/
SELECT p.product_name, p.price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/*3 : Write a query to retrieve the supplier_name and city of all suppliers.*/
SELECT s.supplier_name, s.city
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id;

/* 4 :Write a query to retrieve the product_name and price of products 
where the category is 'Electronics'.*/
SELECT p.product_name, p.price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Electronics';

/* 5 :Write a query to fetch the supplier_name and rating of suppliers located in 'Mumbai.'*/
SELECT s.supplier_name, s.rating
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.city = 'Mumbai';

/* 6 : Write a query to fetch all products with a price greater than 30,000.*/
SELECT p.product_name, p.price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.price > 30000;

/*7 : Write a query to fetch the product_name and price of products in the category 'Appliances'
and price less than 20,000.*/
SELECT p.product_name, p.price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Appliances' AND p.price < 20000;

/* 8 :Write a query to retrieve the supplier_name and rating of suppliers
with a rating greater than 4.0 and located in 'Chennai'. */
SELECT s.supplier_name, s.rating
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.rating > 4.0 AND s.city = 'Chennai';

/* 9 : Write a query to fetch products where the category is 'Electronics'
and the price is between 20,000 and 50,000.*/
SELECT p.product_name 
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Electronics' AND p.price BETWEEN 20000 AND 50000;

/*10. Write a query to count the total number of products.*/
SELECT COUNT(p.product_id)
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/*11 : Write a query to find the average price of products in the 'Appliances' category.*/
SELECT AVG(p.price)
FROM products p 
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Appliances';

/* 12 : Write a query to find the most expensive product and its price.*/
SELECT p.product_name, MAX(p.price)
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/*13 : Write a query to count the number of products in the 'Electronics' category.*/ 
SELECT COUNT(p.product_id)
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Electronics';

/*14 : Write a query to find the average price of products supplied by 'Flipkart'.*/
SELECT AVG(p.price)AS avg_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_name = 'Flipkart';

/*15 : Write a query to count the number of suppliers with a rating above 4.0.*/
SELECT COUNT(s.supplier_id)AS total_suppliers
FROM suppliers s 
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.rating > 4.0;

/*16 : Write a query to find the maximum price of products in the 'Appliances' category.*/
SELECT MAX(p.price)AS max_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Appliances';

/*17 : Write a query to count the number of suppliers from 'Delhi' or 'Mumbai'.*/ 
SELECT COUNT(s.supplier_id)AS total_suppliers
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.city = 'Delhi' OR 'Mumbai';

/*18: Write a query to find the minimum price of 'Electronics' products.*/
SELECT MIN(p.price)AS min_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Electronics';

/*19 : Write a query to find the average rating of suppliers located in 'Pune' or 'Bengaluru'.*/
SELECT AVG(s.rating)AS avg_rating
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.city = 'Pune' OR 'Bengaluru';

/*20: Write a query to find the total number of products supplied by 'Amazon India'.*/
SELECT COUNT(p.product_id)AS total_num_product
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_name = 'Amazon India';

/*21 : Write a query to count the number of suppliers located in cities with a rating above 4.5.*/
SELECT s.city, COUNT(s.supplier_id)AS total_suppliers
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.rating = 4.5;

/* 22 : Write a query to find the average price of 'Appliances' products priced above 10,000.*/
SELECT AVG(p.price)AS avg_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Appliances';

/*23 : Write a query to fetch the supplier_name and product_name
for all products supplied by 'Reliance Digital'.*/
SELECT s.supplier_name, p.product_name
FROM suppliers s 
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.supplier_name = 'Reliance Digital';

/*24 : Write a query to fetch the supplier_name and product_name 
for all products priced above 40,000.*/
SELECT s.supplier_name, p.product_name
FROM suppliers s 
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE p.price > 40000;

/*25 : Write a query to fetch the supplier_name, product_name,
and price for products in the 'Electronics' category supplied by suppliers located in 'Mumbai'.*/
SELECT s.supplier_name, p.product_name, p.price
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE p.category = 'Electronics' AND s.city = 'Mumbai';


/*26 : Write a query to fetch the product_name, category, and price for products
that are either in the 'Furniture' category or priced above 30,000.*/
SELECT p.product_name, p.category , p.price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Furniture' OR p.price > 30000;

/*27 : Write a query to find the total price of all products 
supplied by 'Croma' with a price less than 50,000.*/
SELECT SUM(p.price)AS total_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_name = 'Croma' AND p.price < 50000;


/*28 : Write a query to fetch the product_name, price, and 
category for products that belong to either the 'Appliances' or 'Furniture' category.*/
SELECT p.product_name, p.price, p.category
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Appliances' OR 'Furniture';

/*29 : Write a query to count the number of products where the 
category is 'Electronics' and the price is between 20,000 and 60,000.*/
SELECT COUNT(p.product_id)AS total_num_products
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.category = 'Electronics' AND p.price BETWEEN 20000 AND 60000;


/*30 : Write a query to fetch the supplier_name and the number of products
supplied by each supplier where the supplier is located in 'Hyderabad' or 'Bengaluru'.*/
SELECT s.supplier_name
FROM suppliers s
INNER JOIN products p ON s.supplier_id = p.supplier_id
WHERE s.city IN ('Hyderabad', 'Bengaluru');

