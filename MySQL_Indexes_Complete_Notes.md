# MySQL Indexes — Complete Notes

## 1. What is an Index?

> An index is a data structure that helps MySQL retrieve rows faster without scanning the entire table.

### Real-Life Analogy

Imagine a book with 1,000 pages.

Without an index:
```text
Start from page 1 → page 2 → page 3 → ... → find the topic
```

With an index:
```text
Topic: Java → Page 450 → Go directly to page 450
```

---

## 2. Why Do We Need Indexes?

The main reason is:

> **To improve query performance.**

Example:

```sql
SELECT *
FROM emp
WHERE ename = 'SMITH';
```

Without an appropriate index, MySQL may need to examine many rows.

With an index:

```text
Query → Index → Find matching value → Retrieve row
```

---

## 3. How Does an Index Work?

MySQL's InnoDB storage engine commonly uses B-tree-style indexes for normal indexes.

Conceptually:

```text
Index
7369
7499
7521
7566
7654
7698
7782
...
```

The index helps MySQL navigate toward the required value instead of checking every table row.

---

# 4. Basic Index Syntax

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

Example:

```sql
CREATE INDEX idx_emp_ename
ON emp(ename);
```

---

# 5. Check Existing Indexes

```sql
SHOW INDEX FROM emp;
```

---

# 6. Remove an Index

```sql
DROP INDEX index_name
ON table_name;
```

Example:

```sql
DROP INDEX idx_emp_ename
ON emp;
```

---

# 7. Types of Indexes in MySQL

Important index types/concepts:

1. Primary Key Index
2. Unique Index
3. Single-Column Index
4. Composite Index
5. FULLTEXT Index
6. SPATIAL Index

Important InnoDB concepts:

- Clustered Index
- Secondary Index

---

# 8. Primary Key Index

When you define a column as `PRIMARY KEY`, MySQL automatically creates an index for the primary key.

```sql
CREATE TABLE employee (
    empno INT PRIMARY KEY,
    ename VARCHAR(20)
);
```

`empno` automatically has a primary-key index.

---

# 9. Unique Index

A unique index prevents duplicate values.

```sql
CREATE UNIQUE INDEX idx_employee_email
ON employee(email);
```

Example:

```text
abc@gmail.com  ✅
xyz@gmail.com  ✅
abc@gmail.com  ❌
```

A unique index provides:

```text
Uniqueness + Efficient lookup
```

---

# 10. Single-Column Index

An index created on one column.

```sql
CREATE INDEX idx_emp_ename
ON emp(ename);
```

Useful when queries frequently search using that column.

```sql
SELECT *
FROM emp
WHERE ename = 'SMITH';
```

---

# 11. Composite Index

> An index created on two or more columns is called a composite index.

```sql
CREATE INDEX idx_emp_dept_job
ON emp(deptno, job);
```

This index contains:

```text
1. deptno
2. job
```

---

# 12. Why Use a Composite Index?

For queries such as:

```sql
SELECT *
FROM emp
WHERE deptno = 20
  AND job = 'CLERK';
```

a composite index can be useful:

```sql
CREATE INDEX idx_emp_dept_job
ON emp(deptno, job);
```

---

# 13. Column Order in Composite Index

Column order matters.

```sql
CREATE INDEX idx_emp_dept_job
ON emp(deptno, job);
```

The order is:

```text
(deptno, job)
   ↑      ↑
 first   second
```

The leftmost-prefix principle means the index is especially useful for:

```sql
WHERE deptno = 20;
```

and:

```sql
WHERE deptno = 20
  AND job = 'CLERK';
```

A query only on:

```sql
WHERE job = 'CLERK';
```

may not be able to use this composite index as effectively because `deptno` is the first indexed column.

### Memory Trick

```text
INDEX(deptno, job)
      ↓
   deptno
      ↓
     job
```

> **The first column is important.**

---

# 14. FULLTEXT Index

A FULLTEXT index is designed for searching text content.

```sql
CREATE FULLTEXT INDEX idx_article_content
ON articles(content);
```

It can be used with:

```sql
MATCH(...)
AGAINST(...)
```

Example:

```sql
SELECT *
FROM articles
WHERE MATCH(content)
AGAINST('MySQL');
```

Useful for articles, documents, descriptions, and large text fields.

---

# 15. SPATIAL Index

A SPATIAL index is used with spatial/geographical data types.

```sql
CREATE SPATIAL INDEX idx_location
ON places(location);
```

Useful for geographic coordinates, maps, locations, and spatial data.

---

# 16. Clustered Index

This is an important InnoDB concept.

In InnoDB, the table's data is organized around the clustered index.

Normally, the `PRIMARY KEY` acts as the clustered index.

```text
Primary Key
     ↓
Clustered Index
     ↓
Actual row data
```

Example:

```sql
CREATE TABLE emp (
    empno INT PRIMARY KEY,
    ename VARCHAR(20),
    sal DECIMAL(10,2)
);
```

Here, `empno` is the clustered index.

---

# 17. Secondary Index

Any index other than the clustered primary-key index in InnoDB is generally a secondary index.

```sql
CREATE INDEX idx_emp_ename
ON emp(ename);
```

Conceptually:

```text
empno → Primary/Clustered Index
ename → Secondary Index
```

---

# 18. Index on Foreign Key

Suppose:

```text
EMP.deptno → DEPT.deptno
```

For a frequently used query:

```sql
SELECT *
FROM emp
WHERE deptno = 20;
```

an index may be useful:

```sql
CREATE INDEX idx_emp_deptno
ON emp(deptno);
```

Indexes on columns used in JOINs can also help when appropriate.

---

# 19. Index and JOIN

Example:

```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d
ON e.deptno = d.deptno;
```

