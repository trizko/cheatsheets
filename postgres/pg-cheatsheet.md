##### postgresql.conf file
Normal postgresql db settings file that will appear in both the master and the replica of a db.

##### recovery.conf file
The presence of this file turns on replication. It also has configuration options that can only pertain to a db replica. This file must always be in the $PGDATA directory.

```bash
# start postgresql db
# -D    data directory of db to control (pgdata)
$ pg_ctl -D ~/pgdata start

# pg_basebackup command for starting the replication
# -x    also copy the transaction logs
# -P    show progress meter
# -D    (required) location of data directory (must be empty directory)
# -p    port of db host
# -h    location of host
$ pg_basebackup -x -P -D ~/replica -p 5432 -h localhost


# Simple testing of a postgresql db
# -i    initialize
# -s    scale
# -U    user
# bench target database
$ pgbench -i -s 10 -U bench bench
```
