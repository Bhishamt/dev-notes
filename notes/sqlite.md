# SQLite

## CLI

```bash
sqlite3 app.db
```

```sql
.tables
.schema users
.headers on
.mode box
```

## Pragmas worth setting

```sql
PRAGMA journal_mode = WAL;     -- concurrent readers alongside one writer
PRAGMA busy_timeout = 5000;    -- wait for the lock instead of failing with "database is locked"
PRAGMA foreign_keys = ON;      -- off by default, and it is per connection
PRAGMA synchronous = NORMAL;   -- durable enough with WAL, much faster than FULL
```

Every connection needs `foreign_keys` and `busy_timeout` — they are not stored in the file.

## Notes

- `INTEGER PRIMARY KEY` is an alias for the rowid: fast, no extra index. `AUTOINCREMENT` only prevents rowid reuse and costs a bit.
- Store timestamps as ISO-8601 text (`2026-11-10T14:03:00Z`) or unix epoch integers. Both sort correctly; mixed formats do not.
- Copying a live database by copying the file can miss data in `-wal`. Use `sqlite3 app.db ".backup out.db"` instead.
- `EXPLAIN QUERY PLAN` shows whether an index is used. `CREATE INDEX idx ON t(col)` where the query filters or sorts on `col`.
