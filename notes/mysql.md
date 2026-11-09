# MySQL

## Admin & Service

```powershell
# Quick startup with custom config
mysqld --defaults-file="my.ini" --console

# Safe shutdown
mysqladmin -u root -p shutdown
```

## User Grants & Roles

```sql
-- Create role and grant access
CREATE ROLE IF NOT EXISTS 'app_role';
GRANT SELECT, INSERT, UPDATE, DELETE ON app_db.* TO 'app_role';
GRANT 'app_role' TO 'app_user'@'%';
SET DEFAULT ROLE 'app_role' TO 'app_user'@'%';
FLUSH PRIVILEGES;
```

## Inspection & Locks

```sql
-- View running queries
SHOW FULL PROCESSLIST;

-- Inspect locked transactions
SELECT * FROM performance_schema.data_locks;
SELECT * FROM performance_schema.data_lock_waits;
```
