# Data Catalog for Gold Layer

## Overview
The Gold Layer represents the finalized, business-ready data model designed for reporting and analytical use. It is organized using a star schema and includes both **dimension tables** and **fact tables** for specific business metrics.

---

### 1. **gold.dim_customers**
- **Purpose:** Contains customer records enhanced with demographic and location-related attributes to support customer-level analysis.
- **Columns:**

| Column Name      | Data Type     | Description                                                                                   |
|------------------|---------------|-----------------------------------------------------------------------------------------------|
| customer_key     | INT           | A surrogate key that uniquely identifies each customer within the dimension table.              |
| customer_id      | INT           | A unique numeric identifier assigned to each customer.                                       |
| customer_number  | NVARCHAR(50)  | An alphanumeric customer reference used for identification and tracking.        |
| first_name       | NVARCHAR(50)  | The customer’s given name as stored in the system.                                       |
| last_name        | NVARCHAR(50)  | The customer’s family or surname.                                                     |
| country          | NVARCHAR(50)  | The country where the customer resides (e.g., 'Australia').                             |
| marital_status   | NVARCHAR(50)  | The marital status of the customer (e.g., 'Married', 'Single').                              |
| gender           | NVARCHAR(50)  | The gender of the customer (e.g., 'Male', 'Female', 'n/a').                                  |
| birthdate        | DATE          | The date of birth of the customer, formatted as YYYY-MM-DD (e.g., 1970-08-01).               |
| create_date      | DATE          | The date and time when the customer record was created in the system|

---

### 2. **gold.dim_products**
- **Purpose:** Stores product-related details and attributes used for product analysis and categorization.
- **Columns:**

| Column Name         | Data Type     | Description                                                                                   |
|---------------------|---------------|-----------------------------------------------------------------------------------------------|
| product_key         | INT           | Surrogate key uniquely identifying each product record in the product dimension table.         |
| product_id          | INT           | A unique internal identifier used to track the product.          |
| product_number      | NVARCHAR(50)  | A structured alphanumeric code representing the product, often used for categorization or inventory. |
| product_name        | NVARCHAR(50)  | Descriptive name of the product, including key details such as type, color, and size.         |
| category_id         | NVARCHAR(50)  | A unique identifier representing the product’s category.    |
| category            | NVARCHAR(50)  | The broader classification of the product (e.g., Bikes, Components) to group related items.  |
| subcategory         | NVARCHAR(50)  | A more detailed classification of the product within the category, such as product type.      |
| maintenance_required| NVARCHAR(50)  | Indicates whether the product requires maintenance (e.g., 'Yes', 'No').                       |
| cost                | INT           | The base or manufacturing cost of the product in monetary units.                            |
| product_line        | NVARCHAR(50)  | The specific product line or series (e.g., Road, Mountain).      |
| start_date          | DATE          | The date the product became available for sale or use.|

---

### 3. **gold.fact_sales**
- **Purpose:** Captures detailed sales transactions to enable revenue, quantity, and performance analysis.
- **Columns:**

| Column Name     | Data Type     | Description                                                                                   |
|-----------------|---------------|-----------------------------------------------------------------------------------------------|
| order_number    | NVARCHAR(50)  | A unique alphanumeric identifier for each sales order (e.g., 'SO54496').                      |
| product_key     | INT           | A foreign key linking the sale to the product dimension.                             |
| customer_key    | INT           | A foreign key linking the sale to the customer dimension.                             |
| order_date      | DATE          | The date the sales order was created.                                                          |
| shipping_date   | DATE          | The date the order was shipped to the customer.                                          |
| due_date        | DATE          | The date by which payment for the order is due.                                                      |
| sales_amount    | INT           | The total value of the sale for the transaction line.   |
| quantity        | INT           | The number of product units sold in the transaction. (e.g., 1).                       |
| price           | INT           | The unit price of the product for the sales line item. (e.g., 25).      |