If a JOIN column is frequently used and indexing it is appropriate, an index can help MySQL find matching rows more efficiently.

Do not automatically create an index on every JOIN column. MySQL's optimizer decides how to execute the query based on available indexes and other factors.

---

# 20. Index and WHERE

Indexes are commonly useful for filtering.

```sql
SELECT *
FROM emp
WHERE deptno = 20;
```

Potential index:

```sql
CREATE INDEX idx_emp_deptno
ON emp(deptno);
```

---

# 21. Index and ORDER BY

Indexes can sometimes help with sorting.

```sql
SELECT *
FROM emp
ORDER BY ename;
```

An index on `ename` may help depending on the query and execution plan.

```sql
CREATE INDEX idx_emp_ename
ON emp(ename);
```

The index will not necessarily be used for every such query.

---

# 22. Index and GROUP BY

Indexes can sometimes help queries involving GROUP BY.

```sql
SELECT deptno, COUNT(*)
FROM emp
GROUP BY deptno;
```

An index on `deptno` may be useful depending on the execution plan.

---

# 23. EXPLAIN

Use `EXPLAIN` to understand a query's execution plan.

```sql
EXPLAIN
SELECT *
FROM emp
WHERE ename = 'SMITH';
```

It can help you understand:

- Which table is accessed
- Which indexes are considered
- Which index is chosen
- How many rows MySQL expects to examine
- Join/access strategy

---

# 24. Why Not Create Indexes on Every Column?

Indexes have costs.

### INSERT

```text
INSERT
  ↓
Table + Index maintenance
```

### UPDATE

If an indexed value changes:

```text
UPDATE
  ↓
Table + Index maintenance
```

### DELETE

Corresponding index entries must also be removed.

Therefore:

> **Indexes improve read performance but increase storage usage and write/maintenance overhead.**

---

# 25. Indexes and Storage

Indexes require additional storage.

```text
Table data
   +
Index 1
   +
Index 2
   +
Index 3
```

More indexes → more storage usage.

---

# 26. Selectivity

Selectivity describes how effectively a column can narrow down rows.

### Highly selective

Example:

```text
employee_id
```

Values:

```text
1001
1002
1003
1004
...
```

Usually many distinct values.

### Low selectivity

Example:

```text
status
```

Values:

```text
ACTIVE
ACTIVE
INACTIVE
ACTIVE
INACTIVE
...
```

Only a few distinct values.

An index on a low-selectivity column may be less useful for some queries.

---

# 27. When Should You Consider an Index?

Consider indexing columns frequently used for:

```text
WHERE
JOIN
ORDER BY
GROUP BY
```

Especially when:

- The table is large.
- Queries frequently filter using the column.
- The column has useful selectivity.
- The query is performance-sensitive.
- The index fits the application's actual query patterns.

---

# 28. When Should You Avoid an Index?

Be careful with:

- Very small tables
- Columns rarely used for searching
- Too many indexes
- Frequently changing columns
- Very low-selectivity columns where the index provides little benefit

Always evaluate the actual workload and execution plan.

---

# 29. Common Index Examples

### Index on employee name

```sql
CREATE INDEX idx_emp_ename
ON emp(ename);
```

### Index on department number

```sql
CREATE INDEX idx_emp_deptno
ON emp(deptno);
```

### Composite index

```sql
CREATE INDEX idx_emp_dept_job
ON emp(deptno, job);
```

### Unique index

```sql
CREATE UNIQUE INDEX idx_employee_email
ON employee(email);
```

### FULLTEXT index

```sql
CREATE FULLTEXT INDEX idx_article_content
ON articles(content);
```

---

# 30. Important Difference

| Concept | Purpose |
|---|---|
| Primary Key | Uniquely identifies each row |
| Unique Index | Prevents duplicate indexed values |
| Single-Column Index | Indexes one column |
| Composite Index | Indexes multiple columns |
| FULLTEXT Index | Text searching |
| SPATIAL Index | Spatial/geographical searching |
| Clustered Index | Organizes InnoDB table data around the primary key |
| Secondary Index | Additional indexes apart from the clustered index |

---

# ⭐ Interview Questions

### Q1. What is an index?

> An index is a data structure that improves the speed of data retrieval from a table by allowing MySQL to find rows more efficiently, at the cost of additional storage and write/maintenance overhead.

### Q2. Why are indexes used?

> To improve query performance, especially for suitable searches, joins, and ordering operations.

### Q3. Does an index always make a query faster?

> No. The optimizer decides whether an index is beneficial. For small tables, low-selectivity columns, or certain query patterns, an index may not help.

### Q4. What is a composite index?

> An index created on two or more columns.

### Q5. What is the leftmost-prefix principle?

> In a composite index, queries can generally benefit from the leading columns of the index, so column order matters.

### Q6. What is the disadvantage of indexes?

> They consume additional storage and increase the cost of INSERT, UPDATE, and DELETE operations because indexes must also be maintained.

### Q7. How do you check indexes?

```sql
SHOW INDEX FROM emp;
```

### Q8. How do you analyze a query plan?

```sql
EXPLAIN SELECT ...
```

---

# 🧠 Final Mental Model

```text
                    INDEX
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
     Faster Reads            Extra Cost
          │                       │
       SELECT                 Storage
       WHERE                  INSERT
       JOIN                   UPDATE
       ORDER BY               DELETE
       GROUP BY
```

## ⭐ Most Important Points

```text
1. Index → faster data retrieval
2. Primary Key → automatically indexed
3. Composite Index → multiple columns
4. Column order matters
5. Use EXPLAIN to analyze query plans
6. Indexes consume storage
7. Indexes can slow writes
8. Don't index every column
9. Selectivity matters
10. InnoDB uses a clustered primary-key index and secondary indexes
```
