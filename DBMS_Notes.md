Here are your **SQL Notes** for basic database and table operations:

---

## **Basic SQL Database & Table Commands**

### **1. Show All Databases**
```sql
SHOW DATABASES;
```
- Lists all available databases in the system.

### **2. Check Current Database**
```sql
SELECT DATABASE();
```
- Displays the currently selected database.

### **3. Select a Database**
```sql
USE mysql;
```
- Switches to the `mysql` database (or any other specified database).

### **4. Show Tables in the Selected Database**
```sql
SHOW TABLES;
```
- Lists all tables present in the currently selected database.

---

## **Creating a Database and Viewing Tables**
### **5. Create a New Database**
```sql
CREATE DATABASE vita_2025;
```
- Creates a new database named `vita_2025`.

### **6. Verify Tables in a Database**
```sql
SHOW TABLES;
```
- Displays all tables in the selected database.

---

## **Creating a Table**
### **7. Create a New Table**
```sql
CREATE TABLE test (
    id INT, 
    name VARCHAR(10)
);
```
- Creates a table named `test` with:
  - `id` column (integer type)
  - `name` column (string with max 10 characters)

### **8. View Table Structure**
```sql
DESC test;
```
or  
```sql
SHOW COLUMNS FROM test;
```
- Displays the **structure** of the `test` table, showing:
  - Column names
  - Data types
  - Nullability
  - Keys (Primary, Foreign)
  - Default values

---

### **1. Single Value Insert**
```sql
INSERT INTO test(id, name) VALUES (1, 'a');
```
- This inserts **one row** into the `test` table.
- It explicitly specifies the **columns (`id`, `name`)** and their corresponding **values (`1`, `'a'`)**.

---

### **2. Multi-Value Insert**
```sql
INSERT INTO test(id, name) VALUES (1, 'a'), (3, 'c'), (2, 'd');
```
- This inserts **multiple rows** in a **single query**.
- It improves performance compared to inserting rows one by one.

---

### **3. Insert Without Column Specification**
```sql
INSERT INTO test VALUES (5, 'e');
```
- This inserts a row **without explicitly mentioning column names**.
- It assumes that values are provided **for all columns in the table** in the correct order.

**⚠️ Important:**  
- This works only if you **provide values for every column** in the table.
- If the table has additional columns (e.g., `age` or `email`), this statement will fail **unless those columns have default values or allow NULL**.

---

