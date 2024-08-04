(i) Normal Forms of the Tables
  
  
  The analysis of the tables in the database ensures they adhere to the principles of normalization, specifically First Normal Form (1NF) and Second Normal Form     (2NF). Each table was evaluated based on the rules of 1NF and 2NF to ensure data integrity, eliminate redundancy, and optimize the database structure.

  

CUSTOMERS Table
  
  1NF: The CUSTOMERS table contains atomic values in each column, with each column containing values of a single type. The column names are unique, and the order       of rows does not affect data integrity.
  
  2NF: The table is in 2NF because all non-key attributes (first_name, last_name, email, phone_number, address) are fully functionally dependent on the primary key     (customer_id).



CATEGORIES Table
  
  1NF: The CATEGORIES table contains atomic values in each column, with each column containing values of a single type. The column names are unique, and the order     of rows does not affect data integrity.
  
  2NF: The table is in 2NF because the non-key attribute (category_name) is fully functionally dependent on the primary key (category_id).



PRODUCTS Table

1NF: The PRODUCTS table contains atomic values in each column, with each column containing values of a single type. The column names are unique, and the order of     rows does not affect data integrity.

2NF: The table is in 2NF because all non-key attributes (name, description, price, category_id) are fully functionally dependent on the primary key (product_id).



SIZES Table

  1NF: The SIZES table contains atomic values in each column, with each column containing values of a single type. The column names are unique, and the order of       rows does not affect data integrity.
  
  2NF: The table is in 2NF because the non-key attribute (size_name) is fully functionally dependent on the primary key (size_id).



PRODUCT_AVAILABILITY Table

  1NF: The PRODUCT_AVAILABILITY table contains atomic values in each column, with each column containing values of a single type. The column names are unique, and     the order of rows does not affect data integrity.
  
  2NF: The table is in 2NF because the non-key attribute (stock_quantity) is fully functionally dependent on the composite primary key (product_id, size_id).



ORDERS Table

  1NF: The ORDERS table contains atomic values in each column, with each column containing values of a single type. The column names are unique, and the order of       rows does not affect data integrity.
  
  2NF: The table is in 2NF because all non-key attributes (order_date, customer_id, product_id, size_id, quantity, price) are fully functionally dependent on the       primary key (order_id).



REVIEWS Table

  1NF: The REVIEWS table contains atomic values in each column, with each column containing values of a single type. The column names are unique, and the order of     rows does not affect data integrity.
  
  2NF: The table is in 2NF because all non-key attributes (product_id, customer_id, rating, comment, review_date) are fully functionally dependent on the primary       key (review_id).


(ii) Database & Entity - Relationship Diagram images attached in images subfolder

(iii) Stress Testing & Responses

  CRUD operations 

  1. `Customers` table


Create

Operation: Insert a new customer record.
SQL Command:INSERT INTO CUSTOMERS (customer_id, first_name, last_name, email, phone_number, address)
VALUES (1, 'Jack', 'Doe', 'jack.doe1@example.com', '1234543210', '321 Elm St.');
Result: The operation was successful with no errors


Retrieve

Operation: Retrieve the customer record with customer_id 1.
SQL Command: SELECT * FROM CUSTOMERS WHERE customer_id = 1;
Result: The customer record with customer_id 1 was retrieved successfully with no errors.

Update

Operation: Update the customer record with customer_id 1 to change the first name to "Jane", last name to "Doe", email to "jane.doe2@example.com", phone number to "1234567899", and address to "1234 Elm St."

SQL Command: 
UPDATE CUSTOMERS
SET first_name = 'Jane', last_name = 'Doe', email = 'jane.doe2@example.com', phone_number = '1234567899', address = '1234 Elm St.'
WHERE customer_id = 1;

Result: The operation was successful with no errors.


Delete

Operation: Delete the customer record with customer_id 1.

