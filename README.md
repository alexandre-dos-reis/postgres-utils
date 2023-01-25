# postgres-utils

## Functions

### List of functions

```sql
select
    routine_name
from 
    information_schema.routines
where 
    routine_type = 'FUNCTION'
and
    routine_schema = 'public';
```

### Create a function (with idempotency)

```sql
create or replace function add(a int, b int) returns int as $$
declare 
    -- variable declaration
begin
    -- logic
    select a + b
end;
$$ language sql stable;
```

## Roles / User

### Create a user with login enabled

```sql
create role 
    forum_example_postgraphile login password 'xyz';
```

### Create a role with idempotency

```sql
DO $$
BEGIN
    CREATE ROLE rick_deckard;    
EXCEPTION   
    WHEN duplicate_object THEN
        RAISE NOTICE 'Role already exists. Ignoring...';    
END$$;
```