### **4. Insert Only One Column**
```sql
INSERT INTO test(name) VALUES ('f');
```
- This inserts **only one column (`name`)**.
- The `id` column is **not specified**, so:
  - If `id` is **AUTO_INCREMENT**, it will automatically generate a value.
  - If `id` allows `NULL`, it will insert `NULL` (which may cause an issue if `id` is a `PRIMARY KEY` and doesn't allow `NULL`).
  - If `id` has a **DEFAULT value**, that value will be inserted.

---

### **Summary**
| **Query** | **Explanation** |
|-----------|---------------|
| `INSERT INTO test(id, name) VALUES (1, 'a');` | Inserts a single row with explicit column names. |
| `INSERT INTO test(id, name) VALUES (1, 'a'), (3, 'c'), (2, 'd');` | Inserts multiple rows in a single query. |
| `INSERT INTO test VALUES (5, 'e');` | Inserts a row without specifying columns (values must match table structure). |
| `INSERT INTO test(name) VALUES ('f');` | Inserts only the `name` column (other columns must allow NULL, have a default, or be auto-generated). |

---

### **📌 SQL Notes: `SELECT` & `WHERE` Clause**  

---

## **1. Basic `SELECT` Statement**
### **Retrieve Specific Columns**
```sql
SELECT id FROM test;
```
- Fetches only the `id` column from the `test` table.

### **Retrieve All Columns**
```sql
SELECT * FROM test;
```
- Fetches **all columns** from the `test` table.

---

## **2. Filtering Data with `WHERE`**
### **Equality Condition**
```sql
SELECT * FROM test WHERE id = 1;
```
- Retrieves records where `id` is **equal to 1**.

### **Not Equal Condition**
```sql
SELECT * FROM test WHERE id != 1;
```
or  
```sql
SELECT * FROM test WHERE id <> 1;
```
- Retrieves records where `id` is **not equal to 1**.

---

## **3. Using `IN` & `NOT IN`**
### **Matching Multiple Values (`IN`)**
```sql
SELECT * FROM test WHERE id IN (1, 3);
```
- Retrieves records where `id` is **either 1 or 3**.

### **Excluding Specific Values (`NOT IN`)**
```sql
SELECT * FROM test WHERE id NOT IN (1, 3);
```
- Retrieves records where `id` is **not 1 or 3**.

---

## **4. Checking `NULL` Values**
### **Find Rows Where `id` is `NULL`**
```sql
SELECT * FROM test WHERE id IS NULL;
```
- Retrieves records where `id` has a **NULL value**.

### **Find Rows Where `id` is NOT `NULL`**
```sql
SELECT * FROM test WHERE id IS NOT NULL;
```
- Retrieves records where `id` **is not NULL**.

---

## **5. Comparison Operators**
### **Less Than (`<`)**
```sql
SELECT * FROM test WHERE id < 3;
```
- Retrieves records where `id` is **less than 3**.

### **Greater Than (`>`)**
```sql
SELECT * FROM test WHERE id > 3;
```
- Retrieves records where `id` is **greater than 3**.

### **Less Than or Equal To (`<=`)**
```sql
SELECT * FROM test WHERE id <= 3;
```
- Retrieves records where `id` is **less than or equal to 3**.

### **Greater Than or Equal To (`>=`)**
```sql
SELECT * FROM test WHERE id >= 3;
```
- Retrieves records where `id` is **greater than or equal to 3**.

---

### **🔹 Summary Table**

| Operator | Description | Example |
|----------|------------|---------|
| `=` | Equals | `id = 1` |
| `!=` or `<>` | Not equal | `id != 1` |
| `IN` | Matches values in a list | `id IN (1,3)` |
| `NOT IN` | Excludes values | `id NOT IN (1,3)` |
| `IS NULL` | Checks if value is NULL | `id IS NULL` |
| `IS NOT NULL` | Checks if value is NOT NULL | `id IS NOT NULL` |
| `<` | Less than | `id < 3` |
| `>` | Greater than | `id > 3` |
| `<=` | Less than or equal to | `id <= 3` |
| `>=` | Greater than or equal to | `id >= 3` |

---

### **📌 SQL Notes: `DELETE` & `UPDATE` Commands**  

---

## **1. Deleting Records (`DELETE`)**  
### **Delete Specific Record**
```sql
DELETE FROM test WHERE id = 3;
```
- Deletes the row where `id = 3`.
- **Important:** If `WHERE` is not used, **all records in the table will be deleted**.

### **Delete All Records (Use with Caution!)**
```sql
DELETE FROM test;
```
- Deletes **all rows** from the `test` table but **keeps the table structure**.

### **Delete All Rows & Reset Auto Increment**
```sql
TRUNCATE TABLE test;
```
- Deletes all records **faster than `DELETE`** and **resets AUTO_INCREMENT**.

---

## **2. Updating Records (`UPDATE`)**  
### **Update `id` Where It is `NULL`**
```sql
UPDATE test SET id = 7 WHERE id IS NULL;
```
- Changes `id` to `7` for all rows where `id` is `NULL`.

### **Update Multiple Columns for a Specific Record**
```sql
UPDATE test SET id = 8, name = 'x' WHERE id = 2;
```
- Updates `id = 8` and `name = 'x'` for the row where `id = 2`.

---

## **🔹 Important Notes**
1. **Always use `WHERE`** in `DELETE` and `UPDATE` to avoid modifying all records.  
2. **Use `ROLLBACK` if inside a transaction** to undo changes if needed.  
3. **`TRUNCATE` is faster than `DELETE`** for removing all rows but cannot be rolled back in most databases.  

---

### **🔹 Summary Table**

| Command | Description | Example |
|---------|------------|---------|
| `DELETE` | Deletes specific row(s) | `DELETE FROM test WHERE id = 3;` |
| `DELETE` (All) | Deletes all rows (without resetting auto-increment) | `DELETE FROM test;` |
| `TRUNCATE` | Deletes all rows & resets auto-increment | `TRUNCATE TABLE test;` |
| `UPDATE` | Modifies specific records | `UPDATE test SET id=8 WHERE id=2;` |
| `UPDATE` (Multiple) | Updates multiple columns | `UPDATE test SET id=8, name='x' WHERE id=2;` |

---

### **📌 SQL Notes: `BETWEEN` & `NOT BETWEEN` Operators**  

---

## **1. `BETWEEN` Operator**  
### **Syntax:**  
```sql
SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2;
```
- Fetches rows where the column value **falls within the given range** (inclusive of both values).  

### **Example:**  
```sql
SELECT * FROM test WHERE id BETWEEN 1 AND 5;
```
- Retrieves records where `id` is **between 1 and 5** (including 1 and 5).

---

## **2. `NOT BETWEEN` Operator**  
### **Syntax:**  
```sql
SELECT * FROM table_name WHERE column_name NOT BETWEEN value1 AND value2;
```
- Fetches rows **outside the given range**.  

### **Example:**  
```sql
SELECT * FROM test WHERE id NOT BETWEEN 1 AND 5;
```
- Retrieves records where `id` is **less than 1 or greater than 5**.

---

## **3. Does `BETWEEN` Work on Strings?**
Yes! `BETWEEN` can be used with **strings** because SQL compares strings **lexicographically** (dictionary order).  

### **Example (String Comparison):**  
```sql
SELECT * FROM test WHERE name BETWEEN 'a' AND 'm';
```
- Retrieves records where `name` starts **between 'a' and 'm'** (including 'a' and 'm').

```sql
SELECT * FROM test WHERE name NOT BETWEEN 'a' AND 'm';
```
- Retrieves records where `name` starts **before 'a' or after 'm'**.

---

### **🔹 Summary Table**

| Operator | Works On | Description | Example |
|----------|---------|------------|---------|
| `BETWEEN` | Numbers, Dates, Strings | Finds values within a range (inclusive) | `id BETWEEN 1 AND 5` |
| `NOT BETWEEN` | Numbers, Dates, Strings | Finds values outside the range | `id NOT BETWEEN 1 AND 5` |
| `BETWEEN` (Strings) | Strings (Lexicographically) | Finds values between two words | `name BETWEEN 'a' AND 'm'` |

---

### select * from test where mod(id,2)=0;  ( mod gives remainder )


---

### **📌 MySQL Operators with Explanation & Examples**  

MySQL supports different types of operators for performing operations on data. They are categorized as follows:

---

## **1. Arithmetic Operators**  
Used for mathematical calculations.  

| Operator | Description | Example | Result |
|----------|------------|---------|--------|
| `+` | Addition | `SELECT 10 + 5;` | `15` |
| `-` | Subtraction | `SELECT 10 - 5;` | `5` |
| `*` | Multiplication | `SELECT 10 * 5;` | `50` |
| `/` | Division | `SELECT 10 / 5;` | `2` |
| `%` | Modulus (Remainder) | `SELECT 10 % 3;` | `1` |

---

## **2. Comparison (Relational) Operators**  
Used to compare values and return **TRUE (1), FALSE (0), or NULL**.  

| Operator | Description | Example | Result |
|----------|------------|---------|--------|
| `=` | Equal to | `SELECT 5 = 5;` | `1` (TRUE) |
| `!=` or `<>` | Not equal to | `SELECT 5 <> 3;` | `1` (TRUE) |
| `>` | Greater than | `SELECT 5 > 3;` | `1` (TRUE) |
| `<` | Less than | `SELECT 5 < 3;` | `0` (FALSE) |
| `>=` | Greater than or equal to | `SELECT 5 >= 5;` | `1` (TRUE) |
| `<=` | Less than or equal to | `SELECT 3 <= 5;` | `1` (TRUE) |
| `BETWEEN` | Within a range (inclusive) | `SELECT 5 BETWEEN 3 AND 7;` | `1` (TRUE) |
| `NOT BETWEEN` | Outside a range | `SELECT 5 NOT BETWEEN 3 AND 7;` | `0` (FALSE) |
| `IN` | Match any value in a list | `SELECT 5 IN (1, 3, 5);` | `1` (TRUE) |
| `NOT IN` | Not in the list | `SELECT 2 NOT IN (1, 3, 5);` | `1` (TRUE) |
| `IS NULL` | Check for NULL value | `SELECT NULL IS NULL;` | `1` (TRUE) |
| `IS NOT NULL` | Check for NOT NULL | `SELECT 5 IS NOT NULL;` | `1` (TRUE) |

---

## **3. Logical Operators**  
Used to combine multiple conditions in queries.  

| Operator | Description | Example |
|----------|------------|---------|
| `AND` | Returns TRUE if both conditions are TRUE | `SELECT * FROM users WHERE age > 18 AND city = 'Mumbai';` |
| `OR` | Returns TRUE if at least one condition is TRUE | `SELECT * FROM users WHERE age > 18 OR city = 'Mumbai';` |
| `NOT` | Reverses the condition | `SELECT * FROM users WHERE NOT age > 18;` |

---

## **4. String Operators**  
Used for string manipulation.  

| Operator | Description | Example | Result |
|----------|------------|---------|--------|
| `||` or `CONCAT()` | String concatenation | `SELECT 'Hello' || ' World';` or `SELECT CONCAT('Hello', ' World');` | `'Hello World'` |
| `LIKE` | Pattern matching (case-insensitive) | `SELECT * FROM users WHERE name LIKE 'A%';` | (Names starting with A) |
| `NOT LIKE` | Exclude pattern matches | `SELECT * FROM users WHERE name NOT LIKE 'A%';` | (Names not starting with A) |

- **`LIKE` Wildcards**:
  - `%` = Any number of characters (`'A%'` → starts with 'A')
  - `_` = Single character (`'A_'` → starts with 'A' followed by any one character)

---

## **5. Bitwise Operators**  
Used for bitwise operations on integers.  

| Operator | Description | Example | Result |
|----------|------------|---------|--------|
| `&` | Bitwise AND | `SELECT 5 & 3;` | `1` |
| `|` | Bitwise OR | `SELECT 5 | 3;` | `7` |
| `^` | Bitwise XOR | `SELECT 5 ^ 3;` | `6` |
| `~` | Bitwise NOT | `SELECT ~5;` | `-6` |
| `<<` | Left Shift | `SELECT 5 << 1;` | `10` |
| `>>` | Right Shift | `SELECT 5 >> 1;` | `2` |

---

## **6. Assignment Operators**  
Used to assign values in `SET` statements.  

| Operator | Description | Example |
|----------|------------|---------|
| `=` | Assign a value | `SET @x = 10;` |
| `:=` | Assign a value within a query | `SELECT @y := 20;` |

---

## **7. Other Operators**  
### **CASE Statement (Conditional Logic)**
```sql
SELECT id, name, 
CASE 
    WHEN age < 18 THEN 'Minor' 
    WHEN age BETWEEN 18 AND 60 THEN 'Adult' 
    ELSE 'Senior' 
END AS age_category 
FROM users;
```
- Categorizes ages into "Minor", "Adult", or "Senior".

---

### **🔹 Summary Table of Operators**
| **Type** | **Operators** |
|----------|--------------|
| **Arithmetic** | `+`, `-`, `*`, `/`, `%` |
| **Comparison** | `=`, `!=`, `<>`, `>`, `<`, `>=`, `<=`, `BETWEEN`, `IN`, `NOT IN`, `IS NULL`, `IS NOT NULL` |
| **Logical** | `AND`, `OR`, `NOT` |
| **String** | `||`, `CONCAT()`, `LIKE`, `NOT LIKE` |
| **Bitwise** | `&`, `|`, `^`, `~`, `<<`, `>>` |
| **Assignment** | `=`, `:=` |
| **Pattern Matching** | `%`, `_` (for `LIKE`) |

---

### **📌 MySQL `ASCII()` Function**  

The `ASCII()` function in MySQL returns the **ASCII (American Standard Code for Information Interchange) value** of the first character in a string.

### **Syntax:**  
```sql
SELECT ASCII(character);
```
- Returns an integer representing the ASCII value of the given character.
- If the input is a string, only the **first character** is considered.
- If the input is an **empty string (`''`)**, it returns `0`.

---

### **Example Usage**  

#### **1. Getting ASCII value of a single character**  
```sql
SELECT ASCII('a');
```
**Output:**  
```
97
```
(ASCII value of `'a'` is **97**)

```sql
SELECT ASCII('A');
```
**Output:**  
```
65
```
(ASCII value of `'A'` is **65**)

#### **2. Checking ASCII for a Number Character**
```sql
SELECT ASCII('1');
```
**Output:**  
```
49
```
(ASCII value of `'1'` is **49**)

#### **3. ASCII Value of Special Characters**
```sql
SELECT ASCII('@');
```
**Output:**  
```
64
```
(ASCII value of `'@'` is **64**)

#### **4. ASCII Value of an Empty String**
```sql
SELECT ASCII('');
```
**Output:**  
```
0
```
(Empty string returns **0**)

#### **5. ASCII Value of First Character in a String**
```sql
SELECT ASCII('Hello');
```
**Output:**  
```
72
```
(ASCII value of `'H'` is **72**; only the **first** character is considered)

---

### **🔹 ASCII Value Table for Common Characters**
| Character | ASCII Value |
|-----------|------------|
| `'A'` | 65 |
| `'B'` | 66 |
| `'a'` | 97 |
| `'b'` | 98 |
| `'0'` | 48 |
| `'1'` | 49 |
| `'@'` | 64 |
| `'#'` | 35 |
| `' '` (Space) | 32 |

---

### **📌 Use Case: Finding Non-Printable Characters**
You can use `ASCII()` to check for unexpected special characters in data:
```sql
SELECT id, name FROM users WHERE ASCII(name) < 32;
```
- This finds names that start with **control characters (ASCII < 32)**, which might be errors.

---

### **Conclusion**
- `ASCII()` is useful for **character encoding, sorting, and data validation**.
- It only considers the **first character** of the input string.
- Returns `0` for an **empty string**.

---

### **📌 MySQL Notes: ALTER TABLE (Adding, Modifying, and Renaming Columns & Table)**  

---

## **1. Adding & Dropping Columns (`ALTER TABLE`)**  

### **Add a New Column**  
```sql
ALTER TABLE test ADD c1 INT;
```
- Adds a new column `c1` of type `INT` to the `test` table.

### **Remove a Column**  
```sql
ALTER TABLE test DROP COLUMN c1;
```
- Removes column `c1` from the `test` table.

### **Add Column with Default Value**  
```sql
ALTER TABLE test ADD c1 INT DEFAULT 10;
```
- Adds column `c1` with a default value of `10` for new records.

### **Drop the Column Again**  
```sql
ALTER TABLE test DROP COLUMN c1;
```
- Removes `c1` from the table.

---

## **2. Changing Column Datatype (`MODIFY` vs `CHANGE`)**  

### **Modify Column Size**
```sql
ALTER TABLE test MODIFY name VARCHAR(20);
```
- Changes `name` column datatype to `VARCHAR(20)`.

```sql
ALTER TABLE test MODIFY name VARCHAR(10);
```
- Changes it back to `VARCHAR(10)`.

### **Modify Column to NOT NULL**
```sql
ALTER TABLE test MODIFY id INT NOT NULL;
```
- `id` cannot be `NULL` anymore.

### **Insert Fails Due to NOT NULL Constraint**
```sql
INSERT INTO test(name) VALUES('y'); 
```
- **Fails** because `id` is `NOT NULL` but no value is provided.

---

## **3. Adding NOT NULL with a Default Value**  

### **Set Default Value for `id`**
```sql
ALTER TABLE test MODIFY id INT NOT NULL DEFAULT 1;
```
- Now, `id` **cannot be NULL** and will have a **default value of `1`** if not provided.

```sql
INSERT INTO test(name) VALUES('y');
```
- **Works now!** The default value `1` is assigned to `id`.

---

## **4. Renaming Tables (`RENAME TO`)**  

### **Rename Table**
```sql
ALTER TABLE test RENAME TO test2;
```
- Renames `test` table to `test2`.

### **Rename Table Back**
```sql
ALTER TABLE test2 RENAME TO test;
```
- Renames `test2` back to `test`.

---

### **🔹 Summary Table**

| **Command** | **Description** |
|-------------|---------------|
| `ALTER TABLE test ADD c1 INT;` | Adds a new column `c1` |
| `ALTER TABLE test DROP COLUMN c1;` | Deletes column `c1` |
| `ALTER TABLE test ADD c1 INT DEFAULT 10;` | Adds `c1` with default value `10` |
| `ALTER TABLE test MODIFY name VARCHAR(20);` | Changes `name` column to `VARCHAR(20)` |
| `ALTER TABLE test MODIFY id INT NOT NULL;` | Sets `id` column as `NOT NULL` |
| `ALTER TABLE test MODIFY id INT NOT NULL DEFAULT 1;` | Sets `id` as `NOT NULL` with a default value |
| `ALTER TABLE test RENAME TO test2;` | Renames table to `test2` |
| `ALTER TABLE test2 RENAME TO test;` | Renames `test2` back to `test` |

---

### **📌 MySQL Notes: UNIQUE Key Constraints**  

---

## **1. UNIQUE Key on a Single Column**  

### **Create Table with UNIQUE Key**  
```sql
CREATE TABLE t_uk (
    id INT UNIQUE, 
    name VARCHAR(10)
);
```
- The `id` column is **UNIQUE**, meaning duplicate values are **not allowed**.  

### **Insert Data**  
```sql
INSERT INTO t_uk VALUES (1, 'a');  -- ✅ Success
INSERT INTO t_uk VALUES (1, 'b');  -- ❌ Fails (Duplicate id)
```
- The second insert fails because `1` already exists in the `id` column.  

```sql
INSERT INTO t_uk VALUES (NULL, 'b');  -- ✅ Success
INSERT INTO t_uk VALUES (NULL, 'b');  -- ✅ Success
```
- **UNIQUE allows multiple `NULL` values** (Unlike `PRIMARY KEY`, which does **not** allow `NULL`).

---

## **2. Composite UNIQUE Key (Multiple Columns)**  

### **Create Table with Composite UNIQUE Key**  
```sql
CREATE TABLE test_comp_uk (
    c1 INT, 
    c2 INT, 
    c3 VARCHAR(10), 
    UNIQUE (c1, c2)
);
```
- The combination of `(c1, c2)` **must be unique**, but individual columns can have duplicates.  

### **Insert Data**  
```sql
INSERT INTO test_comp_uk VALUES (1, 1, 'a');  -- ✅ Success
INSERT INTO test_comp_uk VALUES (1, 2, 'a');  -- ✅ Success
INSERT INTO test_comp_uk VALUES (2, 2, 'a');  -- ✅ Success
INSERT INTO test_comp_uk VALUES (2, 2, 'c');  -- ❌ Fails (1st and 2nd columns duplicate)
```
- The **last insert fails** because `(2,2)` already exists.  

---

## **3. Multiple UNIQUE Constraints on Different Columns**  

### **Create Table with Multiple UNIQUE Constraints**  
```sql
CREATE TABLE t_mult_uk (
    c1 INT UNIQUE, 
    c2 INT UNIQUE, 
    c3 VARCHAR(10)
);
```
- Here, **both `c1` and `c2` are individually unique**, meaning:
  - Duplicates in `c1` **are not allowed**.
  - Duplicates in `c2` **are not allowed**.
  - `c3` has **no constraints**.

### **Example Insertions**  
```sql
INSERT INTO t_mult_uk VALUES (1, 10, 'a');  -- ✅ Success
INSERT INTO t_mult_uk VALUES (2, 20, 'b');  -- ✅ Success
INSERT INTO t_mult_uk VALUES (1, 30, 'c');  -- ❌ Fails (Duplicate c1)
INSERT INTO t_mult_uk VALUES (3, 20, 'd');  -- ❌ Fails (Duplicate c2)
```
- **Unique constraints apply separately** to `c1` and `c2`.

---

### **🔹 Summary Table**
| **Concept** | **Syntax** | **Behavior** |
|------------|-----------|------------|
| **Single UNIQUE Key** | `id INT UNIQUE` | Ensures `id` values are unique, but allows multiple `NULL`s. |
| **Composite UNIQUE Key** | `UNIQUE(c1, c2)` | Ensures `(c1, c2)` combinations are unique. |
| **Multiple UNIQUE Columns** | `c1 INT UNIQUE, c2 INT UNIQUE` | Both `c1` and `c2` must have unique values, independently. |
| **NULL Handling** | `INSERT INTO table VALUES (NULL, 'data');` | **Allowed multiple times** in a UNIQUE column. |

---

### **📌 Key Differences: UNIQUE vs PRIMARY KEY**
| Feature | UNIQUE Key | PRIMARY KEY |
|---------|-----------|-------------|
| **NULL Values** | ✅ Allowed (Multiple `NULL`s) | ❌ Not Allowed |
| **Duplicates** | ❌ Not Allowed | ❌ Not Allowed |
| **Multiple in Table?** | ✅ Can have multiple `UNIQUE` keys | ❌ Only **one** PRIMARY KEY per table |
| **Index Type** | ✅ Creates a unique index | ✅ Creates a unique clustered index |

---

### **📌 MySQL Constraints (6 Main Types)**  

**Constraints** are rules applied to table columns to ensure data integrity and consistency.  

---

## **1️⃣ PRIMARY KEY**  
- Ensures that a column (or set of columns) has **unique values** and **does not allow NULL**.  
- Each table can have **only one** `PRIMARY KEY`.  
- It automatically creates a **unique index**.  

### **Syntax:**  
```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50)
);
```
✅ **Valid:**  
```sql
INSERT INTO students VALUES (1, 'Alice');
INSERT INTO students VALUES (2, 'Bob');
```
❌ **Invalid (Duplicate student_id):**  
```sql
INSERT INTO students VALUES (1, 'Charlie');  -- Fails
```
❌ **Invalid (NULL student_id):**  
```sql
INSERT INTO students VALUES (NULL, 'David'); -- Fails
```

---

## **2️⃣ UNIQUE KEY**  
- Ensures that **all values in a column are unique** but allows **NULL values** (multiple `NULL`s are permitted).  

### **Syntax:**  
```sql
CREATE TABLE employees (
    emp_id INT UNIQUE,
    name VARCHAR(50)
);
```
✅ **Valid:**  
```sql
INSERT INTO employees VALUES (1, 'John');
INSERT INTO employees VALUES (2, 'Jane');
INSERT INTO employees VALUES (NULL, 'Alice');  -- NULL allowed
INSERT INTO employees VALUES (NULL, 'Bob');    -- NULL allowed
```
❌ **Invalid (Duplicate emp_id):**  
```sql
INSERT INTO employees VALUES (1, 'Charlie');  -- Fails
```

---

## **3️⃣ NOT NULL**  
- Ensures that a column **cannot store NULL values**.  

### **Syntax:**  
```sql
CREATE TABLE products (
    product_id INT NOT NULL,
    name VARCHAR(50)
);
```
✅ **Valid:**  
```sql
INSERT INTO products VALUES (1, 'Laptop');
INSERT INTO products VALUES (2, 'Phone');
```
❌ **Invalid (NULL value in product_id):**  
```sql
INSERT INTO products VALUES (NULL, 'Tablet'); -- Fails
```

---

## **4️⃣ CHECK** *(Available in MySQL 8.0+)*  
- Ensures that values meet a **specific condition** before being inserted/updated.  

### **Syntax:**  
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    quantity INT CHECK (quantity > 0)
);
```
✅ **Valid:**  
```sql
INSERT INTO orders VALUES (1, 5);  -- Success
```
❌ **Invalid (quantity <= 0):**  
```sql
INSERT INTO orders VALUES (2, -3); -- Fails
```

---

## **5️⃣ DEFAULT**  
- Assigns a **default value** if no value is provided.  

### **Syntax:**  
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    role VARCHAR(20) DEFAULT 'User'
);
```
✅ **Valid (Uses Default Value):**  
```sql
INSERT INTO users (id) VALUES (1);  -- role = 'User'
```
✅ **Valid (Overrides Default Value):**  
```sql
INSERT INTO users VALUES (2, 'Admin');  -- role = 'Admin'
```

