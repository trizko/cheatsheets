### Backup Strategies

In this article, we will discuss 3 different ways to backup and restore your database:
- SQL Dump
- File system level backup
- Continuous archiving


#### SQL Dump

An SQL dump is the simplest form of backup and restoration strategies. The basic idea of this method is to output a file of SQL statements that represent the entire database.


##### _Backup_

Using the `pg_dump` command line utility, we can easily create a backup in the form of a SQL text file. This file is meant to be used with the command line utility `psql`. Example usage:

```bash
$ pg_dump dbname
```

This command will print the SQL commands to standard output. A more useful command would be:

```bash
$ pg_dump dbname > backup.sql
```

The `>` will redirect the printed output into the newly created or overwritten(if already exists) file named `backup.sql`. You can also accomplish this by passing the `-f` flag:

```bash
$ pg_dump -f backup.sql dbname
```

We do not specify the location of the database or the user to read the data as. This is because `pg_dump` assumes that our username is the current operating system username and the location defaults to `localhost` on port `5432`. We can override these defaults by passing the following options:

```bash
$ pg_dump -U postgres -h localhost -p 5432 -f backup.sql dbname
```

Note that the user that is used with `pg_dump` in this scenario must be a superuser, since we are backing up the entire database. If we wanted to only dump a specific table with a user that only has read privileges for that table, we could use the `-t` flag:

```bash
$ pg_dump -U username -t tablename -f backup.sql dbname
```

>An important advantage of pg_dump over the other backup methods
>described later is that pg_dump's output can generally be re-loaded into
>newer versions of PostgreSQL, whereas file-level backups and continuous
>archiving are both extremely server-version-specific. pg_dump is also
>the only method that will work when transferring a database to a
>different machine architecture, such as going from a 32-bit to a 64-bit
>server.
>
>-http://www.postgresql.org/docs/9.4/static/backup-dump.html

#### _Restore_

Restoring a database after generating an SQL file from `pg_dump` is made very easy with the the help of the `psql` command line utility. Example usage:

```bash
$ psql dbname < backup.sql
```
Or, using the `-f` flag(just as we did with `pg_dump`):
```bash
$ psql -f backup.sql dbname
```
