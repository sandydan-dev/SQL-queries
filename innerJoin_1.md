/*
Working with SQLFiddle on site,
I have created a SQL query that will return the desired result. Here is the query:

Key points :
INNER JOIN returns only the rows where there is a match in both tables.

It is useful for combining related data from different tables.

Ensure that the columns used in the ON clause are related and correctly represent the relationship between the tables.

Common Use Cases:

Merging data from different tables, such as orders and customers.

Retrieving related information from multiple tables.

Performing complex queries involving multiple tables with related data.

*/

-- Create the products table
CREATE TABLE products (
id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
category TEXT NOT NULL,
quantity_in_stock INTEGER,
unit_price REAL,
reorder_level INTEGER,
supplier_id INTEGER,
supplier_location TEXT
);

-- Insert data into the products table
INSERT INTO products (product_name, category, quantity_in_stock, unit_price, reorder_level, supplier_id, supplier_location) VALUES
('Smartphone', 'Mobiles', 150, 299.99, 20, 1, 'Delhi'),
('Laptop', 'Computers', 75, 899.99, 10, 2, 'Mumbai'),
('Headphones', 'Audio', 200, 49.99, 50, 3, 'Bangalore'),
('Smartwatch', 'Wearables', 120, 149.99, 15, 4, 'Chennai'),
('Tablet', 'Tablets', 90, 249.99, 30, 5, 'Hyderabad'),
('Monitor', 'Computers', 60, 179.99, 20, 2, 'Mumbai'),
('Bluetooth Speaker', 'Audio', 110, 89.99, 25, 3, 'Bangalore'),
('Keyboard', 'Accessories', 300, 29.99, 100, 6, 'Delhi'),
('Mouse', 'Accessories', 350, 19.99, 150, 6, 'Delhi'),
('Printer', 'Office Supplies', 40, 129.99, 5, 7, 'Chennai');

-- Create the suppliers table
CREATE TABLE suppliers (
supplier_id INTEGER PRIMARY KEY,
supplier_name TEXT NOT NULL,
contact_number TEXT,
supplier_location TEXT,
contact_email TEXT
);

-- Insert data into the suppliers table
INSERT INTO suppliers (supplier_name, contact_number, supplier_location, contact_email) VALUES
('Tech Supplies Inc', '9876543210', 'Delhi', 'contact@techsupplies.com'),
('Gadget World Ltd', '9123456789', 'Mumbai', 'info@gadgetworld.com'),
('AudioMasters', '9988776655', 'Bangalore', 'support@audiomasters.com'),
('WearableTech', '9456781234', 'Chennai', 'sales@wearabletech.com'),
('TabletZone', '9345678123', 'Hyderabad', 'service@tabletzone.com'),
('Accessory Hub', '9162736450', 'Delhi', 'contact@accessoryhub.com'),
('Print Solutions', '9798675432', 'Chennai', 'info@printsolutions.com');

/_
select all products
_/
SELECT _ FROM products;
/_
select all products
_/
SELECT _ FROM suppliers;

/_Example 1: List All Products with Their Supplier Names
Display the names of all products along with their respective supplier names._/

SELECT p.product_name, s.supplier_name
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/_Example 2: List All Products Supplied by 'Tech Supplies Inc'
Display the names and prices of products supplied by 'Tech Supplies Inc'._/
SELECT p.product_name, p.unit_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_name = "Tech Supplies Inc";

/_Example 3: Find the Maximum Unit Price of Products Supplied by 'Tech Supplies Inc'
Identify the maximum unit price of products supplied by 'Tech Supplies Inc'._/
SELECT Max(p.unit_price)AS max_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_name = "Tech Supplies Inc";

/_ Exercises _/
/_Exercise 1: Show the Contact Numbers of Suppliers for Each Product
Retrieve the product names along with the contact numbers of their suppliers._/
SELECT p.product_name, s.contact_number
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/_Exercise 2: Display Supplier Locations for Each Product
List the products along with the locations of their suppliers._/
SELECT p.product_name, s.supplier_location
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/_Exercise 3: List All Products with Their Supplier IDs and Name
Display all products along with their corresponding supplier IDs and names._/
SELECT p.product_name, s.supplier_id, s.supplier_name
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/_Exercise 4: Find the Unit Price and Supplier Name for Each Product
Show the unit price of each product along with the supplier's name._/
SELECT p.product_name, p.unit_price, s.supplier_name
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id;

/_Exercise 5: Find Products Supplied by 'Gadget World Ltd' Located in a Specific Location
List all products supplied by 'Gadget World Ltd' where the supplier is located in 'Mumbai'._/
SELECT p.product_name, s.supplier_location
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_location = "Mumbai";

/_Exercise 6: Find Products Priced Under 200 from Suppliers in 'Bangalore'
List products priced under 200 from suppliers located in 'Bangalore'._/
SELECT p.product_name, p.unit_price, s.supplier_location
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_location = 'Bangalore';

/_Exercise 7: Display Products with Prices Above 250 and Their Supplier's Contact Number
List products with unit prices above 250 along with their supplier's contact number._/
SELECT p.product_name, p.unit_price, s.contact_number
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE p.unit_price > 250;

/_Exercise 8: Find Products Priced Below 300 from Suppliers Located in 'Chennai'
Retrieve products priced below 300 from suppliers located in 'Chennai'._/
SELECT p.product_name , p.unit_price
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_location = 'Chennai';

/_Exercise 9: Determine the Minimum Quantity in Stock for Products Supplied by 'Gadget World Ltd'
Find the minimum quantity in stock for products supplied by 'Gadget World Ltd'._/
SELECT MIN(p.quantity_in_stock)AS min_stock
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_name = 'Gadget World Ltd';

/_Exercise 10: Calculate the Total Number of Products in the 'Accessories' Category Supplied by 'MegaElectronics'
Compute the total number of products in the 'Accessories' category supplied by 'MegaElectronics'._/
SELECT COUNT(p.category)AS total_product
FROM products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
WHERE s.supplier_name = 'MegaElectronics';
