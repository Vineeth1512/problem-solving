# 🔗 MySQL JOINs — Complete Notes

> **Simple, practical, interview-friendly JOIN notes**

---

# 📌 1. What is a JOIN?

> **A JOIN is used to combine data from two or more tables based on a related column.**

### Real-Life Analogy 🏢

Imagine you have two registers:

**EMPLOYEE register**

| empno | ename | deptno |
|---:|---|---:|
| 7369 | SMITH | 20 |
| 7499 | ALLEN | 30 |

**DEPARTMENT register**

| deptno | dname |
|---:|---|
| 10 | ACCOUNTING |
| 20 | RESEARCH |
| 30 | SALES |

The common column is:

```text
EMP.deptno
      ↓
DEPT.deptno
```

A JOIN uses this relationship to combine the information.

---

# 🧠 2. Basic JOIN Syntax

```sql
SELECT columns
FROM table1 t1
JOIN table2 t2
ON t1.column = t2.column;
```

Example:

```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d
ON e.deptno = d.deptno;
```

### Think like this:

```text
EMP
 ↓ deptno
DEPT
```

---

# ⭐ 3. Main JOIN Types

The important JOIN concepts are:

1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
4. FULL OUTER JOIN
5. CROSS JOIN
6. SELF JOIN

> **Note:** SELF JOIN is a technique where a table is joined with itself. Many courses list the four relational JOIN types plus CROSS JOIN and SELF JOIN separately.

---

# 🟢 4. INNER JOIN

### Definition

> **An INNER JOIN returns only the records that have matching values in both tables.**

### Simple idea

```text
Table A       Table B

   A ∩ B

Only matching records
```

### Example

```sql
SELECT e.ename, d.dname
FROM emp e
INNER JOIN dept d
ON e.deptno = d.deptno;
```

### When should I use it?

Use INNER JOIN when the question does **not** ask for unmatched records.

### Keyword clue

```text
"matching records"
"employees with departments"
"departments having employees"
```

---

# 🟡 5. LEFT JOIN

### Definition

> **A LEFT JOIN returns all records from the left table and matching records from the right table. If there is no match, NULL is returned for the right-table columns.**

### Simple idea

```text
ALL LEFT
   +
matching RIGHT
```

### Example

```sql
SELECT d.dname, e.ename
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno;
```

This keeps **every department**, even if it has no employees.

### How do I identify the LEFT table?

Ask:

> **Which table's ALL records must be preserved?**

If the answer is DEPT:

```sql
FROM dept d
LEFT JOIN emp e
```

### Important memory rule

> **The table you want to protect goes on the LEFT.**

---

# 🔵 6. RIGHT JOIN

### Definition

> **A RIGHT JOIN returns all records from the right table and matching records from the left table. If there is no match, NULL is returned for the left-table columns.**

### Example

```sql
SELECT d.dname, e.ename
FROM emp e
RIGHT JOIN dept d
ON e.deptno = d.deptno;
```

Here DEPT is on the right, so all departments are preserved.

### Easy memory

```text
LEFT JOIN
→ protect LEFT table

RIGHT JOIN
→ protect RIGHT table
```

### LEFT and RIGHT are reversible

These are logically equivalent:

```sql
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno;
```

and:

```sql
FROM emp e
RIGHT JOIN dept d
ON e.deptno = d.deptno;
```

---

# 🟣 7. FULL OUTER JOIN

### Definition

> **A FULL OUTER JOIN returns all records from both tables, including matching and unmatched records from both sides.**

Conceptually:

```text
ALL LEFT
   +
ALL RIGHT
   +
matching records
```

### Important MySQL Point ⚠️

MySQL does not directly support:

```sql
FULL OUTER JOIN
```

A common approach is to combine LEFT JOIN and RIGHT JOIN with `UNION`.

```sql
SELECT e.ename, d.dname
FROM emp e
LEFT JOIN dept d
ON e.deptno = d.deptno

UNION

SELECT e.ename, d.dname
FROM emp e
RIGHT JOIN dept d
ON e.deptno = d.deptno;
```

### Memory

```text
LEFT  → all left
RIGHT → all right
FULL  → all both
```

---

# 🟠 8. CROSS JOIN

### Definition

> **A CROSS JOIN combines every row of the first table with every row of the second table.**

This creates a **Cartesian product**.

### Example

```sql
SELECT e.ename, d.dname
FROM emp e
CROSS JOIN dept d;
```

