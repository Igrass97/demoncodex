Data Definition Language sentences are used to create and modify the structure of the tables and the objects of the database.

- **CREATE**: create objects in the database.
- **ALTER**: modify the structure of the database.
- **DROP**: deletes objects from the database.
- **TRUNCATE**: deletes all records in the database, keeping the structure.
- **COMMENT**: leaves a comment in tables and columns.

## Practical Example: Client, Invoice, Product, Invoice Detail (Oracle)

### Table Creation (CREATE)
``` SQL
CREATE TABLE product (product_code VARCHAR2(8) NOT NULL, name VARCHAR2(30) NOT NULL, price NUMBER(8,3));

CREATE TABLE client (client_code VARCHAR2(8) NOT NULL, first_name VARCHAR2(30) NOT NULL);

CREATE TABLE invoice (branch NUMBER(2), invoice_code NUMBER(2), invoice_date TIMESTAMP, payment_method VARCHAR2(3), client_code VARCHAR2(8), total_amount NUMBER(14,2));

CREATE TABLE invoice_detail (branch NUMBER(2), invoice_code NUMBER(2), product_code VARCHAR2(8), quantity NUMBER(8,3) NOT NULL, price NUMBER(8,3), subtotal NUMBER(9,3));
```

### View Creation (CREATE)
``` SQL
CREATE VIEW v_invoice_client01 AS 
SELECT invoice_code, invoice_date, total_amount 
FROM invoice 
WHERE client_code = 'A01’
```

### Index Creation (CREATE)
``` SQL
CREATE INDEX invoice_date_idx ON invoice(invoice_date);
```

### Create User (CREATE)

``` SQL
CREATE USER username IDENTIFIED BY userpassword;
```

### Create Role (CREATE)
``` SQL
CREATE ROLE my_role;
```

### Grant Create Session and Select (GRANT)
Allows the user to connect to the database

``` SQL
GRANT CREATE_SESSION TO username;
GRANT SELECT ANY TABLE TO username;
```

### Grant Privileges to Role/User (GRANT)
The privileges are: **SELECT**, **ALTER**, **DROP**, **DELETE**, **REFERENCE**, **INDEX** and **ALL**
``` SQL
GRANT SELECT ON product TO <my_role | user>;
```

### Grant Role to User (GRANT)
``` SQL
GRANT my_role TO username;
```

### Revoke Role (REVOKE)
``` SQL
REVOKE my_role FROM username;
```

### Revoke Privilege to Role/User
``` SQL
REVOKE SELECT ON product FROM username;
```
---
### Altering the Tables (ALTER)
``` SQL
ALTER TABLE Client ADD last_name VARCHAR2(30));
```

**NOTE:** ALTER TABLE can be used with: **ADD**, **MODIFY** and **DROP**.

### Add Primary Key (ALTER / CREATE)
**After the table is created**
``` SQL
ALTER TABLE Product ADD CONSTRAINT product_pk PRIMARY KEY (product_code));
ALTER TABLE Client ADD CONSTRAINT client_pk PRIMARY KEY (client_code));
ALTER TABLE Invoice ADD CONSTRAINT invoice_pk PRIMARY KEY (invoice_code));
```

**Before the table is created**
``` SQL
CREATE TABLE Product (product_code VARCHAR2(8) PRIMARY KEY, name VARCHAR2(30), price NUMBER(8,3));
```

``` SQL
CREATE TABLE Product (product_code VARCHAR2(8), name VARCHAR2(30), price NUMBER(8,3), CONSTRAINT articulos_pk PRIMARY KEY (codigo_del_articulo));
```

### Add Foreign Keys (ALTER)
``` SQL
ALTER TABLE Invoice ADD CONSTRAINT invoice_fk FOREIGN KEY (client_code) REFERENCES Client(client_code); 

ALTER TABLE InvoiceDetail ADD CONSTRAINT product_fk FOREIGN KEY (product_code) REFERENCES Product(product_code); 

ALTER TABLE InvoiceDetail ADD CONSTRAINT invoice_fk FOREIGN KEY (invoice_code) REFERENCES Invoice(invoice_code);
```

### Add Check Constraint (ALTER)
``` SQL
ALTER TABLE Product ADD CONSTRAINT price_ck CHECK (price > 0);
```
