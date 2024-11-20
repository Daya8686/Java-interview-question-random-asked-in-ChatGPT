# Difference Between Inner Join and Outer Join and How to Use Joins in Spring JPA?

# Inner Join

## Definition:
An inner join returns only the rows that have matching values in both tables. It filters out records where there is no match between the two tables.

## SQL Syntax:
```sql
SELECT * FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```
# Outer Join

## Definition:
An outer join returns all the rows from one table and the matched rows from the other table. If there is no match, the result is `NULL` for columns of the table without a match.

### Types of Outer Joins:
- **Left Outer Join**: Returns all rows from the left table and matched rows from the right table.
- **Right Outer Join**: Returns all rows from the right table and matched rows from the left table.
- **Full Outer Join**: Returns all rows when there is a match in either table.

## SQL Syntax:

### Left Join:
```sql
SELECT * FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### Right Join:
```sql

SELECT * FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### Full Join:
```sql

SELECT * FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

#### Using Joins in Spring Data JPA:
In Spring Data JPA, you can use JPQL or native queries to perform joins. Here's how you can perform an inner join and a left join:

### Inner Join Example:

```java

@Query("SELECT e FROM Employee e JOIN e.department d WHERE d.name = :deptName")
List<Employee> findEmployeesByDepartmentName(@Param("deptName") String deptName);
```
### Left Outer Join Example:

```java

@Query("SELECT e FROM Employee e LEFT JOIN e.department d")
List<Employee> findAllEmployeesWithDepartments();
```
### Native Query Example:

```java

@Query(value = "SELECT * FROM Employee e INNER JOIN Department d ON e.dept_id = d.id WHERE d.name = :deptName", nativeQuery = true)
List<Employee> findEmployeesByDepartmentNameNative(@Param("deptName") String deptName);
```