---

## **6️⃣ FOREIGN KEY**  
- Enforces **referential integrity** by linking to a column in another table.  
- Prevents inserting values that do not exist in the **parent table**.  

### **Syntax:**  
```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);
  
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```
✅ **Valid:**  
```sql
INSERT INTO departments VALUES (1, 'HR');
INSERT INTO employees VALUES (101, 'Alice', 1);  -- Allowed (dept_id exists in departments)
```
❌ **Invalid (dept_id does not exist in departments):**  
```sql
INSERT INTO employees VALUES (102, 'Bob', 5); -- Fails
```

---

### **🔹 Summary Table**

| **Constraint** | **Description** | **Allows NULL?** | **Allows Duplicate?** |
|--------------|---------------|----------------|----------------|
| **PRIMARY KEY** | Uniquely identifies a row | ❌ No | ❌ No |
| **UNIQUE** | Ensures all values are unique | ✅ Yes (Multiple `NULL`s allowed) | ❌ No (except `NULL`) |
| **NOT NULL** | Prevents `NULL` values | ❌ No | ✅ Yes |
| **CHECK** | Ensures values meet a condition | ✅ Yes (Unless restricted) | ✅ Yes |
| **DEFAULT** | Assigns a default value if not provided | ✅ Yes | ✅ Yes |
| **FOREIGN KEY** | Ensures referential integrity | ✅ Yes | ✅ Yes (If allowed by parent table) |

