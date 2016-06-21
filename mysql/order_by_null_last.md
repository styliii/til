## Order by NULL last

### Problem
Sort by a nullable column that may or may not have a value, but ensure that the results with a null value for that column show up last (default behavior is for results with null values to show up first when ordering by that column ascending)

### Solution
MySQL has undocumented syntax to sort nulls last ([See solution here](http://stackoverflow.com/questions/2051602/mysql-orderby-a-number-nulls-last)).

```sql
SELECT * FROM tablename WHERE visible=1 ORDER BY -position DESC, id DESC
```

Place a negative symbol in front of the column where you want NULL values to show up last, and order by DESC.
