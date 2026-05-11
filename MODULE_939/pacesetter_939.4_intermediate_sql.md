# Pacesetter Guide 939.4 - Intermediate SQL

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

SQL remains the backbone of data access in most organizations. Many RAG applications combine structured data from databases with unstructured data from documents. Strong SQL skills complement your vector search capabilities and are essential for AI application development.

## Learning Objectives

- Write complex SQL queries with JOINs, subqueries, and CTEs
- Use window functions for analytical queries
- Aggregate and group data effectively
- Optimize query performance
- Combine SQL data with AI pipelines

---

## Key Concepts

### Common Table Expressions (CTEs)

```sql
WITH monthly_sales AS (
    SELECT 
        DATE_TRUNC('month', sale_date) AS month,
        SUM(amount) AS total_sales
    FROM sales
    GROUP BY 1
)
SELECT month, total_sales,
    LAG(total_sales) OVER (ORDER BY month) AS prev_month
FROM monthly_sales;
```

### Window Functions

```sql
SELECT 
    employee_name,
    department,
    salary,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank,
    AVG(salary) OVER (PARTITION BY department) AS dept_avg
FROM employees;
```

### SQL in AI Applications

| Use Case | SQL Role |
|----------|----------|
| **RAG metadata filtering** | Query structured metadata alongside vector search |
| **Data preparation** | Extract and transform data for embedding |
| **Analytics** | Analyze AI application usage and performance |
| **Feature engineering** | Create features for ML models from database data |

---

## DataCamp Course

**[Intermediate SQL](https://app.datacamp.com/learn/courses/intermediate-sql)**

---

## Related Assessment

- **[POC 939.4.1 - Intermediate SQL (25 pts)](https://perscholas.instructure.com/courses/3227/assignments/627661)**

---

## Canvas Links

- [Pacesetter Guide 939.4](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-939-dot-4-intermediate-sql)
