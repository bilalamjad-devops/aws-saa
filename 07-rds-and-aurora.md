

# 6. The most important distinction for your notes

Add this:

### RDS Events

Monitor **RDS infrastructure/service events**:

```text
Instance failure
Failover
Backup
Maintenance
Configuration changes
```

They **do NOT detect SQL data changes** such as:

```text
INSERT
UPDATE
DELETE
```

### Aurora MySQL → Lambda

Aurora MySQL can use native Lambda integration to react to database operations.

```text
Database change
      ↓
Aurora MySQL
      ↓
Lambda
      ↓
SQS
```


24-August-2026