---

### **🔹 Key Differences: PRIMARY KEY vs UNIQUE KEY**
| Feature | PRIMARY KEY | UNIQUE KEY |
|---------|-------------|-------------|
| **NULL Values** | ❌ Not Allowed | ✅ Allowed |
| **Duplicates** | ❌ Not Allowed | ❌ Not Allowed |
| **Multiple in Table?** | ❌ Only one | ✅ Multiple allowed |
| **Index Type** | ✅ Clustered Index | ✅ Non-clustered Index |

---


### **📌 MySQL Notes: SQL Types, Transactions & Joins**  

---

## **1️⃣ SQL Types (Categories of SQL Commands)**  

| **SQL Type** | **Description** | **Example Commands** |
|-------------|----------------|------------------|
| **DDL (Data Definition Language)** | Defines & modifies database structure | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML (Data Manipulation Language)** | Manipulates data in tables | `INSERT`, `UPDATE`, `DELETE` |
| **DCL (Data Control Language)** | Controls user permissions & access | `GRANT`, `REVOKE` |
| **TCL (Transaction Control Language)** | Manages transactions in SQL | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |
| **DRL (Data Retrieval Language)** | Fetches data from the database | `SELECT` |

---

## **2️⃣ Transactions: COMMIT & ROLLBACK**  
Transactions allow executing multiple SQL statements as a **single unit of work**.  

