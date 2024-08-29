
# Supply Chain Management (SCM) Database Design and Normalization

## Overview

Supply Chain Management (SCM) involves the coordination and management of the flow of goods, services, and information from suppliers to customers. This document discusses the design of a relational database for SCM, focusing on key components such as entities, attributes, relationships, and normalization into the Third Normal Form (3NF).

## Database Design

### Entities and Attributes

1. **Product Category**
   - `Category_id` (Primary Key)
   - `Category_name` (e.g., furniture, clothing, electronics)

2. **Inventory**
   - `Product_Id` (Primary Key): Unique identifier for each product.
   - `Product_name`: Name of each product.
   - `Category_id` (Foreign Key)
   - `Stock_level`: Quantity of product left in the inventory.

3. **Supplier**
   - `Supplier_id` (Primary Key)
   - `Supplier_name`
   - `Supplier_contact`
   - `Supplier_location`
   - `Category_id` (Foreign Key)
   - `Product_id` (Foreign Key)

4. **Order Details**
   - `Order_id` (Primary Key)
   - `Order_date`
   - `Order_status`
   - `Order_value`
   - `Customer_id` (Foreign Key)
   - `Product_id` (Foreign Key)

5. **Customer**
   - `Customer_id` (Primary Key)
   - `Customer_name`
   - `Loyalty_status`
   - `Email`
   - `Customer_address`

6. **Shipment**
   - `Shipment_id` (Primary Key)
   - `Order_id` (Foreign Key)
   - `Shipment_date`
   - `Shipment_status` (Received, Not Received)
   - `Delivery_date`
   - `Product_weight`
   - `Shipped_qty`
   - `Product_id` (Foreign Key)

### Normalization to 3NF

#### 1. No Transitive Dependencies
In 3NF, there should be no transitive dependencies, meaning non-key attributes should not depend on other non-key attributes.

#### 2. Functional Dependency on the Primary Key
Each non-key attribute in a table should be functionally dependent on the entire primary key.

### Entity Descriptions and 3NF Compliance

1. **Product Category**
   - `Category_id` is the primary key.
   - `Category_name` depends on `Category_id`.
   - No transitive dependencies.

2. **Inventory**
   - `Product_id` is the primary key.
   - `Product_name` and `Stock_level` depend only on `Product_id`.
   - No transitive dependencies.

3. **Supplier**
   - `Supplier_id` is the primary key.
   - `Supplier_name`, `Supplier_contact`, and `Supplier_location` depend only on `Supplier_id`.
   - No transitive dependencies.

4. **Order Details**
   - `Order_id` is the primary key.
   - `Order_value`, `Order_date`, and `Order_status` depend only on `Order_id`.
   - No transitive dependencies.

5. **Customer**
   - `Customer_id` is the primary key.
   - `Customer_name`, `Email`, `Customer_address`, and `Loyalty_status` depend only on `Customer_id`.
   - No transitive dependencies.

6. **Shipment**
   - `Shipment_id` is the primary key.
   - `Shipment_date` depends only on `Shipment_id`.
   - `Order_id` is a foreign key and depends on `Shipment_id`.
   - No transitive dependencies.

### Entity-Relationship (ER) Diagram and Relationships

1. **Product and Supplier**: 
   - One-to-Many: A product can be supplied by one supplier, but a supplier can supply multiple products.
   - Relationship established through `Supplier_id` as a foreign key in the `Product` table.

2. **Product and Product Details**:
   - One-to-Many: Each product can have multiple instances in an order with specific details.
   - Relationship represented through `Category_id` as a foreign key in the `Inventory` table.

3. **Order and Customer**:
   - One-to-Many: Each order is placed by one customer, but a customer can place multiple orders.
   - Relationship established through `Customer_id` as a foreign key in the `Order` table.

4. **Order and Shipment**:
   - One-to-One: Each order can have one corresponding shipment, and each shipment is associated with one order.
   - Relationship established through `Order_id` as a foreign key in the `Shipment` table.

### Implementation

#### Database Creation

The following T-SQL statements were used to create the database and tables:

