# 🗂️ SQL Relational Database Management Project


This project demonstrates the design and implementation of a **Customer Database Management System** using Oracle Live SQL. It includes both **Data Definition Language (DDL)** and **Data Manipulation Language (DML)** commands to define tables, enforce integrity constraints, and manage data efficiently.

---

## 🔗 View on Oracle Live SQL  
[Click here to open in Oracle Live SQL](https://livesql.oracle.com/ords/livesql/s/c4ii254ipfpoql82fvtc4q4rh)

---

## 📘 Project Overview  
This relational database stores and manages customer, address, and order information, demonstrating concepts like normalization, referential integrity, and data manipulation through SQL.

The database was designed in **3rd Normal Form (3NF)** to minimize redundancy and improve data integrity.

---

## 🧱 Database Structure  
### **1. Customers Table**
| Column | Description | Constraint |
|--------|--------------|-------------|
| `customer_id` | Unique customer identifier | Primary Key |
| `last_name` | Customer's last name | NOT NULL |
| `first_name` | Customer's first name | NOT NULL |
| `email_address` | Customer email | UNIQUE |
| `first_seen_date` | First date seen | NOT NULL |

### **2. Addresses Table**
| Column | Description | Constraint |
|--------|--------------|-------------|
| `address_id` | Unique address identifier | Primary Key |
| `customer_id` | Linked customer | Foreign Key (references Customers) |
| `address_street1` / `2` | Street address |  |
| `city`, `state`, `zip` | Location details |  |
| `address_last_modified_date` | Auto-updated date | DEFAULT SYSDATE NOT NULL |

### **3. Orders Table**
| Column | Description | Constraint |
|--------|--------------|-------------|
| `order_number` | Unique order ID | Primary Key |
| `customer_id` | Customer reference | Foreign Key |
| `product_name` | Product purchased | NOT NULL |
| `sell_date` / `ship_date` | Dates of sale and shipment | CHECK (sell_date <= ship_date) |

---

## ⚙️ SQL Concepts Used  
- `CREATE TABLE` with `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, and `NOT NULL` constraints  
- `ALTER TABLE` with `CHECK` constraint  
- `INSERT`, `UPDATE`, and `COMMIT` statements  
- Normalization to **3NF**

---

## 💾 Entity Relationship (ER) Diagram  
Below is the conceptual ER Model based on normalization to 3NF:

**Entities:**
- **Customers**
  - PK: customer_id  
  - Attributes: last_name, first_name, suffix, phone_number, email_address, first_seen_date  
- **Addresses**
  - PK: address_id  
  - FK: customer_id  
  - Attributes: address_street1, address_street2, city, state, zip, last_modified_date  
- **Orders**
  - PK: order_number  
  - FK: customer_id  
  - Attributes: product_name, list_price, sell_price, sell_date, ship_date  

📎 *ER Diagram and schema were developed based on the database normalization process in Assignment 5.*  

*(You can upload your ER diagram image or PDF here for reference. If it’s your “Assignment_5_Reem_Meisner.pdf,” rename it to something like `ER_Diagram.pdf` and link it like this:)*  
[View ER Diagram (PDF)](

---

## 💻 SQL Code  
Below is an example portion of the SQL used in this project:

```sql
CREATE TABLE Customers (
    customer_id NUMBER(10),
    last_name VARCHAR2(50) NOT NULL,
    first_name VARCHAR2(50) NOT NULL,
    email_address VARCHAR2(100),
    first_seen_date DATE NOT NULL,
    CONSTRAINT customers_pk PRIMARY KEY (customer_id),
    CONSTRAINT customers_email_uk UNIQUE (email_address)
);
