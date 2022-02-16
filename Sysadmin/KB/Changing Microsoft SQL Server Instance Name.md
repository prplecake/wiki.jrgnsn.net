SQL Server instances are typically identified by the hostname of the computer and the name of the SQL Server instance. Ex: `<Server Name>\<Instance Name>`, A full path to the database could be `<Server Name>\<Instance Name>\<Database Name>`.

## Rename the Instance

```sql
-- This procedure lists servers
sp_helpserver
-- This procedure drops the specified server.
sp_dropserver 'SERVER_NAME' 
-- This procedure adds a new local server.
sp_addserver 'NEW_SERVER_NAME', 'local'
```