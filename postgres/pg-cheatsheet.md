##### postgresql.conf file
Normal postgresql db settings file that will appear in both the master and the replica of a db.

##### recovery.conf file
The presence of this file turns on replication. It also has configuration options that can only pertain to a db replica. This file must always be in the $PGDATA directory. Sample:
```
standby_mode = 'on'
primary_conninfo = 'host=<master_ip> port=5432 user=rep password=yourpassword'
trigger_file = '/tmp/postgresql.trigger.5432'
```

##### SQL
```SQL
-- Create replication user
CREATE USER rep REPLICATION LOGIN CONNECTION LIMIT 1 ENCRYPTED PASSWORD 'yourpassword';
```

##### General commands
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
##### HOW TO INSTALL POSTGRESQL 9.4 ON CENTOS 6
```bash
# download package metadata
$ curl -O http://yum.postgresql.org/9.4/redhat/rhel-7-x86_64/pgdg-centos94-9.4-2.noarch.rpm

# install package metadata
$ yum localinstall pgdg-centos94-9.4-2.noarch.rpm

# install these packages for both production and development
$ yum install postgresql94-server.x86_64 postgresql94-devel.x86_64 libpqxx.x86_64
# install these for development only.
$ yum install postgresql94.x86_64 postgresql94-contrib.x86_64

# switch to postgres user
$ sudo -u postgres -i  # this is preferred over "sudo su - postgres"

# add postgres utilities to PATH
$ vim ~/.bash_profile
$ export PATH="$PATH:/usr/pgsql-9.4/bin/"
$ source ~/.bash_profile  # reload bash_profile to apply changes

# initialize the data directory (default: /var/lib/pgsql/9.4/data)
$ initdb

# start database server
$ exit  # exit postgres user. return to being root
$ service postgresql-9.4 start

# return to being postgres user
$ sudo -u postgres -i

# now you can connect to the db
$ psql

# enable python to connect to the db
$ pip install psycopg2
```
