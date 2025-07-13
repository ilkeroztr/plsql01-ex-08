# Oracle PL/SQL: Create & Execute a Stored Procedure (EX-08)

This guide demonstrates how to create a stored procedure in Oracle 21c XE and use it to insert a record into a table.  
It was implemented on a VM using Docker.

---

##  Objective

- Create a `CUSTOMER` table
- Write a stored procedure named `insert_customer`
- Insert a record using this procedure
- Display the result with a SELECT query

---

##  Technologies Used

- Oracle Database 21c XE
- PL/SQL
- Docker
- Linux VM (Debian)

---

##  Step-by-Step Instructions

### 1. Connect to the Oracle Container

```bash
sudo docker exec -it oraclexe bash
sqlplus testuser/testpass@//localhost:1521/XEPDB1
```

### 2. Create the CUSTOMER Table
```sql
CREATE TABLE CUSTOMER (
  ID NUMBER GENERATED ALWAYS AS IDENTITY,
  FIRST_NAME VARCHAR2(50),
  LAST_NAME VARCHAR2(50),
  AGE NUMBER
);
```
### 3. Create the Stored Procedure
```sql
CREATE OR REPLACE PROCEDURE insert_customer (
  p_first_name IN VARCHAR2,
  p_last_name IN VARCHAR2,
  p_age IN NUMBER
)
IS
BEGIN
  INSERT INTO CUSTOMER (FIRST_NAME, LAST_NAME, AGE)
  VALUES (p_first_name, p_last_name, p_age);
  COMMIT;
END;
```
 If successful, you’ll see:
 ```
Procedure created.
```

### 4. Execute the Procedure
```sql
EXEC insert_customer('Bruce', 'Wayne', 35);
```

### 5. Check the Table
```sql
SELECT * FROM CUSTOMER;
```

 Expected Output:
 ```
 ID  FIRST_NAME  LAST_NAME  AGE
--  ----------  ---------  ---
1   Bruce       Wayne      35
```
