# product-database
Script to create a database for products on base of the following activity:

### Product Catalog Database Design Challenge

Background: As an IT Software Engineer, you have been tasked with designing a relational database for a product catalog. The database will support the storage of product information, including categorization and product variations (e.g., different colors or sizes). Your goal is to create an SQL script that can be used to create this database. The SQL script should be compatible with any relational database system. 

Scenario: You are provided with the following requirements and specifications for the database: 

Requirements: 
The database should support the storage of product information, including: 
Product name
Product description
Product price
Products should be categorized into different categories.
Each product can belong to one or more categories, and each category can have subcategories. Products can have variations. 

For example, a product may be available in different colors or sizes. Each variation should have its own price. 

Tasks: 
Design the SQL schema for the product catalog database based on the provided requirements and specifications. 
Your schema should include tables and relationships that represent the product catalog. 
Write an SQL script that creates the complete database structure, including tables, columns, and relationships. Ensure that your script is compatible with any relational database system (e.g., MySQL, PostgreSQL, SQL Server). 
Include sample data in your script to populate the database with at least a few products, categories, and product variations. 

Acceptance Criteria: 
The SQL script successfully creates the database structure without errors. 
The schema includes appropriate tables, columns, and relationships to represent the product catalog. 
Sample data is included to demonstrate how the database should be populated. 

Submission: Please provide the SQL script that creates the database structure and includes sample data. Ensure that your script is well-documented and organized. 
Note: You are free to choose any table names, column names, and data types that you believe are appropriate for this task. You may also include any additional features or optimizations that you think would enhance the database design. If you have any questions or need clarification on the requirements, please feel free to reach out for assistance.


-- Show structure
``DESC PROD_VARIATIONS;
DESC PROD_CATEGORIES;
DESC CAT_OPTIONS;
DESC CATEGORIES;
DESC SUB_OPTIONS;
DESC PROD_OPTIONS;
DESC SUBCATEGORIES;
DESC PRODUCTS;``


-- Drop all
``DROP TABLE PROD_VARIATIONS;
DROP TABLE PROD_CATEGORIES;
DROP TABLE CAT_OPTIONS;
DROP TABLE CATEGORIES;
DROP TABLE SUB_OPTIONS;
DROP TABLE PROD_OPTIONS;
DROP TABLE SUBCATEGORIES;
DROP TABLE PRODUCTS;``
