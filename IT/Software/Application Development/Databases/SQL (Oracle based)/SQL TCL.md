**TCL** stands for **Transaction Control Languages**. These commands are used for maintaining consistency of the database and for the management of transactions made by the DML commands. 

A **Transaction** is a set of SQL statements that are executed on the data stored in DBMS.

- **COMMIT** − to save the changes.
- **ROLLBACK** − to roll back the changes.
- **SAVEPOINT** − creates points within the groups of transactions in which to ROLLBACK.
- **SET TRANSACTION** − Places a name on a transaction.

## Commit changes
``` SQL
DELETE FROM CUSTOMERS WHERE AGE = 25; 
COMMIT;
```

## Rollback changes
This can only rollback changes since the last COMMIT or ROLLBACK.

``` SQL
/* THIS WILL ROLLBACK THE DELETION */
DELETE FROM CUSTOMERS WHERE AGE = 25; 
ROLLBACK;

/* THIS WILL NOT ROLLBACK THE DELETION */
DELETE FROM CUSTOMERS WHERE AGE = 25; 
COMMIT;
ROLLBACK;
```

## Savepoints
A SAVEPOINT is a logical rollback point in a transaction.

``` SQL
/* OPERATIONS ...*/
SAVEPOINT savepoint_name;
/* OPERATIONS ...*/
ROLLBACK TO savepoint_name;

/* DELETE SAVEPOINT */
RELEASE SAVEPOINT SAVEPOINT_NAME;
```

## SET TRANSACTION
The SET TRANSACTION command can be used to initiate a database transaction. This command is used to specify characteristics for the transaction that follows. For example, you can specify a transaction to be read only or read write.

``` SQL
SET TRANSACTION [ READ WRITE | READ ONLY ];
```