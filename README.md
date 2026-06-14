# Completer-SQL-Database_smart_inventory_relational-database_creation_project.
Smart Inventory Management System is a Microsoft SQL Server database project designed to manage products, suppliers, customers, purchases, and sales. It uses normalized tables and foreign key relationships to ensure data integrity while supporting inventory tracking, reporting, and business analytics.
Completer SQL Relational database creation project.

Requirements
Download free SQL Server Management Studio 2022 from the link below.
https://learn.microsoft.com/en-us/ssms/install/install
  
From the above click on the blue download SSMS installer button, the SQL Server Management Studio 2022 installation kit will download to your computer default downloads folder.
Double click the installation kit described on the step above to start SQL installation process.
Upon successful completion, on your computer search bar, type SQL, a window will pop up with the SQL server icon shown below.
 
Click on the icon to open the connection interface like the one shown below.
 
Pick the server named localhost\SQLEXPRESS and the rest settings, however for production environment, its important an advanced method having username and password is applied (I shall demonstrate that in our next project)
On the above interface, click on the Connect button at the bottom.
The connection will take you to the interface like the one below.
 
To create the database, relational tables and constraints,  on the above interface, click on the new query icon/ menu   to open the interface like one below.
 
On the above interface, copy paste the ENTIRE code below into the window on the right pane.
And thereafter click on the execute icon  

-- =========================================
-- 1. CREATE DATABASE
-- =========================================
CREATE DATABASE smart_inventory;
USE smart_inventory;

-- =========================================
-- 2. ROOT TABLES (NO DEPENDENCIES)
-- =========================================

CREATE TABLE supplier_category (
    supplier_category_code INT PRIMARY KEY,
    supplier_category NVARCHAR (100)
);

CREATE TABLE region (
    region_code INT PRIMARY KEY,
    county NVARCHAR (100)
);

CREATE TABLE staff (
    staff_id INT PRIMARY KEY,
    staff_name NVARCHAR (100)
);

CREATE TABLE taxation (
    tax_code INT PRIMARY KEY,
    tax_rate DECIMAL(5,2)
);



-- =========================================
-- 3. DEPENDENT MASTER TABLES
-- =========================================

CREATE TABLE product_category (
    category_code INT PRIMARY KEY,
    category_name NVARCHAR (100),
    supplier_category_code INT,
    FOREIGN KEY (supplier_category_code)
        REFERENCES supplier_category(supplier_category_code)
);

CREATE TABLE customer (
    customer_code INT PRIMARY KEY,
    customer NVARCHAR (150),
    region_code INT,
    FOREIGN KEY (region_code)
        REFERENCES region(region_code)
);

CREATE TABLE supplier (
    supplier_code INT PRIMARY KEY,
    supplier NVARCHAR (150),
    region_code INT,
    supplier_category_code INT,
    FOREIGN KEY (region_code)
        REFERENCES region(region_code),
    FOREIGN KEY (supplier_category_code)
        REFERENCES supplier_category(supplier_category_code)
);

-- =========================================
-- 4. PRODUCT TABLE
-- =========================================

CREATE TABLE product (
    product_code INT PRIMARY KEY,
    product_name NVARCHAR (150),
    category_code VARCHAR (10),
    supplier_category_code INT,
    FOREIGN KEY (category_code)
        REFERENCES product_category(category_code),
    FOREIGN KEY (supplier_category_code)
        REFERENCES supplier_category(supplier_category_code)
);
-- =========================================
-- 5. TRANSACTION TABLES
-- =========================================

CREATE TABLE purchase (
    purchase_id INT IDENTITY (1,1) PRIMARY KEY,
    supplier_category_code VARCHAR (10),
    category_code VARCHAR (10),
    product_code VARCHAR (20),
    purchase_date DATETIME,
    quantity INT,
    unit_price DECIMAL (10,2),

    FOREIGN KEY (supplier_category_code)
        REFERENCES supplier_category(supplier_category_code),
    FOREIGN KEY (category_code)
        REFERENCES product_category(category_code),
    FOREIGN KEY (product_code)
        REFERENCES product(product_code)
);
CREATE TABLE sale (
    sale_id INT IDENTITY (1,1) PRIMARY KEY,
    staff_id INT,
    region_code INT,
    customer_code INT,
    supplier_category_code INT,
    category_code INT,
    product_code VARCHAR (20),
    sale_date DATETIME,
    quantity INT,
    unit_price DECIMAL (10,2),
    tax_code INT,
    FOREIGN KEY (staff_id)
        REFERENCES staff(staff_id),
    FOREIGN KEY (region_code)
        REFERENCES region(region_code),
    FOREIGN KEY (customer_code)
        REFERENCES customer(customer_code),
    FOREIGN KEY (supplier_category_code)
        REFERENCES supplier_category(supplier_category_code),
    FOREIGN KEY (category_code)
        REFERENCES product_category(category_code),
    FOREIGN KEY (product_code)
        REFERENCES product(product_code),
    FOREIGN KEY (tax_code)
        REFERENCES taxation(tax_code)
);
You get a successful completion message that you have created database named smart_ inventory
On the left hand panel click on the + at the left of the Database folder to expand it.
 

Locate your Database named  
Click on the + sign on the left side of the database and it expand it. For you to view all the tables click on the + sign on the left of the name Tables.  
It diplays all the tables in the Database as shown below
 
To install the same database in another computer without having to follow all the above steps, script the database by right clicking the database dynamic_inventory, select tasks, then select generate script as shown below.
 

From the above step, select a location within your computer where the scripted file will be stored.
 
The script for this project is included in the folder as script.sql file.
Safe the above file for future importation instead of following all the above steps.
Now you have a complete empty database.
In our next lesson I will demonstrated on how to insert data in to the tables, perform queries, views, stored procedures and conduct database management and administration tasks.
Powered by:

Peter Murungi
ggmurungi@gmail.com