### **Transaction Flow**
1. **Start Transaction:**  
   ```sql
   START TRANSACTION;
   ```
2. **Execute Queries:**  
   ```sql
   INSERT INTO table_name VALUES (1, 'Data');
   UPDATE table_name SET column = 'new_value' WHERE id = 1;
   ```
3. **Decide on Transaction Outcome:**
   - **Happy?** ✅ **Commit:**  
     ```sql
     COMMIT; -- Saves all changes permanently
     ```
     - **After `COMMIT`**, you **CANNOT ROLLBACK** changes.
   - **Unhappy?** ❌ **Rollback:**  
     ```sql
     ROLLBACK; -- Reverts all changes since START TRANSACTION
     ```
     - **After `ROLLBACK`**, no changes are saved.

---

## **3️⃣ Joins in SQL**
Joins are used to **combine rows** from multiple tables based on related columns.

### **Types of Joins:**
| **Join Type** | **Description** |
|--------------|----------------|
| **Cross Join** | Cartesian product of both tables (no condition). |
| **Equi Join** | Uses `=` condition to match columns. |
| **Inner Join** | Returns matching rows from both tables. |
| **Outer Join** | Returns matched + unmatched rows (LEFT, RIGHT, FULL). |
| **Left Outer Join** | All records from the left table + matching rows from right. |
| **Right Outer Join** | All records from the right table + matching rows from left. |
| **Full Outer Join** | Returns all rows from both tables (MySQL does not support directly). |
| **Non-Equi Join** | Uses conditions like `<`, `>`, `!=` instead of `=`. |