SQL Command:DELETE FROM CUSTOMERS WHERE customer_id = 1;
Result: The operation failed with the following error: Error Code: 1451. Cannot delete or update a parent row: a foreign key constraint fails (`online_clothing_store`.`orders`, CONSTRAINT `orders_ibfk_1` FOREIGN KEY (`customer_id`) REFERENCES `customers` (`customer_id`))


Solution: To delete the customer record, references to customer_id 1 in other tables (such as ORDERS and REVIEWS) must be deleted first.

Delete References in ORDERS Table DELETE FROM ORDERS WHERE customer_id = 1;

Delete References in REVIEWS Table: DELETE FROM REVIEWS WHERE customer_id = 1;

Retry Deletion in CUSTOMERS Table: DELETE FROM CUSTOMERS WHERE customer_id = 1;

The customer record was successfully deleted after removing references from other tables.



2. `CATEGORIES` Table

The following outlines the CRUD operations performed on the `CATEGORIES` table and the results of each operation.

1. Create
   - Operation: Insert a new category record.
   - SQL Command:
  
     INSERT INTO CATEGORIES (category_id, category_name)
     VALUES (12, 'Formalwear');
     
   - Result: The operation was successful with no errors.

2. Retrieve
   - Operation: Retrieve the category record with `category_id` 12.
   - SQL Command
     SELECT  FROM CATEGORIES WHERE category_id = 12;
   - Result: The category record with `category_id` 12 was retrieved successfully with no errors.   

3. Update
   - Operation: Update the category record with `category_id` 12 to change the category name to "Evening Wear".
   - SQL Command:

     UPDATE CATEGORIES
     SET category_name = 'Evening Wear'
     WHERE category_id = 12;

   - Result: The operation was successful with no errors.


4. Delete
   - Operation: Delete the category record with `category_id` 12.
   - SQL Command:
     
     DELETE FROM CATEGORIES WHERE category_id = 12;
     
   - Result: The operation failed with the following error:
     
     Error Code: 1451. Cannot delete or update a parent row: a foreign key constraint fails (`online_clothing_store`.`products`, CONSTRAINT `products_ibfk_1` FOREIGN KEY (`category_id`) REFERENCES `categories` (`category_id`))
     

   - Solution: To delete the category record, references to `category_id` 12 in the `PRODUCTS` table must be deleted first.
     - Delete References in `PRODUCTS` Table:
       
       DELETE FROM PRODUCTS WHERE category_id = 12;
       
     - Retry Deletion in `CATEGORIES` Table:
       
       DELETE FROM CATEGORIES WHERE category_id = 12;
       

   - Final Result: The category record was successfully deleted after removing references from the `PRODUCTS` table.

3. `ORDERS` Table


  1. Create
    Operation: Insert a new order record.
    SQL Command:
     INSERT INTO ORDERS (order_id, order_date, customer_id, product_id, size_id, quantity, price)
     VALUES (6, '20240706', 6, 6, 6, 1, 14.99);
     
    Result: The operation was successful with no errors.

  2. Retrieve
    Operation: Retrieve the order record with `order_id` 5.
    SQL Command:
  
     SELECT  FROM ORDERS WHERE order_id = 5;
     
    Result: The order record with `order_id` 5 was retrieved successfully with no errors.
     


  3. Update
    Operation: Update the order record with `order_id` 5 to change the quantity to 3 and price to 29.99.
    SQL Command:
   
     UPDATE ORDERS
     SET quantity = 3, price = 29.99
     WHERE order_id = 5;
     
    Result: The operation was successful with no errors.
     

  4. Delete
    Operation: Delete the order record with `order_id` 5.
    SQL Command:
    
     DELETE FROM ORDERS WHERE order_id = 5;
     
    Result: The operation was successful with no errors.

