# Problem
Extract latest data points (w.r.t Date column) from PostgreSQL table (having multiple entries for same user) by JOINing it with other table w.r.t userId. 

# Environment
* IDE Version : pyCharm Community Edition 2022.2.3
* Python Version: 3.8
* PgAdmin Version: 6.15
* PostgreSQL Version: 14.6
* psycopg2 Version: 2.9.5

# How you fix it
Use of subquery and Max function is the key. Other commonly used SQL functions DISTINCT, ORDER BY, GROUP BY doesn't help in this cause. 
Indexing the columns will speed up things.
# Solution
### PostgreSQL Query
Below PostgreSQL query first joins two tables, then apply required filters, and put Max function within a subquery
to get the latest date.
```
SELECT t1."userId"  
FROM "table1" t1
JOIN "table2" t2 ON t1."userId" = t2."userId"
WHERE t1."Date" BETWEEN '2022-02-01' and '2022-10-31' 
        AND (t1."description" = 'Customer funded' or t1."description" = 'Customer Funded' or t1."description" = 'Customer Funding')
    AND t2."accountType" = 'PRIMARY'
    AND t2."updatedAt" = (SELECT MAX ("updatedAt") 
                          FROM "table2"
                          WHERE "userId" = t2."userId"
                          AND t2."transactions" IS NOT NULL
```
Note: you can join 3rd table in the subquery as well. 

### Below is python code to execute above query

psycopg2 library is being used here. although there are more options available in this regard.
```
import psycopg2
conn = None
try:
    conn = psycopg2.connect(database="new",
                            host="new.dummy.amazonaws.com",
                            user="postgres user",
                            password="password",
                            port=port,
                            )
    PostgreSQL_Query = """
                       SQL query here
                       """
    cursor = conn.cursor()
    cursor.execute(PostgreSQL_Query)
    data = cursor.fetchall()
    cursor.close()
except (Exception, psycopg2.DatabaseError) as error:
    print(error)
finally:
    if conn is not None:
        conn.close()    
```
