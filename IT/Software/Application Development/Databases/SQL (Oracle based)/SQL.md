SQL (Structured Query Language) is a language designed for communication between users and databases. Its purpose is to perform tasks related to retrieving stored information, performing calculations, modifying existing data, and adding new rows containing information about clients, products, transactions (such as sales, purchases, orders, reservations, attendance, absences, arrivals, etc.). This is because most modern applications use relational databases and, consequently, SQL.

The most notable feature of SQL is that it is non-procedural. In other words, it doesn't specify how to perform a task in its statements but rather describes the desired result. The database server, based on its optimizer and metadata (data about data), handles the task of executing the provided SQL statement.

Although SQL doesn't have control flow statements in its original design, some optional control flow features have been included in the SQL standard, such as ISO/IEC 9075-5:1996, which can provide some control over execution.

Additionally, control flow statements, known as persistent stored modules, are often considered as procedural extensions to SQL. Database providers offer these extensions, such as Oracle's PL/SQL, Microsoft SQL Server's T-SQL, IBM's DB2 SQL-PL, and PostgreSQL's PSQL. These extensions generally complement SQL to create stored procedures, packages, and triggers, which will be explained in the following module.

**Characteristics of the SQL Language:**

SQL is a language specifically designed for communication with databases. Unlike other languages like English or programming languages like Java or Visual Basic, SQL is based on a limited set of words. This simplicity is intentional, as SQL is designed to efficiently read and write data in a relational database.


[[SQL DDL]]
[[SQL DML]]
[[SQL TCL]]