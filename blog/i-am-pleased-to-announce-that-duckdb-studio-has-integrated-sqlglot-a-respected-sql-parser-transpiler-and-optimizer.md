# I am pleased to announce that DuckDB Studio has integrated SQLGlot, a respected SQL parser, transpiler, and optimizer

> DuckDB Studio has integrated SQLGlot, a widely recognized SQL parser, transpiler, and optimizer, enhancing its SQL processing capabilities.

Author: Senthilnathan Karuppaiah · Date: 2024-04-12

### What is SQLGlot?

 
<a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://sqlglot.com/sqlglot.html">SQLGlot</a> is a no-dependency SQL parser, transpiler, optimizer, and engine. It can be used to format SQL or translate between <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://github.com/tobymao/sqlglot/blob/main/sqlglot/dialects/__init__.py">21 different dialects</a> like <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://duckdb.org/" >DuckDB</a>, <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://prestodb.io/">Presto</a> / <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://trino.io/">Trino</a>, <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://spark.apache.org/" >Spark</a> / <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://www.databricks.com/" >Databricks</a>, Snowflake, and BigQuery. It aims to read a wide variety of SQL inputs and output syntactically and semantically correct SQL in the targeted dialects.

![TickitDB](/i/blog/Iam-pleased-to-announceDuckDB-Studio-has-integrated-SQLGlot-banner.GIF)

## So, what’s new?

Seamless SQL Parsing: Extract tables, columns, and select fields effortlessly.

Cross-Dialect Translation: Speak SQL in 21 dialects! Whether it’s DuckDB, Presto/Trino, or Snowflake, switch dialects like you switch tabs.

Smart Optimization: Fine-tune SQL queries for peak performance.

Code Beautification: Write SQL that's not just functional but also aesthetically pleasing, making maintenance and collaboration a breeze.

SQL parsing goes beyond just being clever; it’s an indispensable instrument in DataOps, crucial for revealing insights about table and field usage, data lineage, and analytics of data flow.

It's been rewarding to incorporate SQLGlot's capabilities into DuckDB Studio, all the credits goes to Toby Mao, the creative mind behind SQLGlot and Tobiko Data, the DataOps Platform. Their significant contributions are instrumental in driving the data engineering field toward a more interconnected and productive future.

See the integration in action at DuckDB Studio, now live on Vercel