4. `PRODUCT_AVAILABILITY` Table


  1. Create
   - Operation: Insert a new product availability record.
   - SQL Command:
     INSERT INTO PRODUCT_AVAILABILITY (product_id, size_id, stock_quantity)
     VALUES (1, 1, 50);
     
   - Result: The operation was successful with no errors.

  2. Retrieve
   - Operation: Retrieve the product availability record with `product_id` 1 and `size_id` 1.
   - SQL Command:
     
     SELECT  FROM PRODUCT_AVAILABILITY WHERE product_id = 1 AND size_id = 1;
     
   - Result: The product availability record with `product_id` 1 and `size_id` 1 was retrieved successfully with no errors.
 

  3. Update
   - Operation: Update the product availability record with `product_id` 1 and `size_id` 1 to change the stock quantity to 100.
   - SQL Command:
     UPDATE PRODUCT_AVAILABILITY
     SET stock_quantity = 100
     WHERE product_id = 1 AND size_id = 1;
    
   - Result: The operation was successful with no errors.
 

  4. Delete
   - Operation: Delete the product availability record with `product_id` 1 and `size_id` 1.
   - SQL Command:
     
     DELETE FROM PRODUCT_AVAILABILITY WHERE product_id = 1 AND size_id = 1;
     
   - Result: The operation was successful with no errors.

5. `PRODUCTS` Table


  1. Create
   - Operation: Insert a new product record.
   - SQL Command:
     
     INSERT INTO PRODUCTS (product_id, name, description, price, category_id)
     VALUES (3, 'Hoodie', 'Warm and cozy hoodie.', 19.99, 3);
     
   - Result: The operation was successful with no errors.

  2. Retrieve
   - Operation: Retrieve the product record with product_id 3.
   - SQL Command:
     
     SELECT  FROM `PRODUCTS` WHERE product_id = 3;
     
   - Result: The product record with product_id 3 was retrieved successfully with no errors.
      

  3. Update
   - Operation: Update the product record with product_id 3 to change the price to 24.99 and description to "Cozy and stylish hoodie."
   - SQL Command:
     
     UPDATE `PRODUCTS`
     SET price = 24.99, description = 'Cozy and stylish hoodie.'
     WHERE product_id = 3;
     
   - Result: The operation was successful with no errors.
     

  4. Delete
   - Operation: Delete the product record with product_id 3.
   - SQL Command:
     
     DELETE FROM `PRODUCTS` WHERE product_id = 3;
     
   - Result: The operation failed with the following error:
     
     Error Code: 1451. Cannot delete or update a parent row: a foreign key constraint fails (online_clothing_store.reviews, product_availability, orders, CONSTRAINT reviews_ibfk_1, product_availability_ibfk_1, orders_ibfk_1 FOREIGN KEY (product_id) REFERENCES products (product_id))
     

   - Solution: To delete the product record, references to product_id 3 in the `REVIEWS`, `PRODUCT_AVAILABILITY`, and `ORDERS` tables must be deleted first.
     - Delete References in REVIEWS Table:
       
       DELETE FROM REVIEWS WHERE product_id = 3;
       
     - Delete References in `PRODUCT_AVAILABILITY` Table:
       
       DELETE FROM PRODUCT_AVAILABILITY WHERE product_id = 3;
       
     - Delete References in `ORDERS` Table:
       
       DELETE FROM ORDERS WHERE product_id = 3;
       
     - Retry Deletion in `PRODUCTS` Table:
       
       DELETE FROM PRODUCTS WHERE product_id = 3;
       

   - Final Result: The product record was successfully deleted after removing references from the REVIEWS, PRODUCT_AVAILABILITY, and ORDERS tables.

6. `REVIEWS` Table


1. Create
   - Operation: Insert a new review record.
   - SQL Command:
     
     INSERT INTO REVIEWS (review_id, product_id, customer_id, rating, comment, review_date)
     VALUES (5, 5, 5, 4, 'Good value for money.', '2024-07-05');
     
   - Result: The operation was successful with no errors.

2. Retrieve
   - Operation: Retrieve the review record with `review_id` 5.
   - SQL Command:
     
     SELECT  FROM REVIEWS WHERE review_id = 5;
     
   - Result: The review record with `review_id` 5 was retrieved successfully with no errors.
     