---

## **4️⃣ SQL Join Examples**
### **Table Creation**
```sql
CREATE TABLE t1 (
    c1 INT,
    c2 VARCHAR(5)
);

CREATE TABLE t2 (
    c1 INT,
    c3 VARCHAR(5)
);
```
### **Insert Data**
```sql
INSERT INTO t1 VALUES (1, 'a'), (2, 'b'), (3, 'c');
INSERT INTO t2 VALUES (3, 'x'), (4, 'y'), (5, 'z');
```

---

### **❌ Ambiguous Column Error**
```sql
SELECT c2, c2, c3 FROM t1, t2; -- Error (Column c2 appears twice)
```
- To avoid this, use **table aliases or explicit table names**.

---

### **✅ Cross Join (Cartesian Product)**
```sql
SELECT * FROM t1 CROSS JOIN t2;
```
- Combines **all rows** from `t1` with **all rows** from `t2`.  
- If `t1` has **3 rows** and `t2` has **3 rows**, the result will have **3 × 3 = 9 rows**.

---

### **✅ Correct Query Using Column Names**
```sql
SELECT t1.c1, t1.c2, t2.c3 FROM t1 CROSS JOIN t2;
```
- This prevents **ambiguity errors** and ensures clarity.

---

### **❌ Incorrect Query (Ambiguous Columns)**
```sql
SELECT c1, c2, c3 FROM t1 CROSS JOIN t2; -- Error: c1 exists in both tables
```
- Must specify `t1.c1` or `t2.c1` to avoid confusion.

