# Query Performance Insights

Query Performance Insights (QPI) is a collection of useful scripts that enable you find what is happening with your SQL Server. It is a set of views and functions that wrap Query Store and Dynamic Management Views.

## Why I need this kind of library?

SQL Server/Azure SQL Database provide a lot of views that we can use to analyze query performance (dynamic management views and Query Store views). However, sometime it is hard to see what is happening in the database engine. There are DMVs and Query Store, but when we need to get the answer to the simple questions such as "Did query performance changed after I added an index?" or "How many IOPS do we use?", we need to dig into Query Store schema, think about every single report, or search for some useful query.

This is the reason why I have collected the most useful queries that find information from underlying system views, and wrapped them in a set of useful views. Some usefull resources that I have used:

 - Paul Randal [Wait statistics library](https://www.sqlskills.com/help/waits/), [Wait statistics - tell me where it hurts](https://www.sqlskills.com/blogs/paul/wait-statistics-or-please-tell-me-where-it-hurts/), [How to examine IO subsystme latencies](https://www.sqlskills.com/blogs/paul/how-to-examine-io-subsystem-latencies-from-within-sql-server/)
 - Erin Stellato [What Virtual Filestats Do, and Do Not, Tell You About I/O Latency](https://sqlperformance.com/2013/10/t-sql-queries/io-latency).
 - Aaron Bertrand [Determine system memory](https://www.mssqltips.com/sqlservertip/2393/determine-sql-server-memory-use-by-database-and-object/)
 - Dimitri Furman & [SqlCat team](https://blogs.msdn.microsoft.com/sqlcat/) blog posts
 - Tim Ford & Louis Davidson [Performance tunning with DMV](https://www.red-gate.com/library/performance-tuning-with-sql-server-dynamic-management-views), 
 - Ajith Krishnan [Interpreting the counter values from sys.dm_os_performance_counters](https://blogs.msdn.microsoft.com/psssql/2013/09/23/interpreting-the-counter-values-from-sys-dm_os_performance_counters/).

## Examples

Getting information abouth your workload:
```
select * from qpi.queries;

select * from qpi.dm_queries;
select * from qpi.dm_bre;
```

Getting the information about the system performance:
```
exec qpi.snapshot_file_stats;
select * from qpi.file_stats;

exec qpi.snapshot_wait_stats;
select * from qpi.wait_stats;

exec qpi.snapshot_perf_counters;
select * from qpi.perf_counters;
```

## Performance analysis

QPI library simplifies query performance analysis. Some useful scripts and scenarios are shown in [query performance analysis page](doc/QueryPerformanceAnalisys.md).

## Installation
QPI library is just a set of views, functions, and utility tables that you can install on your SQL Server or Azure SQL instance. Currently, it supports SQL Server 2016+ and Azure SQL Database.
You can download the [source](https://raw.githubusercontent.com/JocaPC/qpi/master/src/qpi.sql) and run it in your database. All functions, views, and tables are placed in `qpi` schema in your database. You can also remove all funcitons and views in `qpi` schema using [cleaning script](https://raw.githubusercontent.com/JocaPC/qpi/master/src/qpi.clean.sql)

> Many views depends on Query Store so make sure that Query store is running on your SQL Server.