If:

```text
EMP  = 14 rows
DEPT = 4 rows
```

Then:

```text
14 × 4 = 56 rows
```

### Simple analogy

If you have:

```text
3 shirts
2 pants
```

Every shirt can combine with every pair of pants:

```text
3 × 2 = 6 combinations
```

### Important

CROSS JOIN normally does not need an `ON` condition.

---

# 🔴 9. SELF JOIN

### Definition

> **Joining a table with itself is known as a SELF JOIN.**

It is used when records in the same table have a relationship with each other.

### Real Example

Our `emp` table contains:

```text
empno
ename
mgr
```

The `mgr` column contains the employee number of the manager.

So the same `emp` table represents both:

```text
Employee
Manager
```

### Query

```sql
SELECT e.ename AS employee,
       m.ename AS manager
FROM emp e
JOIN emp m
ON e.mgr = m.empno;
```

Here:

```text
e → Employee
m → Manager
```

### Most important relationship

```sql
ON e.mgr = m.empno
```

Think:

```text
Employee's manager ID
          ↓
Manager's employee ID
```

---

# 🧠 10. How to Choose the JOIN from a Question

Don't memorize JOIN names from the question.

Ask:

> **What records must be preserved?**

---

## Case 1 — Only matching records

Question:

> Show employees and their departments.

No unmatched records are requested.

➡️ **INNER JOIN**

---

## Case 2 — All employees

Question:

> Show all employees, including employees without a department.

Which table must be preserved?

```text
EMP
```

Use:

```sql
FROM emp e
LEFT JOIN dept d
ON e.deptno = d.deptno;
```

---

## Case 3 — All departments

Question:

> Show all departments, including departments with no employees.

Which table must be preserved?

```text
DEPT
```

Use:

```sql
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno;
```

Or:

```sql
FROM emp e
RIGHT JOIN dept d
ON e.deptno = d.deptno;
```

---

## Case 4 — All records from both

Question:

> Show all employees and all departments, including unmatched records from both tables.

➡️ **FULL OUTER JOIN concept**

In MySQL, use the appropriate `UNION` approach.

---

## Case 5 — Every possible combination

Question:

> Show every possible employee-department combination.

➡️ **CROSS JOIN**

---

## Case 6 — Same table relationship

Question:

> Show employee and manager.

Both are in `emp`.

➡️ **SELF JOIN**

---

# ⭐ 11. The Most Important JOIN Question

When reading a question, ask:

> **"Which table's records should NOT disappear?"**

### Example

> All departments, including departments with zero employees.

Answer:

```text
DEPT should NOT disappear.
```

Therefore:

```sql
FROM dept d
LEFT JOIN emp e
```

### Another example

> All employees, including employees without departments.

Answer:

```text
EMP should NOT disappear.
```

Therefore:

```sql
FROM emp e
LEFT JOIN dept d
```

---

# 🔥 12. JOIN + WHERE

`ON` establishes the relationship.

`WHERE` filters the result.

Example:

```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d
ON e.deptno = d.deptno
WHERE d.loc = 'DALLAS';
```

### Remember

```text
ON
↓
How are the tables connected?

WHERE
↓
Which rows do I want?
```

---

# 🧮 13. JOIN + GROUP BY

Question:

> Show department name and number of employees in each department.

```sql
SELECT d.dname,
       COUNT(e.empno) AS employee_count
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.deptno, d.dname;
```

### Thinking

```text
"number of employees"
        ↓
COUNT()

"each department"
        ↓
GROUP BY
```

---

# 🎯 14. COUNT(*) vs COUNT(column) with LEFT JOIN

This is extremely important.

Consider:

```sql
SELECT d.dname, COUNT(*)
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.deptno, d.dname;
```

For a department with zero employees, LEFT JOIN still creates a row containing NULL employee values.

So:

```sql
COUNT(*)
```

can count that generated row.

### Better:

```sql
COUNT(e.empno)
```

Because `COUNT(column)` ignores NULL.

Therefore:

```sql
SELECT d.dname,
       COUNT(e.empno) AS employee_count
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.deptno, d.dname;
```

A department with no employees gets:

```text
0
```

---

# 🟢 15. JOIN + SUM

Question:

> Show department name and total salary.

```sql
SELECT d.dname,
       SUM(e.sal) AS total_salary
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.deptno, d.dname;
```

---

