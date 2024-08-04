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