---

## **🔹 Summary**
| **Concept** | **Key Takeaways** |
|------------|-----------------|
| **SQL Types** | DDL, DML, DCL, TCL, DRL |
| **Transaction Flow** | `START TRANSACTION` → Queries → `COMMIT` / `ROLLBACK` |
| **COMMIT vs ROLLBACK** | `COMMIT` saves permanently, `ROLLBACK` undoes changes |
| **Cross Join** | Produces Cartesian Product (no condition) |
| **Ambiguous Column Issue** | Use table aliases to avoid errors |

---


# **📌 MySQL Set Operators: UNION, UNION ALL, INTERSECT, EXCEPT**  

Set operators **combine the results** of two or more `SELECT` queries.  

---

## **1️⃣ UNION**  
- **Removes duplicates** (returns only unique rows).  
- Both queries must have the **same number of columns** with **compatible data types**.  

### **Syntax:**  
```sql
SELECT column1, column2 FROM table1
UNION
SELECT column1, column2 FROM table2;
```

### **Example:**  
```sql
CREATE TABLE t1 (id INT, name VARCHAR(10));
CREATE TABLE t2 (id INT, name VARCHAR(10));

INSERT INTO t1 VALUES (1, 'Alice'), (2, 'Bob'), (3, 'Charlie');
INSERT INTO t2 VALUES (3, 'Charlie'), (4, 'David'), (5, 'Eve');

SELECT * FROM t1
UNION
SELECT * FROM t2;
```
### **Output:**
| id | name   |
|----|--------|
| 1  | Alice  |
| 2  | Bob    |
| 3  | Charlie |
| 4  | David  |
| 5  | Eve    |

✅ **Duplicates are removed** (`Charlie` appears only once).  

---

## **2️⃣ UNION ALL**  
- **Includes duplicates** (returns all records from both queries).  

### **Syntax:**  
```sql
SELECT column1, column2 FROM table1
UNION ALL
SELECT column1, column2 FROM table2;
```

### **Example:**  
```sql
SELECT * FROM t1
UNION ALL
SELECT * FROM t2;
```
### **Output:**
| id | name   |
|----|--------|
| 1  | Alice  |
| 2  | Bob    |
| 3  | Charlie |
| 3  | Charlie |
| 4  | David  |
| 5  | Eve    |

✅ **Duplicates are kept** (`Charlie` appears twice).  

---

## **3️⃣ INTERSECT (Not Natively Supported in MySQL)**  
- Returns **only common records** between two queries.  

### **Workaround Using `INNER JOIN`**
```sql
SELECT id, name FROM t1
INNER JOIN t2 USING(id, name);
```

### **Output:**
| id | name   |
|----|--------|
| 3  | Charlie |

✅ **Only common rows are returned**.

---

## **4️⃣ EXCEPT (MySQL Equivalent: `LEFT JOIN WHERE NULL` or `NOT IN`)**  
- Returns rows that exist in the **first query but not in the second**.  
- MySQL does **not support `EXCEPT` directly**, but we can achieve the same using `LEFT JOIN WHERE NULL` or `NOT IN`.  