# 🔵 16. JOIN + AVG

```sql
SELECT d.dname,
       AVG(e.sal) AS average_salary
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.deptno, d.dname;
```

---

# 🟣 17. JOIN + HAVING

Question:

> Show departments having more than 3 employees.

```sql
SELECT d.dname,
       COUNT(e.empno) AS employee_count
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.deptno, d.dname
HAVING COUNT(e.empno) > 3;
```

### Remember

```text
WHERE  → filters rows
HAVING → filters groups
```

---

# 🧠 18. Conditional Aggregation with JOIN

Question:

> Show departments where at least 2 employees earn more than 2000.

Use:

```sql
HAVING SUM(e.sal > 2000) >= 2
```

Complete:

```sql
SELECT d.dname,
       COUNT(e.empno) AS employee_count
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
GROUP BY d.deptno, d.dname
HAVING SUM(e.sal > 2000) >= 2;
```

### Why?

In MySQL:

```text
e.sal > 2000
```

becomes:

```text
TRUE  → 1
FALSE → 0
```

So:

```sql
SUM(e.sal > 2000)
```

counts employees earning more than 2000.

---

# 🔗 19. Three-Table JOIN

Suppose we have:

```text
EMP
 ↓ deptno
DEPT
 ↓ loc_id
LOCATION
```

The JOIN chain is:

```text
EMP → DEPT → LOCATION
```

### General syntax

```sql
SELECT columns
FROM table1 t1
JOIN table2 t2
ON t1.column = t2.column
JOIN table3 t3
ON t2.column = t3.column;
```

### Example

```sql
SELECT e.ename,
       d.dname,
       l.city
FROM emp e
JOIN dept d
ON e.deptno = d.deptno
JOIN location l
ON d.loc_id = l.loc_id;
```

---

# 🧠 20. How to Think About 3-Table JOINs

Don't start by writing JOIN.

### Step 1 — Find the requested columns

Example:

```text
ENAME → EMP
DNAME → DEPT
CITY  → LOCATION
```

### Step 2 — Find the tables

```text
EMP + DEPT + LOCATION
```

### Step 3 — Find relationships

```text
EMP.deptno = DEPT.deptno

DEPT.loc_id = LOCATION.loc_id
```

### Step 4 — Build the chain

```text
EMP
 ↓
DEPT
 ↓
LOCATION
```

### Step 5 — Add conditions

```text
WHERE
GROUP BY
HAVING
ORDER BY
```

---

# 🧩 21. Bridge / Intermediate Table

Sometimes two tables don't have a direct relationship.

Example:

```text
EMP ❌ LOCATION
```

But:

```text
EMP → DEPT → LOCATION
```

`DEPT` acts as the **bridge/intermediate table**.

Even if you don't select anything from DEPT, you may need it to connect the other tables.

Example:

```sql
SELECT e.ename, l.city
FROM emp e
JOIN dept d
ON e.deptno = d.deptno
JOIN location l
ON d.loc_id = l.loc_id;
```

---

# 🏆 22. JOIN Clause Order

A common structure is:

```sql
SELECT ...
FROM ...
JOIN ...
ON ...
JOIN ...
ON ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...;
```

Example:

```sql
SELECT d.dname,
       AVG(e.sal) AS avg_salary
FROM emp e
JOIN dept d
ON e.deptno = d.deptno
JOIN location l
ON d.loc_id = l.loc_id
WHERE l.city = 'DALLAS'
GROUP BY d.deptno, d.dname
HAVING AVG(e.sal) > 2000
ORDER BY avg_salary DESC;
```

---

# ⚡ 23. ON vs WHERE

This is a very common interview question.

### ON

> Defines how tables are related.

```sql
ON e.deptno = d.deptno
```

### WHERE

> Filters rows after the JOIN result is formed.

```sql
WHERE d.loc = 'DALLAS'
```

### Easy memory

```text
ON    → CONNECT
WHERE → FILTER
```

---

# ⚡ 24. WHERE vs HAVING

### WHERE

Filters individual rows:

```sql
WHERE e.sal > 2000
```

### HAVING

Filters groups:

```sql
HAVING AVG(e.sal) > 2000
```

### Easy memory

```text
WHERE
↓
Rows

HAVING
↓
Groups
```

---

# 📊 25. JOIN Comparison

