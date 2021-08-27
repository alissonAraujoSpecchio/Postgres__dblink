# dblink
Repository to save dblink configuration, steps, how to use, etc...

## Creating extension

To use dblink it's necessary to create the extension dblink, but it's just possible if postgres-contrib is installed, so use:

### FEDORA/CENTOS
```
sudo dnf install postgres-contrib
```

### UBUNTU
```
sudo apt install postgres-contrib
```

Then, logged in the database, you can create the extension:

```sql
CREATE EXTENSION dblink;
```
## Example How to Use

```sql
CREATE TABLE teste_table AS
    SELECT * FROM dblink('host=hostname user=username
                         password=passwd dbname=teste_db',
                         'select * from remote_teste_table)
    AS t1(
         id integer,
         name varchar,
    );
```

## dblink_exec

This one is used to execute commands that don't return rows, like drops, inserts and deletes.
Example:

```sql
select dblink_exec('host=hostname user=username
                   password=passwd dbname=teste_db',
                   'drop table teste_table');
```
