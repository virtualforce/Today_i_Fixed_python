# Problem
How to search multiple words by parsing a PostgreSQL JSON column using SQL query. 

# Environment
* PgAdmin Version: 6.15
* PostgreSQL Version: 14.6

# How you fix it
The trick is to make use of Postgres JSON parsing with normal Full Text Search functions of 
to_tsvector & to_tsquery.

# Solution
### PostgreSQL Query
Below is the PostgreSQL query, which look into "Payload" column in "Accounts" table. Then
parse the JSON in "Payload", and take the 2nd element of sub-field of 'name' within 'transactions'
field to search for two words 'transfer' & 'checking'.
```
    SELECT id, "userId", "date" 
    FROM public."Accounts" ac
    WHERE to_tsvector(ac."Payload"::json#>>'{transactions, name, 1}') @@ to_tsquery('transfer & checking')
    ORDER BY "date" DESC LIMIT 10;
``` 

# Refrences

* [Controlling Text Search](https://www.postgresql.org/docs/current/textsearch-controls.html)
* [Work Easily With JSON Using PostgreSQL Parse JSON](https://hevodata.com/learn/postgresql-parse-json/)