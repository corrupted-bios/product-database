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
```
DESC PROD_VARIATIONS;
DESC PROD_CATEGORIES;
DESC CAT_OPTIONS;
DESC CATEGORIES;
DESC SUB_OPTIONS;
DESC PROD_OPTIONS;
DESC SUBCATEGORIES;
DESC PRODUCTS;
```

-- Drop all
```
DROP TABLE PROD_VARIATIONS;
DROP TABLE PROD_CATEGORIES;
DROP TABLE CAT_OPTIONS;
DROP TABLE CATEGORIES;
DROP TABLE SUB_OPTIONS;
DROP TABLE PROD_OPTIONS;
DROP TABLE SUBCATEGORIES;
DROP TABLE PRODUCTS;
```

-- Exibir todos produtos e suas categorias:
SELECT TITLE, CATEGORIES.DESCRIPTION, SUBCATEGORIES.DESCRIPTION FROM PRODUCTS, PROD_CATEGORIES
JOIN CATEGORIES
ON CATEGORIES.CATEGORY_ID = PROD_CATEGORIES.CATEGORY_ID
JOIN SUBCATEGORIES
ON SUBCATEGORIES.SUBCATEGORY_ID = CATEGORIES.SUBCATEGORY_ID
WHERE PROD_CATEGORIES.PRODUCT_ID = PRODUCTS.PRODUCT_ID
ORDER BY TITLE;

-- Exibir todos produtos, seus atributos e seus preços:
SELECT 
PROD.TITLE, PROP.OPTION_NAME, PROP.OPTION_VALUE, PRVA.PRICE 
FROM 
PRODUCTS PROD, PROD_OPTIONS PROP, PROD_VARIATIONS PRVA
WHERE PROD.PRODUCT_ID = PRVA.PRODUCT_ID
AND PROP.PROD_OPTION_ID = PRVA.PROD_OPTION_ID
ORDER BY 1, 2, 4;

-- Exibir produtos dentro de uma faixa de preço dentro de uma categoria:
SELECT 
PROD.TITLE, PROP.OPTION_NAME, PROP.OPTION_VALUE, PRVA.PRICE 
FROM 
PRODUCTS PROD, PROD_OPTIONS PROP, PROD_VARIATIONS PRVA
WHERE PROD.PRODUCT_ID = PRVA.PRODUCT_ID
AND PROP.PROD_OPTION_ID = PRVA.PROD_OPTION_ID
AND PRVA.PRICE > 700
AND PROD.PRODUCT_ID = (
SELECT PRCA.PRODUCT_ID FROM PROD_CATEGORIES PRCA WHERE
PRCA.CATEGORY_ID = 12)
ORDER BY 1, 2, 4;

-- Exibir um produto e seu preço com base nos atributos escolhidos:
SELECT 
PROD.TITLE, PROP.OPTION_NAME, PROP.OPTION_VALUE, PRVA.PRICE 
FROM 
PRODUCTS PROD, PROD_OPTIONS PROP, PROD_VARIATIONS PRVA
WHERE PROD.PRODUCT_ID = PRVA.PRODUCT_ID
AND PROD.PRODUCT_ID = 4
AND PROP.PROD_OPTION_ID = PRVA.PROD_OPTION_ID
AND PROP.PROD_OPTION_ID IN (
SELECT PROD_OPTION_ID FROM PROD_OPTIONS WHERE
OPTION_NAME = 'Color' AND OPTION_VALUE = 'Black')
ORDER BY 1, 2, 4;

-- Pesquisar todos os produtos de uma categoria:
SELECT 
PROD.TITLE, PROP.OPTION_NAME, PROP.OPTION_VALUE, PRVA.PRICE 
FROM 
PRODUCTS PROD, PROD_OPTIONS PROP, PROD_VARIATIONS PRVA
WHERE PROD.PRODUCT_ID = PRVA.PRODUCT_ID
AND PROP.PROD_OPTION_ID = PRVA.PROD_OPTION_ID
AND PROD.PRODUCT_ID = (
SELECT PRCA.PRODUCT_ID FROM PROD_CATEGORIES PRCA WHERE
PRCA.CATEGORY_ID = 12)
ORDER BY 1, 2, 4;

-- Exibir quais atributos tem em uma especifica categoria:
SELECT CATE.DESCRIPTION, PROP.OPTION_NAME, PROP.OPTION_VALUE 
FROM PROD_OPTIONS PROP, CAT_OPTIONS CAOP, CATEGORIES CATE
WHERE PROP.PROD_OPTION_ID = CAOP.PROD_OPTION_ID
AND CATE.CATEGORY_ID = CAOP.CATEGORY_ID;

-- Lista de categorias e subcategorias
SELECT CATEGORIES.DESCRIPTION, SUBCATEGORIES.DESCRIPTION 
FROM CATEGORIES, SUBCATEGORIES
WHERE CATEGORIES.SUBCATEGORY_ID = SUBCATEGORIES.SUBCATEGORY_ID
ORDER BY 1, 2;
