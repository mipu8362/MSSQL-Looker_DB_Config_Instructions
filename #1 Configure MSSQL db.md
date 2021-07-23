# Encrypting Network Traffic
Looker strongly recommends encrypting network traffic between the Looker application and your database. Consider one of the options described on the Enabling secure database access documentation page.

If you’re interested in using SSL encryption, see the Microsoft documentation.


# Configuring Server Authentication
Looker requires “SQL Server Authentication” on your MSSQL server. If your MSSQL server is configured as “Windows Integrated Authentication” only, change the server configuration to “Windows Integrated Authentication and SQL Server Authentication.”

If this is not set properly Looker will be unable to connect. This will appear in your SQL Server log messages like: “An attempt to log in using SQL authentication failed. Server is configured for windows authentication only.”

If this change is required you can complete the following steps:
1. In SQL Server Management Studio Object Explorer, right-click the server, and then click Properties.
2. On the Security page, under Server authentication, select the new server authentication mode, and then click OK.
3. In the SQL Server Management Studio dialog box, click OK to acknowledge the requirement to restart SQL Server.
4. In Object Explorer, right-click your server, and then click Restart. If SQL Server Agent is running, it must also be restarted.
You can read about this more in Microsoft’s documentation.


# Creating a Looker User

Looker authenticates to your database using SQL Server Authentication. Using a domain account is not supported.

To create an account, run the following commands. Change some_password_here to a unique, secure password:
```sql
CREATE LOGIN looker
  WITH PASSWORD = 'some_password_here';
USE MyDatabase;
CREATE USER looker FOR LOGIN looker;
GO
```


# Granting the Looker user permission to SELECT from tables
Looker requires the SELECT permission for each table or schema you will want to query. There are multiple ways to assign SELECT permission:
- To grant SELECT permission to individual schemas, run the following command for each schema:
```sql
GRANT SELECT on SCHEMA :: 'schema_name' to looker;
```
- To grant SELECT permission to individual tables, run the following command for each table:
```sql
GRANT SELECT on OBJECT :: 'schema_name'.'table_name' to looker;
```
- For MSSQL version 2012 or later, you can alternatively assign the Looker user the db_datareader role using these commands:
```sql
USE MyDatabase;
ALTER ROLE db_datareader ADD MEMBER looker;
GO
```

# Granting the Looker user permission to view and stop running queries
Looker requires rights to detect and stop currently running queries, which requires the following permissions:

- ALTER ANY CONNECTION
- VIEW SERVER STATE
To grant these permissions, run the following commands:
```sql
USE Master;
GRANT ALTER ANY CONNECTION TO looker;
GRANT VIEW SERVER STATE to looker;
GO
```
# Granting the Looker user permission to create tables
To give the Looker user the permission to create **PDTs**, issue the following commands:
```sql
USE MyDatabase;
GRANT CREATE TABLE to looker;
GO
```

# Temp schema setup
To create a schema owned by the Looker user and grant the necessary rights to the Looker user, issue this command:
```sql
CREATE SCHEMA looker_scratch AUTHORIZATION looker;
```



https://docs.looker.com/setup-and-management/database-config/mssql
