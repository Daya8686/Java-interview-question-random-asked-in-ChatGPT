# How does @Transactional annotation understand that it got failed when a table get failed to update in a spring boot application 

# Spring Boot Transaction Management

In a Spring Boot application, transactions are typically managed using Spring's transaction management abstraction, often with the help of the `@Transactional` annotation. When a transaction is managed by Spring, the framework ensures that the entire set of operations within the transaction is either fully completed (committed) or fully undone (rolled back) if any part of the transaction fails.

## How Spring Transaction Management Works

### 1. Transaction Boundaries
Transactions in Spring are defined using the `@Transactional` annotation, which can be applied at the method or class level. When a method annotated with `@Transactional` is invoked, Spring creates a transaction context.

### 2. Transaction Management
Spring uses a `PlatformTransactionManager` to manage transactions. Common implementations include:
- `DataSourceTransactionManager` for JDBC.
- `JpaTransactionManager` for JPA.
- `HibernateTransactionManager` for Hibernate.

### 3. Transaction Propagation
Spring handles different propagation behaviors (e.g., `REQUIRED`, `REQUIRES_NEW`, etc.) which determine how transactions are managed in nested method calls.

### 4. Exception Handling and Rollback
When a transaction is active, Spring monitors the method execution for exceptions. By default, Spring will roll back the transaction if a runtime (unchecked) exception (`RuntimeException` or its subclasses) is thrown. It will not roll back on checked exceptions unless explicitly configured.

### 5. Failure Detection
If an operation within the transaction fails (e.g., a database update fails due to a constraint violation), an exception will be thrown. Spring's transaction management infrastructure will catch this exception and determine whether to roll back the transaction.

## Example

Consider the following example of a Spring Boot service class using `@Transactional`:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class EmployeeService {

    @Autowired
    private EmployeeRepository employeeRepository;

    @Autowired
    private DepartmentRepository departmentRepository;

    @Transactional
    public void updateEmployeeAndDepartment(Employee employee, Department department) {
        // Update employee information
        employeeRepository.save(employee);

        // Update department information
        departmentRepository.save(department);
    }
}
```
## How Transaction Fails and is Handled

### Update Operation
Both `employeeRepository.save(employee)` and `departmentRepository.save(department)` are part of the same transaction.

### Exception Occurs
If either of these operations throws a `RuntimeException` (e.g., due to a database constraint violation), the exception will propagate up the call stack.

### Transaction Rollback
Spring's transaction management detects the exception and marks the transaction for rollback. This means all changes made within the transaction are undone.

### Transaction Status
The transaction manager updates the transaction status to indicate failure.

## Custom Rollback Rules
You can customize the rollback behavior using the `rollbackFor` and `noRollbackFor` attributes of `@Transactional`.

### Example
```java
@Transactional(rollbackFor = Exception.class, noRollbackFor = SpecificException.class)
public void updateEmployeeAndDepartment(Employee employee, Department department) {
    // Update employee information
    employeeRepository.save(employee);

    // Update department information
    departmentRepository.save(department);
}
```

```java

@Transactional(rollbackFor = {SQLException.class, MyCustomException.class})
public void updateEmployeeAndDepartment(Employee employee, Department department) {
    // Update operations
}

```
## Transaction Management with Programmatic Approach
While `@Transactional` is the most common way to manage transactions, you can also manage them programmatically.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.PlatformTransactionManager;
import org.springframework.transaction.TransactionDefinition;
import org.springframework.transaction.TransactionStatus;
import org.springframework.transaction.support.DefaultTransactionDefinition;

@Service
public class EmployeeService {

    @Autowired
    private PlatformTransactionManager transactionManager;

    public void updateEmployeeAndDepartment(Employee employee, Department department) {
        DefaultTransactionDefinition def = new DefaultTransactionDefinition();
        def.setName("updateEmployeeAndDepartment");
        def.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRED);

        TransactionStatus status = transactionManager.getTransaction(def);
        try {
            // Update employee information
            employeeRepository.save(employee);

            // Update department information
            departmentRepository.save(department);

            transactionManager.commit(status);
        } catch (Exception e) {
            transactionManager.rollback(status);
            throw e;
        }
    }
}
```
---
In summary, Spring's transaction management infrastructure detects failures by monitoring for exceptions during transaction execution. If an exception occurs, it marks the transaction for rollback, ensuring data consistency.