```sql
-- Create a database
CREATE DATABASE SUPPLY_CHAIN_MGT;

-- Create a table named ProductCategory
CREATE TABLE ProductCategory (
    category_id INT IDENTITY PRIMARY KEY,
    category_name VARCHAR(50)
);

-- Create a table named Inventory
CREATE TABLE Inventory (
    product_id INT IDENTITY PRIMARY KEY,
    product_name VARCHAR(50),
    stock_level INT,
    category_id INT REFERENCES ProductCategory(category_id)
);

-- Create a table named Supplier
CREATE TABLE Supplier (
    supplier_id INT IDENTITY PRIMARY KEY,
    supplier_name VARCHAR(50), 
    supplier_contact VARCHAR(50),
    location VARCHAR(50),
    category_id INT REFERENCES ProductCategory(category_id),
    product_id INT REFERENCES Inventory(product_id)
);

-- Create a table named Customer
CREATE TABLE Customer (
    customer_id INT IDENTITY(101,1) PRIMARY KEY,
    customer_name VARCHAR(50),
    loyalty_status VARCHAR(50),
    Email VARCHAR(50),
    customer_address VARCHAR(250)
);

-- Create a table named OrderDetails
CREATE TABLE OrderDetails (
    order_id INT IDENTITY(201,1) PRIMARY KEY, 
    order_date DATE,
    order_status VARCHAR(50),
    order_value DECIMAL(10,2),
    product_id INT REFERENCES Inventory(product_id),
    customer_id INT REFERENCES Customer(customer_id)
);

-- Create a table named Shipment
CREATE TABLE Shipment (
    shipment_id INT IDENTITY(501,1) PRIMARY KEY,
    shipment_date DATE, 
    shipment_status VARCHAR(50),
    delivery_date DATE,
    product_weight DECIMAL(10,2),
    shipped_qty INT,
    product_id INT REFERENCES Inventory(product_id),
    order_id INT REFERENCES OrderDetails(order_id)
);
```

#### Data Population

```sql
-- Populate ProductCategory table
INSERT INTO ProductCategory(category_name) VALUES
    ('Clothings'),
    ('Electronics'),
    ('Furniture');

-- Populate Inventory table
INSERT INTO Inventory (product_name, Category_id, stock_level) VALUES
    ('Chair', 3, 100),
    ('Table', 3, 80),
    ('T-shirt', 1, 200),
    ('Laptop', 2, 10),
    ('Mobile Phone', 2, 15);

-- Populate Supplier table
INSERT INTO Supplier(supplier_name, supplier_contact, location, category_id) VALUES 
    ('Furniture Emporium', '123-456-7890', 'North America', 3),
    ('Table Master', '456-789-0123', 'Europe', 3);

-- Populate Customer table
INSERT INTO Customer (Customer_name, Loyalty_status, Email, Customer_address) VALUES
    ('Sophia Wilson', 'Gold', 'sophia.wilson@example.com', '456 Oak St, Anytown, UK'),
    ('William Johnson', 'Silver', 'william.johnson@example.com', '789 Cedar St, Othertown, Canada');

-- Populate OrderDetails table
INSERT INTO OrderDetails (order_date, order_status, order_value, product_id, customer_id) VALUES
    ('2023-11-20', 'complete', 500, 1, 101),
    ('2023-05-10', 'incomplete', 400, 2, 102);

-- Populate Shipment table
INSERT INTO Shipment (order_id, shipment_date, shipment_status, delivery_date, product_weight, shipped_qty, product_id) VALUES
    (201, '2024-01-07', 'Received', '2024-01-10', 50.5, 10, 1),
    (202, '2024-02-12', 'Received', '2024-02-15', 1059.2, 120, 2);
```

## Conclusion

The Supply Chain Management database is designed to efficiently manage inventory, procurement, and logistics processes. The database is normalized to 3NF, ensuring data integrity, eliminating redundancy, and supporting accurate and efficient tracking of products, orders, and shipments. The relationships between entities are carefully modeled to reflect real-world supply chain operations.
