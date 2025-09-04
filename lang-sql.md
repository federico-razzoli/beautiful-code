# Beautiful SQL

These queries are tested on MariaDB. Where possible, I try to make them fairly standard.


## Truth

```
SELECT NULL IS UNKNOWN;
```

`IS UNKNOWN` is a synonym for `IS NULL`.

Unbeautiful note: `UNKNOWN` is not a synonym for `NULL`. And `NULL` semantics only suggest an unknown value
in some cases.


## Fibonacci

```
WITH RECURSIVE fibonacci(n, current_value, next_value) AS (
    (
        SELECT
            -- 0-based "index"
            0 AS n,
            -- first Fibonacci number
            0 AS current_value,
            -- second Fibonacci number
            1 AS next_value
    ) UNION ALL (
        SELECT 
                n + 1, 
                next_value, 
                current_value + next_value
            FROM 
                fibonacci
            -- limit the number of rows (the series is infinite)
            WHERE n < 20
    )
)
SELECT n AS natural_number, current_value AS fibonacci_number
    FROM fibonacci
    ORDER BY n
;
```


## Trees

Traverse a tree up to the root:

```
WITH RECURSIVE path_to_root AS (
    (
    -- starting node
    SELECT node_id, parent_id, 0 AS level
        FROM tree
        WHERE node_id = ?
    ) UNION ALL (
    -- recursively query the next levels
    SELECT t.node_id, t.parent_id, p.level + 1 AS level
        FROM tree t
        JOIN path_to_root p
            ON t.node_id = p.parent_id
)
SELECT node_id 
    FROM path_to_root
    ORDER BY level
;
```

## Find Ranges by Point

```
... WHERE '1994-01-01 00:00:00' BETWEEN start_timestamp AND end_timestamp
```

Unfortunately, some DBMSs don't optimise this properly.

