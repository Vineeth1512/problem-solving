# 🛠️ MySQL Stored Procedures --- Complete Notes

> **Beginner → Intermediate → Advanced**
>
> Simple English • Practical Examples • Interview Ready • Production
> Concepts

------------------------------------------------------------------------

## 📚 Table of Contents

1.  [What is a Stored Procedure?](#1-what-is-a-stored-procedure)
2.  [Why Do We Need Stored
    Procedures?](#2-why-do-we-need-stored-procedures)
3.  [Stored Procedure vs Normal SQL](#3-stored-procedure-vs-normal-sql)
4.  [Basic Syntax](#4-basic-syntax)
5.  [Why DELIMITER is Used](#5-why-delimiter-is-used)
6.  [Creating and Calling a
    Procedure](#6-creating-and-calling-a-procedure)
7.  [IN Parameters](#7-in-parameters)
8.  [OUT Parameters](#8-out-parameters)
9.  [INOUT Parameters](#9-inout-parameters)
10. [Local Variables and DECLARE](#10-local-variables-and-declare)
11. [SET and SELECT INTO](#11-set-and-select-into)
12. [IF / ELSEIF / ELSE](#12-if--elseif--else)
13. [CASE](#13-case)
14. [Loops](#14-loops)
15. [WHILE Loop](#15-while-loop)
16. [REPEAT Loop](#16-repeat-loop)
17. [LOOP and LEAVE](#17-loop-and-leave)
18. [Parameters + Conditions](#18-parameters--conditions)
19. [INSERT / UPDATE / DELETE
    Procedures](#19-insert--update--delete-procedures)
20. [Transactions](#20-transactions)
21. [Error Handling and HANDLER](#21-error-handling-and-handler)
22. [Cursors](#22-cursors)
23. [Nested Blocks](#23-nested-blocks)
24. [Calling One Procedure from
    Another](#24-calling-one-procedure-from-another)
25. [Dynamic SQL](#25-dynamic-sql)
26. [Security and Permissions](#26-security-and-permissions)
27. [Managing Procedures](#27-managing-procedures)
28. [Procedure vs Function](#28-procedure-vs-function)
29. [Advantages and Disadvantages](#29-advantages-and-disadvantages)
30. [Production-Level Guidelines](#30-production-level-guidelines)
31. [Common Mistakes](#31-common-mistakes)
32. [Interview Questions](#32-interview-questions)
33. [Quick Revision Sheet](#33-quick-revision-sheet)
34. [Practice Roadmap](#34-practice-roadmap)

------------------------------------------------------------------------

# 1. What is a Stored Procedure?

A **Stored Procedure** is a group of SQL statements stored inside the
database that can be executed by calling its name.

### Simple definition

> **A stored procedure is reusable SQL logic stored in the database and
> executed using `CALL`.**

Example:

``` sql
CREATE PROCEDURE getEmployees()
BEGIN
    SELECT * FROM emp;
END
```

Call it:

``` sql
CALL getEmployees();
```

### Real-life analogy

Think of a stored procedure like a **function in JavaScript or Java**.

JavaScript:

``` javascript
function add(a, b) {
    return a + b;
}

add(10, 20);
```

MySQL:

``` sql
CREATE PROCEDURE addNumbers(IN a INT, IN b INT)
BEGIN
    SELECT a + b;
END;
```

Call:

``` sql
CALL addNumbers(10, 20);
```

### Mental model

``` text
Application
    ↓
CALL procedure
    ↓
MySQL
    ↓
Stored SQL logic executes
    ↓
Result
```

------------------------------------------------------------------------

# 2. Why Do We Need Stored Procedures?

Suppose an application repeatedly needs:

``` sql
SELECT *
FROM emp
WHERE deptno = 20;
```

We can store this logic:

``` sql
CREATE PROCEDURE getEmployeesByDept(IN dept_id INT)
BEGIN
    SELECT *
    FROM emp
    WHERE deptno = dept_id;
END;
```

Then simply call:

``` sql
CALL getEmployeesByDept(20);
```

## Main benefits

-   ♻️ Reusability
-   📦 Encapsulates multiple SQL statements
-   🔐 Can help control access to database objects
-   🧠 Supports procedural logic
-   🔄 Reduces repeated SQL code
-   🏢 Useful for database-side business operations

> **Important:** Stored procedures are not automatically faster than
> application SQL. Performance depends on the query, indexes, execution
> plan, network cost, and overall design.

------------------------------------------------------------------------

# 3. Stored Procedure vs Normal SQL

## Normal SQL

``` text
Application
    ↓
SQL query
    ↓
Database
    ↓
Result
```

## Stored Procedure

``` text
Application
    ↓
CALL procedure
    ↓
Database
    ↓
Stored SQL logic
    ↓
Result
```

A procedure can contain many statements:

``` sql
CREATE PROCEDURE employeeOperation()
BEGIN
    SELECT ...;
    UPDATE ...;
    INSERT ...;
END;
```

------------------------------------------------------------------------

# 4. Basic Syntax

``` sql
DELIMITER //

CREATE PROCEDURE procedure_name()
BEGIN

    -- SQL statements

END //

DELIMITER ;
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE getEmployees()
BEGIN
    SELECT *
    FROM emp;
END //

DELIMITER ;
```

Call:

``` sql
CALL getEmployees();
```

------------------------------------------------------------------------

# 5. Why DELIMITER is Used

## The problem

Normally MySQL clients use:

``` text
;
```

as the statement terminator.

Inside a procedure, we also need `;`:

``` sql
CREATE PROCEDURE getEmployees()
BEGIN
    SELECT * FROM emp;
    SELECT * FROM dept;
END;
```

The client may treat the first `;` as the end of the whole
`CREATE PROCEDURE` statement.

## Solution

Temporarily change the client delimiter:

``` sql
DELIMITER //
```

Now:

``` text
;  → ends an individual SQL statement
// → ends the complete CREATE PROCEDURE statement
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE getEmployees()
BEGIN
    SELECT * FROM emp;
    SELECT * FROM dept;
END //

DELIMITER ;
```

### Important

`DELIMITER` is primarily a command understood by MySQL client tools such
as MySQL Workbench. It is not part of the stored procedure's SQL body.

### Easy memory

``` text
DELIMITER //
       ↓
Create procedure
       ↓
SQL statements end with ;
       ↓
END //
       ↓
DELIMITER ;
```

------------------------------------------------------------------------

# 6. Creating and Calling a Procedure

## Create

``` sql
DELIMITER //

CREATE PROCEDURE getEmployees()
BEGIN
    SELECT *
    FROM emp;
END //

DELIMITER ;
```

## Call

``` sql
CALL getEmployees();
```

## Recreate safely

During development, this pattern is useful:

``` sql
DROP PROCEDURE IF EXISTS getEmployees;

DELIMITER //

CREATE PROCEDURE getEmployees()
BEGIN
    SELECT *
    FROM emp;
END //

DELIMITER ;
```

------------------------------------------------------------------------

# 7. IN Parameters

`IN` means the procedure receives a value from the caller.

Syntax:

``` sql
CREATE PROCEDURE procedure_name(
    IN parameter_name datatype
)
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE getEmployeesByDept(IN dept_id INT)
BEGIN
    SELECT ename, job, sal
    FROM emp
    WHERE deptno = dept_id;
END //

DELIMITER ;
```

Call:

``` sql
CALL getEmployeesByDept(20);
```

Flow:

``` text
20
↓
dept_id
↓
WHERE deptno = dept_id
```

## Multiple IN parameters

``` sql
DELIMITER //

CREATE PROCEDURE getEmployees(
    IN dept_id INT,
    IN minimum_salary DECIMAL(10,2)
)
BEGIN
    SELECT ename, job, sal
    FROM emp
    WHERE deptno = dept_id
      AND sal > minimum_salary;
END //

DELIMITER ;
```

Call:

``` sql
CALL getEmployees(20, 2000);
```

------------------------------------------------------------------------

# 8. OUT Parameters

`OUT` means the procedure sends a value back to the caller.

Example:

``` sql
DELIMITER //

CREATE PROCEDURE getEmployeeCount(
    IN dept_id INT,
    OUT total_employees INT
)
BEGIN
    SELECT COUNT(*)
    INTO total_employees
    FROM emp
    WHERE deptno = dept_id;
END //

DELIMITER ;
```

Call:

``` sql
CALL getEmployeeCount(20, @total);
```

Read the output:

``` sql
SELECT @total;
```

## Flow

``` text
IN

Caller ───────→ Procedure


OUT

Caller ←─────── Procedure
```

### Important

`@total` is a MySQL **user-defined session variable**.

------------------------------------------------------------------------

# 9. INOUT Parameters

`INOUT` means:

> The procedure receives a value and can modify that value before
> returning it.

Example:

``` sql
DELIMITER //

CREATE PROCEDURE increaseSalary(
    INOUT salary INT
)
BEGIN
    SET salary = salary + 1000;
END //

DELIMITER ;
```

Call:

``` sql
SET @salary = 5000;

CALL increaseSalary(@salary);

SELECT @salary;
```

Result:

``` text
6000
```

## Parameter summary

  Type      Meaning          Data flow
  --------- ---------------- --------------------
  `IN`      Input            Caller → Procedure
  `OUT`     Output           Procedure → Caller
  `INOUT`   Input + Output   Caller ↔ Procedure

### Memory trick

``` text
IN     → Input
OUT    → Output
INOUT  → Input + Output
```

------------------------------------------------------------------------

# 10. Local Variables and DECLARE

A procedure can have local variables.

Syntax:

``` sql
DECLARE variable_name datatype;
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE employeeDetails(IN employee_id INT)
BEGIN
    DECLARE employee_salary DECIMAL(10,2);

    SELECT sal
    INTO employee_salary
    FROM emp
    WHERE empno = employee_id;

    SELECT employee_salary;
END //

DELIMITER ;
```

### Important rule

`DECLARE` statements must appear at the beginning of their
`BEGIN ... END` block, before executable statements.

------------------------------------------------------------------------

# 11. SET and SELECT INTO

## SET

Use `SET` to assign a value.

``` sql
SET total_salary = 5000;
```

Example:

``` sql
DECLARE total_salary DECIMAL(10,2);

SET total_salary = 5000;
```

## SELECT ... INTO

Use `SELECT ... INTO` to place a query result into a variable.

``` sql
SELECT sal
INTO employee_salary
FROM emp
WHERE empno = 7839;
```

### Mental model

``` text
SELECT ... INTO
        ↓
Database result
        ↓
Variable
```

------------------------------------------------------------------------

# 12. IF / ELSEIF / ELSE

Stored procedures support conditional logic.

Syntax:

``` sql
IF condition THEN

    statements;

ELSEIF another_condition THEN

    statements;

ELSE

    statements;

END IF;
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE checkSalary(IN employee_salary INT)
BEGIN

    IF employee_salary >= 3000 THEN
        SELECT 'High Salary';

    ELSEIF employee_salary >= 2000 THEN
        SELECT 'Medium Salary';

    ELSE
        SELECT 'Normal Salary';

    END IF;

END //

DELIMITER ;
```

Call:

``` sql
CALL checkSalary(3500);
```

Result:

``` text
High Salary
```

------------------------------------------------------------------------

# 13. CASE

`CASE` is useful when there are multiple possible conditions.

Example:

``` sql
DELIMITER //

CREATE PROCEDURE salaryCategory(IN employee_salary INT)
BEGIN

    SELECT
        CASE
            WHEN employee_salary >= 3000 THEN 'HIGH'
            WHEN employee_salary >= 2000 THEN 'MEDIUM'
            ELSE 'LOW'
        END AS category;

END //

DELIMITER ;
```

Call:

``` sql
CALL salaryCategory(2500);
```

Result:

``` text
MEDIUM
```

------------------------------------------------------------------------

# 14. Loops

Stored procedures can execute statements repeatedly.

Common loop constructs:

``` text
WHILE
REPEAT
LOOP
```

These are useful for procedural tasks, although set-based SQL is often
preferable for operations that can be expressed as a single query.

------------------------------------------------------------------------

# 15. WHILE Loop

Syntax:

``` sql
WHILE condition DO

    statements;

END WHILE;
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE printNumbers()
BEGIN
    DECLARE counter INT DEFAULT 1;

    WHILE counter <= 5 DO
        SELECT counter;
        SET counter = counter + 1;
    END WHILE;

END //

DELIMITER ;
```

Call:

``` sql
CALL printNumbers();
```

------------------------------------------------------------------------

# 16. REPEAT Loop

`REPEAT` executes the body and then checks the condition.

Syntax:

``` sql
REPEAT

    statements;

UNTIL condition
END REPEAT;
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE printNumbers()
BEGIN
    DECLARE counter INT DEFAULT 1;

    REPEAT
        SELECT counter;
        SET counter = counter + 1;
    UNTIL counter > 5
    END REPEAT;

END //

DELIMITER ;
```

### Important difference

``` text
WHILE
→ checks condition before execution

REPEAT
→ executes first, checks condition afterward
```

------------------------------------------------------------------------

# 17. LOOP and LEAVE

`LOOP` creates a loop that can be exited using `LEAVE`.

Example:

``` sql
DELIMITER //

CREATE PROCEDURE printNumbers()
BEGIN
    DECLARE counter INT DEFAULT 1;

    number_loop: LOOP

        SELECT counter;

        SET counter = counter + 1;

        IF counter > 5 THEN
            LEAVE number_loop;
        END IF;

    END LOOP number_loop;

END //

DELIMITER ;
```

### Key terms

``` text
LOOP
→ creates loop

LEAVE
→ exits loop

label
→ identifies the loop
```

------------------------------------------------------------------------

# 18. Parameters + Conditions

Procedures become powerful when parameters and conditions work together.

Example:

``` sql
DELIMITER //

CREATE PROCEDURE employeeStatus(
    IN employee_id INT
)
BEGIN
    DECLARE employee_salary DECIMAL(10,2);

    SELECT sal
    INTO employee_salary
    FROM emp
    WHERE empno = employee_id;

    IF employee_salary >= 3000 THEN
        SELECT 'High Salary';
    ELSE
        SELECT 'Normal Salary';
    END IF;

END //

DELIMITER ;
```

Call:

``` sql
CALL employeeStatus(7839);
```

------------------------------------------------------------------------

# 19. INSERT / UPDATE / DELETE Procedures

## INSERT

``` sql
DELIMITER //

CREATE PROCEDURE addEmployee(
    IN employee_id INT,
    IN employee_name VARCHAR(20),
    IN employee_job VARCHAR(20),
    IN employee_salary DECIMAL(10,2),
    IN employee_dept INT
)
BEGIN

    INSERT INTO emp(empno, ename, job, sal, deptno)
    VALUES (
        employee_id,
        employee_name,
        employee_job,
        employee_salary,
        employee_dept
    );

END //

DELIMITER ;
```

Call:

``` sql
CALL addEmployee(
    8000,
    'RAHUL',
    'CLERK',
    1500,
    20
);
```

## UPDATE

``` sql
DELIMITER //

CREATE PROCEDURE updateEmployeeSalary(
    IN employee_id INT,
    IN new_salary DECIMAL(10,2)
)
BEGIN

    UPDATE emp
    SET sal = new_salary
    WHERE empno = employee_id;

END //

DELIMITER ;
```

Call:

``` sql
CALL updateEmployeeSalary(8000, 2000);
```

## DELETE

``` sql
DELIMITER //

CREATE PROCEDURE deleteEmployee(
    IN employee_id INT
)
BEGIN

    DELETE FROM emp
    WHERE empno = employee_id;

END //

DELIMITER ;
```

Call:

``` sql
CALL deleteEmployee(8000);
```

------------------------------------------------------------------------

# 20. Transactions

Procedures can contain transaction logic.

Common commands:

``` sql
START TRANSACTION;
COMMIT;
ROLLBACK;
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE transferMoney(
    IN from_account INT,
    IN to_account INT,
    IN amount DECIMAL(10,2)
)
BEGIN

    START TRANSACTION;

    UPDATE accounts
    SET balance = balance - amount
    WHERE account_id = from_account;

    UPDATE accounts
    SET balance = balance + amount
    WHERE account_id = to_account;

    COMMIT;

END //

DELIMITER ;
```

### Real-world analogy

Bank transfer:

``` text
Account A: -1000
Account B: +1000
```

Both operations should succeed together.

If something fails, the transaction can be rolled back.

> Transaction design must also consider validation, errors, isolation,
> locking, and storage-engine behavior. Do not blindly `COMMIT` without
> thinking about failure cases.

------------------------------------------------------------------------

# 21. Error Handling and HANDLER

MySQL provides handlers for conditions such as SQL errors and
`NOT FOUND`.

General pattern:

``` sql
DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
BEGIN
    -- error handling
END;
```

Example:

``` sql
DELIMITER //

CREATE PROCEDURE safeOperation()
BEGIN

    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        SELECT 'Operation failed' AS message;
    END;

    START TRANSACTION;

    -- database operations

    COMMIT;

END //

DELIMITER ;
```

### Handler types

Common choices:

``` text
CONTINUE
→ handle condition and continue

EXIT
→ handle condition and leave the current block
```

------------------------------------------------------------------------

# 22. Cursors

A **cursor** allows a procedure to process query results one row at a
time.

Typical cursor flow:

``` text
DECLARE cursor
      ↓
DECLARE NOT FOUND handler
      ↓
OPEN cursor
      ↓
FETCH row
      ↓
Process row
      ↓
Repeat
      ↓
CLOSE cursor
```

Example structure:

``` sql
DELIMITER //

CREATE PROCEDURE processEmployees()
BEGIN

    DECLARE done INT DEFAULT 0;
    DECLARE employee_name VARCHAR(20);

    DECLARE employee_cursor CURSOR FOR
        SELECT ename FROM emp;

    DECLARE CONTINUE HANDLER FOR NOT FOUND
        SET done = 1;

    OPEN employee_cursor;

    read_loop: LOOP

        FETCH employee_cursor INTO employee_name;

        IF done = 1 THEN
            LEAVE read_loop;
        END IF;

        SELECT employee_name;

    END LOOP;

    CLOSE employee_cursor;

END //

DELIMITER ;
```

### Important

Cursors are powerful, but they process rows individually.

Whenever possible, prefer a **set-based SQL statement** when the same
result can be achieved without a cursor.

------------------------------------------------------------------------

# 23. Nested Blocks

A procedure can contain nested `BEGIN ... END` blocks.

Example:

``` sql
DELIMITER //

CREATE PROCEDURE example()
main_block: BEGIN

    DECLARE x INT DEFAULT 10;

    inner_block: BEGIN
        DECLARE y INT DEFAULT 20;

        SELECT x, y;
    END;

END //

DELIMITER ;
```

Variables declared in an inner block are generally local to that block.

------------------------------------------------------------------------

# 24. Calling One Procedure from Another

A procedure can call another procedure using `CALL`.

Example:

``` sql
DELIMITER //

CREATE PROCEDURE procedureA()
BEGIN
    SELECT 'Procedure A';
END //

DELIMITER ;
```

Another procedure:

``` sql
DELIMITER //

CREATE PROCEDURE procedureB()
BEGIN
    CALL procedureA();
    SELECT 'Procedure B';
END //

DELIMITER ;
```

Call:

``` sql
CALL procedureB();
```

Output:

``` text
Procedure A
Procedure B
```

This can help organize larger database logic.

------------------------------------------------------------------------

# 25. Dynamic SQL

Sometimes the SQL statement itself needs to be constructed dynamically.

MySQL supports prepared statements such as:

``` sql
SET @sql = 'SELECT * FROM emp WHERE deptno = ?';

PREPARE stmt FROM @sql;

SET @dept = 20;

EXECUTE stmt USING @dept;

DEALLOCATE PREPARE stmt;
```

### Important

Dynamic SQL should be used carefully.

Avoid building SQL by blindly concatenating untrusted user input.

Prefer parameter binding where supported.

------------------------------------------------------------------------

# 26. Security and Permissions

Stored procedures can be useful for controlled database access.

For example, instead of giving an application direct permission to
update a sensitive table, an organization may expose a procedure that
performs a controlled operation.

Example idea:

``` text
Application
     ↓
CALL updateEmployeeSalary(...)
     ↓
Stored Procedure
     ↓
EMP table
```

Permissions can be managed with MySQL privileges such as:

``` sql
GRANT
REVOKE
```

### Important security principle

> A stored procedure is not automatically secure. Security still depends
> on privileges, validation, SQL design, and how input is handled.

------------------------------------------------------------------------

# 27. Managing Procedures

## Show procedures

``` sql
SHOW PROCEDURE STATUS;
```

For the current database:

``` sql
SHOW PROCEDURE STATUS
WHERE Db = DATABASE();
```

## Show procedure definition

``` sql
SHOW CREATE PROCEDURE getEmployees;
```

## Delete procedure

``` sql
DROP PROCEDURE getEmployees;
```

Safer:

``` sql
DROP PROCEDURE IF EXISTS getEmployees;
```

------------------------------------------------------------------------

# 28. Stored Procedure vs Function

This is a common interview question.

  -----------------------------------------------------------------------
  Feature                 Procedure               Function
  ----------------------- ----------------------- -----------------------
  Called using            `CALL`                  Usually used in an
                                                  expression

  Parameters              `IN`, `OUT`, `INOUT`    Function parameters are
                                                  input parameters

  Return                  Can return result sets  Returns a single value
                          and OUT values          

  Can contain multiple    Yes                     Yes, subject to
  SQL statements                                  function restrictions

  Typical use             Operations / workflows  Calculate and return a
                                                  value
  -----------------------------------------------------------------------

### Procedure

``` sql
CALL getEmployees();
```

### Function

``` sql
SELECT calculateBonus(5000);
```

### Easy memory

``` text
Procedure → perform an operation
Function  → calculate/return a value
```

> MySQL functions have additional restrictions compared with procedures,
> especially around side effects and statements that modify data.

------------------------------------------------------------------------

# 29. Advantages and Disadvantages

## ✅ Advantages

### 1. Reusability

Write logic once:

``` sql
CREATE PROCEDURE ...
```

Use it many times:

``` sql
CALL ...
```

### 2. Encapsulation

Complex SQL logic can be grouped inside the database.

### 3. Centralized logic

Multiple applications can use the same database operation.

### 4. Security

Permissions can be designed around controlled database operations.

### 5. Reduced repeated SQL

Application code can call a procedure instead of repeatedly sending
complex SQL.

------------------------------------------------------------------------

## ❌ Disadvantages

### 1. Database-specific syntax

Procedure code can be strongly tied to MySQL.

### 2. Maintenance complexity

Very large procedures can become difficult to maintain.

### 3. Testing can be harder

Database-side procedural logic requires database-focused testing.

### 4. Logic can become tightly coupled to the database

Moving to another database system may require rewriting procedures.

### 5. Performance is not automatically better

A procedure is not a magic performance optimization.

------------------------------------------------------------------------

# 30. Production-Level Guidelines

## 1. Keep procedures focused

Prefer:

``` text
getEmployeeById
updateEmployeeSalary
createOrder
```

over one huge procedure that performs unrelated operations.

## 2. Use meaningful names

Good:

``` text
getEmployeesByDept
updateEmployeeSalary
createOrder
```

Avoid:

``` text
p1
test123
abc
```

## 3. Validate inputs

Example:

``` sql
IF amount <= 0 THEN
    SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Amount must be greater than zero';
END IF;
```

## 4. Handle errors

Use appropriate handlers for operations that require robust failure
handling.

## 5. Use transactions carefully

For multi-step operations where atomicity is required:

``` text
START TRANSACTION
      ↓
Operations
      ↓
COMMIT / ROLLBACK
```

## 6. Prefer set-based SQL

Instead of processing thousands of rows one at a time with a cursor,
first ask:

> Can this be solved with one `UPDATE`, `INSERT ... SELECT`, `DELETE`,
> or other set-based query?

## 7. Index appropriately

Stored procedures still depend on indexes and query plans.

Use:

``` sql
EXPLAIN
```

to inspect important queries.

------------------------------------------------------------------------

# 31. Common Mistakes

## Mistake 1 --- Forgetting DELIMITER

Incorrect:

``` sql
CREATE PROCEDURE test()
BEGIN
    SELECT * FROM emp;
END;
```

In MySQL Workbench, use:

``` sql
DELIMITER //

CREATE PROCEDURE test()
BEGIN
    SELECT * FROM emp;
END //

DELIMITER ;
```

------------------------------------------------------------------------

## Mistake 2 --- Forgetting `CALL`

Incorrect:

``` sql
getEmployees();
```

Correct:

``` sql
CALL getEmployees();
```

------------------------------------------------------------------------

## Mistake 3 --- Forgetting `BEGIN ... END`

For a multi-statement procedure:

``` sql
CREATE PROCEDURE test()
BEGIN
    ...
END
```

------------------------------------------------------------------------

## Mistake 4 --- Incorrect variable declaration position

Usually:

``` sql
BEGIN

    DECLARE x INT;

    SELECT ...;

END
```

Not:

``` sql
BEGIN

    SELECT ...;

    DECLARE x INT;

END
```

------------------------------------------------------------------------

## Mistake 5 --- Confusing IN and OUT

Remember:

``` text
IN     → send data in
OUT    → receive data out
INOUT  → send + receive
```

------------------------------------------------------------------------

## Mistake 6 --- Using `COUNT(*)` carelessly with outer joins

For example, when counting matching employees in a department-preserving
outer join, understand the difference between:

``` sql
COUNT(*)
```

and:

``` sql
COUNT(e.empno)
```

This is especially important when unmatched rows are represented by
`NULL`.

------------------------------------------------------------------------

# 32. Interview Questions

## Beginner

### Q1. What is a stored procedure?

> A stored procedure is a group of SQL statements stored in the database
> that can be executed by calling its name.

### Q2. How do you execute a stored procedure?

``` sql
CALL procedure_name();
```

### Q3. Why is DELIMITER used?

> It allows the MySQL client to distinguish the end of the complete
> procedure definition from the `;` terminators used by statements
> inside the procedure.

### Q4. What are procedure parameters?

``` text
IN
OUT
INOUT
```

------------------------------------------------------------------------

## Intermediate

### Q5. Difference between IN and OUT?

``` text
IN  → input to procedure
OUT → output from procedure
```

### Q6. What is INOUT?

> A parameter that can receive an input value and return a modified
> value.

### Q7. What is DECLARE?

> `DECLARE` is used to define local variables, cursors, and handlers
> inside a stored-program block.

### Q8. Can a procedure contain INSERT, UPDATE and DELETE?

Yes.

### Q9. Can a procedure contain IF and loops?

Yes.

### Q10. Can one procedure call another procedure?

Yes, using:

``` sql
CALL procedure_name();
```

------------------------------------------------------------------------

## Advanced

### Q11. What is a cursor?

> A cursor allows a stored program to process rows from a result set
> individually.

### Q12. What is a handler?

> A handler defines what MySQL should do when a specified condition
> occurs during stored-program execution.

### Q13. Why use transactions inside procedures?

> To make related database operations succeed or fail as a unit when
> atomicity is required.

### Q14. Are stored procedures always faster?

**No.**

Performance depends on the SQL statements, indexes, execution plans,
data volume, network overhead, and overall architecture.

### Q15. Procedure vs Function?

> A procedure is generally used to perform database operations and can
> return result sets or OUT values, while a function returns a value and
> is commonly used inside SQL expressions.

------------------------------------------------------------------------

# 33. Quick Revision Sheet

``` text
╔════════════════════════════════════════════╗
║       MYSQL STORED PROCEDURE CHEAT SHEET   ║
╚════════════════════════════════════════════╝

CREATE
----------------------------------------------
DELIMITER //

CREATE PROCEDURE name()
BEGIN
    SQL;
END //

DELIMITER ;


CALL
----------------------------------------------
CALL name();


PARAMETERS
----------------------------------------------
IN      → input
OUT     → output
INOUT   → input + output


VARIABLE
----------------------------------------------
DECLARE x INT;


ASSIGN
----------------------------------------------
SET x = 10;


QUERY INTO VARIABLE
----------------------------------------------
SELECT sal
INTO x
FROM emp
WHERE empno = 7839;


CONDITION
----------------------------------------------
IF condition THEN
    ...
ELSE
    ...
END IF;


LOOPS
----------------------------------------------
WHILE
REPEAT
LOOP + LEAVE


TRANSACTION
----------------------------------------------
START TRANSACTION;
COMMIT;
ROLLBACK;


ERROR HANDLER
----------------------------------------------
DECLARE EXIT HANDLER FOR SQLEXCEPTION
BEGIN
    ...
END;


CURSOR
----------------------------------------------
DECLARE cursor
OPEN
FETCH
CLOSE


MANAGEMENT
----------------------------------------------
SHOW PROCEDURE STATUS;

SHOW CREATE PROCEDURE name;

DROP PROCEDURE IF EXISTS name;
```

------------------------------------------------------------------------

# 34. Practice Roadmap

We will **not jump directly into advanced procedures**.

We will learn by writing code.

## 🟢 Level 1 --- Beginner

1.  Create a simple procedure
2.  Call a procedure
3.  Understand `DELIMITER`
4.  Procedure without parameters
5.  Procedure with `IN`
6.  Multiple `IN` parameters
7.  Procedure with `SELECT`
8.  Procedure with `WHERE`

### Goal

You should be able to create and call basic reusable database operations
without looking at notes.

------------------------------------------------------------------------

## 🟡 Level 2 --- Parameters & Variables

9.  `OUT`
10. `INOUT`
11. User variables
12. `DECLARE`
13. `SET`
14. `SELECT INTO`
15. Multiple local variables

### Goal

You should understand data flow:

``` text
Caller → Procedure → Caller
```

------------------------------------------------------------------------

## 🟠 Level 3 --- Decision Making

16. `IF`
17. `ELSEIF`
18. `ELSE`
19. `CASE`
20. Nested conditions
21. Validation
22. `SIGNAL`

### Goal

Build procedures containing real business rules.

------------------------------------------------------------------------

## 🔵 Level 4 --- CRUD Procedures

23. INSERT procedure
24. UPDATE procedure
25. DELETE procedure
26. Search procedure
27. Pagination procedure
28. Procedures with JOINs
29. Procedures with GROUP BY
30. Procedures with HAVING

### Goal

Build realistic backend/database operations.

------------------------------------------------------------------------

## 🟣 Level 5 --- Loops

31. WHILE
32. REPEAT
33. LOOP
34. LEAVE
35. ITERATE
36. Labels
37. Nested loops

### Goal

Understand procedural iteration.

------------------------------------------------------------------------

## 🔴 Level 6 --- Transactions & Error Handling

38. Transactions
39. COMMIT
40. ROLLBACK
41. Handlers
42. `SQLEXCEPTION`
43. `NOT FOUND`
44. `CONTINUE`
45. `EXIT`
46. Validation + transaction + handler

### Goal

Build safe multi-step database operations.

------------------------------------------------------------------------

## ⚫ Level 7 --- Advanced

47. Cursors
48. Cursor + handler
49. Cursor + loop
50. Nested blocks
51. Calling procedures from procedures
52. Dynamic SQL
53. Prepared statements
54. Security and privileges
55. Production-level procedure design

### Goal

Become comfortable reading and writing advanced stored-program logic.

------------------------------------------------------------------------

# 🧠 Final Mental Model

When you see a Stored Procedure question, think:

``` text
                    STORED PROCEDURE
                           │
          ┌────────────────┼────────────────┐
          ↓                ↓                ↓
      Parameters        Variables        SQL Logic
      IN/OUT/INOUT      DECLARE          SELECT
                                         INSERT
                                         UPDATE
                                         DELETE
          │                │                │
          └────────────────┼────────────────┘
                           ↓
                     Conditions
                     IF / CASE
                           ↓
                        Loops
                 WHILE / REPEAT / LOOP
                           ↓
                  Error Handling
                      HANDLER
                           ↓
                     Transactions
                  COMMIT / ROLLBACK
                           ↓
                       Cursors
```

## 🔥 Golden Rule

> **First understand what data comes in, what operation the procedure
> performs, and what data needs to come out. Then choose parameters,
> variables, conditions, loops, transactions, or cursors only when they
> are actually needed.**

------------------------------------------------------------------------

# 🎯 Practice Strategy

For every practice problem, follow this order:

``` text
1. Understand the requirement
        ↓
2. Identify input
        ↓
3. Identify output
        ↓
4. Write the SQL first
        ↓
5. Convert it into a procedure
        ↓
6. Add parameters
        ↓
7. Add conditions if required
        ↓
8. Test with CALL
        ↓
9. Check edge cases
```

This way, you learn **how to think**, rather than memorizing procedure
syntax.
