# Postgres Workshop

### Objectives
Become familiar with SQL commands to:
 * create new databases
 * create tables in a database
 * add rows
 * retrieve data from existing databases
 * alter tables (e.g. add columns)
 * run the above on your machine

### Practice SQL commands
Practice SQL commands going through the following sections of this [tutorial](sqlzoo.net) (you can do more if you like, of course):
* [SELECT](http://sqlzoo.net/wiki/SELECT_basics)
* [UPDATE](http://sqlzoo.net/wiki/UPDATE)
* [ALTER](http://sqlzoo.net/wiki/ALTER)
* [DELETE](http://sqlzoo.net/wiki/DELETE)
* [UNION](http://sqlzoo.net/wiki/UNION)

### Create and update a database

Except from 1. and 2. you will find out all the commands you need on your own (in pairs)!
1. on your command-line open the postgreSQL (psql) shell - ``psql`` or ``psql postgres``.
2. create a new database with ``create database database_name``. If you get ``ERROR:  permission denied to create database``, exit the shell and start a terminal session as user "postgres" (``sudo -su postgres``) and open psql.
3. Create a table with naming of your choice.
4. Play with SQL commands in order to:
 * Query the table by specific parameters
 * Alter the values of existing cells of your table
 * Alter data types
 * Add columns
 * Combine operations
 * etc. surprise us!

### Resources
* [PG Databases management](https://www.postgresql.org/docs/9.6/static/managing-databases.html) (includes creation)
* [PG Queries](https://www.postgresql.org/docs/9.6/static/queries.html)
* [SQL tutorial](sqlzoo.net)`