| JOIN | What it returns |
|---|---|
| INNER JOIN | Matching records only |
| LEFT JOIN | All left + matching right |
| RIGHT JOIN | All right + matching left |
| FULL OUTER JOIN | All records from both sides |
| CROSS JOIN | Every possible combination |
| SELF JOIN | Same table joined with itself |

---

# 🧠 26. JOIN Decision Tree

```text
                 What does the question require?
                           |
             ┌─────────────┴─────────────┐
             ↓                           ↓
       Only matching                Unmatched?
             ↓                           ↓
       INNER JOIN             Which records must stay?
                                         |
                          ┌──────────────┴──────────────┐
                          ↓                             ↓
                     All LEFT                      All RIGHT
                          ↓                             ↓
                     LEFT JOIN                    RIGHT JOIN
```

Additional cases:

```text
All records from BOTH
        ↓
FULL OUTER JOIN concept

Every possible combination
        ↓
CROSS JOIN

Same table relationship
        ↓
SELF JOIN
```

---

# 🧪 27. Common JOIN Interview Questions

### Question 1

> WAQTD employee name and department name.

Think:

```text
EMP + DEPT
Matching records
→ INNER JOIN
```

---

### Question 2

> WAQTD all departments including departments with zero employees.

Think:

```text
DEPT must be preserved
→ LEFT JOIN
```

```sql
FROM dept d
LEFT JOIN emp e
ON d.deptno = e.deptno
```

---

### Question 3

> WAQTD all employees including employees without departments.

Think:

```text
EMP must be preserved
→ LEFT JOIN
```

```sql
FROM emp e
LEFT JOIN dept d
ON e.deptno = d.deptno
```

---

### Question 4

> WAQTD employee and manager name.

Think:

```text
Same table
→ SELF JOIN
```

```sql
FROM emp e
JOIN emp m
ON e.mgr = m.empno
```

---

### Question 5

> WAQTD every possible employee-department combination.

Think:

```text
Every possible combination
→ CROSS JOIN
```

---

# ⭐ 28. Most Important Interview Definitions

### JOIN

> A JOIN is used to combine data from two or more tables based on a related column.

### INNER JOIN

> An INNER JOIN returns only matching records from both tables.

### LEFT JOIN

> A LEFT JOIN returns all records from the left table and matching records from the right table.

### RIGHT JOIN

> A RIGHT JOIN returns all records from the right table and matching records from the left table.

### FULL OUTER JOIN

> A FULL OUTER JOIN returns all records from both tables, including matched and unmatched records.

### CROSS JOIN

> A CROSS JOIN returns every possible combination of rows from two tables.

### SELF JOIN

> Joining a table with itself is known as a SELF JOIN.

---

# 🚀 29. JOIN Problem-Solving Formula

Whenever you see a JOIN question:

```text
QUESTION
   ↓
1. What columns are requested?
   ↓
2. Which tables contain those columns?
   ↓
3. How are those tables related?
   ↓
4. Which records must be preserved?
   ↓
5. Choose JOIN
   ↓
6. Write ON condition
   ↓
7. Need WHERE?
   ↓
8. Need GROUP BY?
   ↓
9. Need HAVING?
   ↓
10. Need ORDER BY?
```

---

# 🎯 30. Golden Rules

```text
1. JOIN → combines tables
2. ON → connects tables
3. WHERE → filters rows
4. GROUP BY → creates groups
5. HAVING → filters groups
6. ORDER BY → sorts results

7. LEFT JOIN → preserve LEFT
8. RIGHT JOIN → preserve RIGHT
9. INNER JOIN → matching only
10. FULL OUTER JOIN → preserve BOTH
11. CROSS JOIN → every combination
12. SELF JOIN → same table with itself

13. With LEFT JOIN, COUNT(right_table.column) is usually safer
    than COUNT(*) when counting matching right-side rows.

14. For 3-table JOINs, find the relationship chain first.
15. Don't memorize JOINs from keywords; identify which records
    the question says must be preserved.
```

# 💡 Final Memory Picture

```text
             SQL JOINs
                 │
     ┌───────────┼───────────┐
     ↓           ↓           ↓
  MATCHING    PRESERVE     SPECIAL
     │           │           │
 INNER JOIN   LEFT/RIGHT   CROSS JOIN
              JOIN         SELF JOIN
                │
                ↓
          FULL OUTER JOIN
```

> **The key to JOINs is not memorizing syntax. Understand the relationship between tables and ask which records the question wants to keep.**