### **Syntax Using `LEFT JOIN WHERE NULL`**
```sql
SELECT t1.id, t1.name 
FROM t1
LEFT JOIN t2 ON t1.id = t2.id AND t1.name = t2.name
WHERE t2.id IS NULL;
```
### **Syntax Using `NOT IN`**
```sql
SELECT id, name FROM t1
WHERE id NOT IN (SELECT id FROM t2);
```

### **Output:**
| id | name   |
|----|--------|
| 1  | Alice  |
| 2  | Bob    |

✅ **Only records from `t1` that are not in `t2` are returned**.

---

## **🔹 Summary Table**

| **Set Operator** | **Description** | **Removes Duplicates?** | **MySQL Support** |
|----------------|----------------|------------------|------------------|
| `UNION` | Combines results, removes duplicates | ✅ Yes | ✅ Yes |
| `UNION ALL` | Combines results, keeps duplicates | ❌ No | ✅ Yes |
| `INTERSECT` | Returns common records | ✅ Yes | ❌ No (Use `INNER JOIN`) |
| `EXCEPT` | Returns records in first query but not second | ✅ Yes | ❌ No (Use `LEFT JOIN WHERE NULL` or `NOT IN`) |

---

## **🔹 Key Differences**
| Feature | UNION | UNION ALL | INTERSECT | EXCEPT |
|---------|-------|----------|-----------|--------|
| **Removes Duplicates?** | ✅ Yes | ❌ No | ✅ Yes | ✅ Yes |
| **Performance** | Slower (sorting required) | Faster | Slower | Slower |
| **Common Use Case** | Unique combined list | Full dataset (with duplicates) | Find common records | Find missing records |

---

# **📌 MySQL Aggregate Functions: COUNT, SUM, MAX, MIN, AVG**  

Aggregate functions **perform calculations** on multiple rows and return a **single value**.  

---

## **1️⃣ COUNT Function**
The `COUNT()` function counts the number of rows.  

### **Basic Usage:**
```sql
SELECT COUNT(*) FROM t_def;  -- Counts all rows, including NULL values
SELECT COUNT(1) FROM t_def;  -- Equivalent to COUNT(*)
SELECT COUNT('a') FROM t_def;  -- Counts all rows, but ignores NULLs
SELECT COUNT(2) FROM t_def;  -- Same as COUNT(*), as 2 is a constant
```

### **COUNT with Specific Column**
```sql
SELECT COUNT(id) FROM t_def;  -- Counts only non-NULL values in 'id' column
SELECT COUNT(name) FROM t_def;  -- Counts non-NULL values in 'name' column
```

### **COUNT with DISTINCT Values**
```sql
SELECT COUNT(DISTINCT name) FROM t_def;  -- Counts unique values in 'name'
SELECT COUNT(DISTINCT id) FROM t_def;  -- Counts unique values in 'id'
```

---

## **2️⃣ SUM Function**
The `SUM()` function calculates the **total sum** of a numeric column.

### **Usage:**
```sql
SELECT SUM(id) FROM t_def;  -- Returns the total sum of 'id'
SELECT SUM(DISTINCT id) FROM t_def;  -- Sums only distinct values in 'id'
```
✅ **Only works on numeric values**.  
❌ **Ignores NULL values**.

---

## **3️⃣ MAX and MIN Functions**
- `MAX()` returns the **largest** value.
- `MIN()` returns the **smallest** value.
- ✅ Works on **ALL DATA TYPES** (numeric, text, dates, etc.).

### **Usage:**
```sql
SELECT MAX(id) FROM t_def;  -- Returns the highest ID
SELECT MIN(id) FROM t_def;  -- Returns the lowest ID

SELECT MAX(name) FROM t_def;  -- Returns the last name in alphabetical order
SELECT MIN(name) FROM t_def;  -- Returns the first name in alphabetical order
```
📌 **Text comparison is based on ASCII values**.  

---

## **4️⃣ AVG Function**
The `AVG()` function calculates the **average value** of a numeric column.

### **Usage:**
```sql
SELECT AVG(id) FROM t_def;  -- Returns the average of 'id'
SELECT AVG(DISTINCT id) FROM t_def;  -- Averages only distinct values in 'id'
```
✅ **Works only on numeric values**.  
❌ **Ignores NULL values**.

---

## **🔹 Summary Table**

| **Function** | **Description** | **Works on Data Type** | **NULL Handling** |
|-------------|----------------|----------------|----------------|
| `COUNT(*)` | Counts all rows | Any | Includes NULLs |
| `COUNT(column)` | Counts non-NULL values | Any | Excludes NULLs |
| `COUNT(DISTINCT column)` | Counts unique non-NULL values | Any | Excludes NULLs |
| `SUM(column)` | Returns sum of values | Numeric only | Ignores NULLs |
| `SUM(DISTINCT column)` | Returns sum of unique values | Numeric only | Ignores NULLs |
| `MAX(column)` | Returns highest value | Any (numbers, text, dates) | Ignores NULLs |
| `MIN(column)` | Returns lowest value | Any (numbers, text, dates) | Ignores NULLs |
| `AVG(column)` | Returns average | Numeric only | Ignores NULLs |
| `AVG(DISTINCT column)` | Returns average of unique values | Numeric only | Ignores NULLs |

---