3. Update
   - Operation: Update the review record with `review_id` 5 to change the rating to 5 and comment to "Excellent value for money."
   - SQL Command:
     
     UPDATE REVIEWS
     SET rating = 5, comment = 'Excellent value for money.'
     WHERE review_id = 5;
     
   - Result: The operation was successful with no errors.
     
   

4. Delete
   - Operation: Delete the review record with `review_id` 5.
   - SQL Command:
     
     DELETE FROM REVIEWS WHERE review_id = 5;
     
   - Result: The operation failed with the following error:
     
     Error Code: 1451. Cannot delete or update a parent row: a foreign key constraint fails (`online_clothing_store`.`reviews`, CONSTRAINT `reviews_ibfk_1` FOREIGN KEY (`product_id`) REFERENCES `products` (`product_id`), CONSTRAINT `reviews_ibfk_2` FOREIGN KEY (`customer_id`) REFERENCES `customers` (`customer_id`))
     

   - Solution: To delete the review record, references to `product_id` 5 and `customer_id` 5 in the `REVIEWS` table must be removed first.
     - Delete References in the `REVIEWS` Table:
       
       DELETE FROM REVIEWS WHERE review_id = 5;
       
     - Delete References in the `ORDERS` Table:
       
       DELETE FROM ORDERS WHERE product_id = 5 AND customer_id = 5;
       

     - Delete References in the `PRODUCTS` Table:
       
       DELETE FROM PRODUCTS WHERE product_id = 5;
       
     - Delete References in the `CUSTOMERS` Table:
       
       DELETE FROM CUSTOMERS WHERE customer_id = 5;
       

     - Retry Deletion in `REVIEWS` Table:
       
       DELETE FROM REVIEWS WHERE review_id = 5;
       

   - Final Result: The review record was successfully deleted after removing references from the `REVIEWS`, `ORDERS`, `PRODUCTS`, and `CUSTOMERS` tables.

7. `SIZES` Table

1. Create
   - Operation: Insert a new size record.
   - SQL Command:
     
     INSERT INTO SIZES (size_id, size_name)
     VALUES (3, 'M');
     
   - Result: The operation was successful with no errors.

2. Retrieve
   - Operation: Retrieve the size record with `size_id` 3.
   - SQL Command:
     
     SELECT  FROM SIZES WHERE size_id = 3;
     
   - Result: The size record with `size_id` 3 was retrieved successfully with no errors.
   


  3. Update
   - Operation: Update the size record with `size_id` 3 to change the size name to "Medium".
   - SQL Command:
     
     UPDATE SIZES
     SET size_name = 'Medium'
     WHERE size_id = 3;
     
   - Result: The operation was successful with no errors.
   
   

  4. Delete
   - Operation: Delete the size record with `size_id` 3.
   - SQL Command:
     
     DELETE FROM SIZES WHERE size_id = 3;
     
   - Result: The operation failed with the following error:
     
     Error Code: 1451. Cannot delete or update a parent row: a foreign key constraint fails (`online_clothing_store`.`product_availability`, CONSTRAINT `product_availability_ibfk_2` FOREIGN KEY (`size_id`) REFERENCES `sizes` (`size_id`))
     

   - Solution: To delete the size record, references to `size_id` 3 in the `PRODUCT_AVAILABILITY` and `ORDERS` tables must be deleted first.
     - Delete References in `PRODUCT_AVAILABILITY` Table:
       
       DELETE FROM PRODUCT_AVAILABILITY WHERE size_id = 3;
       
     - Delete References in `ORDERS` Table:
       
       DELETE FROM ORDERS WHERE size_id = 3;
       
     - Retry Deletion in `SIZES` Table:
       
       DELETE FROM SIZES WHERE size_id = 3;
       

   - Final Result: The size record was successfully deleted after removing references from the `PRODUCT_AVAILABILITY` and `ORDERS` tables.

 
