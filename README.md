RefreshAllMaterializedViews
===========================

Function to refresh all materialized views in a PostgreSQL 9.4 database (for PostgreSQL 9.3 use release v1.0 that does not rely on concurrent materialized view updates).

PostgreSQL 9.4 supports materialized views but does not have a functionality 
to refresh the views except for issuing refresh command for each view 
individually.  After asking on stackoverflow and not finding solution 
(http://stackoverflow.com/questions/19981600/how-to-refresh-all-materialized-views-in-postgresql-9-3-at-once) 
I decided to write my own function.

Usage
-----

The function has two optional parameters, _schema and _concurrently.
The default is all schemas for _schema and false for _concurrently.

To refresh views in all schemas, not concurrently:
```sql
select RefreshAllMaterializedViews();
select RefreshAllMaterializedViews('*');
select RefreshAllMaterializedViews('*', false);
```

To refresh views in one schema, not concurrently:
```sql
select RefreshAllMaterializedViews('my_schema');
select RefreshAllMaterializedViews('my_schema', false);
```

To refresh views in all schemas concurrently:
```sql
select RefreshAllMaterializedViews('*', true);
```

To refresh views in one schema concurrently:
```sql
select RefreshAllMaterializedViews('my_schema', true);
```


Note: If you created the materialized view ```WITH NO DATA``` you have'll have to first populate the Materialized Views with RefreshAllMaterializedViews() before you can use the concurrent version.
