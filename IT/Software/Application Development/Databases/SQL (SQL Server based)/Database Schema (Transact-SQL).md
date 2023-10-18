**Applies to:** ![](https://learn.microsoft.com/en-us/sql/includes/media/yes-icon.svg?view=sql-server-ver16) [SQL Server](https://learn.microsoft.com/en-us/sql/sql-server/sql-docs-navigation-guide?view=sql-server-ver16#applies-to) ![](https://learn.microsoft.com/en-us/sql/includes/media/yes-icon.svg?view=sql-server-ver16) [Azure SQL Database](https://learn.microsoft.com/en-us/sql/sql-server/sql-docs-navigation-guide?view=sql-server-ver16#applies-to) ![](https://learn.microsoft.com/en-us/sql/includes/media/yes-icon.svg?view=sql-server-ver16) [Azure SQL Managed Instance](https://learn.microsoft.com/en-us/sql/sql-server/sql-docs-navigation-guide?view=sql-server-ver16#applies-to) ![](https://learn.microsoft.com/en-us/sql/includes/media/yes-icon.svg?view=sql-server-ver16) [Azure Synapse Analytics](https://learn.microsoft.com/en-us/sql/sql-server/sql-docs-navigation-guide?view=sql-server-ver16#applies-to) ![](https://learn.microsoft.com/en-us/sql/includes/media/yes-icon.svg?view=sql-server-ver16) [Analytics Platform System (PDW)](https://learn.microsoft.com/en-us/sql/sql-server/sql-docs-navigation-guide?view=sql-server-ver16#applies-to) ![](https://learn.microsoft.com/en-us/sql/includes/media/yes-icon.svg?view=sql-server-ver16) [SQL Endpoint in Microsoft Fabric](https://learn.microsoft.com/en-us/sql/sql-server/sql-docs-navigation-guide?view=sql-server-ver16#applies-to) ![](https://learn.microsoft.com/en-us/sql/includes/media/yes-icon.svg?view=sql-server-ver16) [Warehouse in Microsoft Fabric](https://learn.microsoft.com/en-us/sql/sql-server/sql-docs-navigation-guide?view=sql-server-ver16#applies-to)

``` SQL
-- Syntax for SQL Server and Azure SQL Database 
CREATE SCHEMA schema_name_clause [ <schema_element> [ ...n ] ] 

<schema_name_clause> ::= 
	{ 
	schema_name 
	| AUTHORIZATION owner_name 
	| schema_name AUTHORIZATION owner_name 
	} 
	
<schema_element> ::= 
	{ 
	table_definition 
	| view_definition 
	| grant_statement 
	| revoke_statement 
	| deny_statement 
	}
```

A **schema** is a collection of database objects like tables, triggers, stored procedures, etc. A schema is connected with a user which is known as the schema owner. Database may have one or more schema.

``` SQL
CREATE SCHEMA nacho_sch AUTHORIZATION nacho;

CREATE TABLE nacho_sch.Persons(
id INT PRIMARY KEY IDENTITY, 
Name VARCHAR(200), 
DOB DATETIME2 NOT NULL
);
```

``` SQL
/* LIST ALL SCHEMAS */
SELECT  *
FROM sys.schemas
```