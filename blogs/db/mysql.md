# MySQL troubleshoot and tricks

### User management

Login as root from the shell:
```
$ mysql -u[username] -p
```

Existing user list (login as root user):
```
$ USE mysql;
$ SELECT User FROM mysql.user;
```

Create new user:
```
$ CREATE USER 'newuser'@'hostname' IDENTIFIED BY 'password';
```

Update/Change user password:
```
$ USE mysql;
$ ALTER USER 'user'@'hostname' IDENTIFIED BY 'newpassword'; 
OR
$ SET PASSWORD FOR 'username'@'hostname' = PASSWORD('newpassword');
OR
$ UPDATE mysql.user SET Password=PASSWORD('newpassword') WHERE USER='username' AND Host='hostname';
```

Grant all previleadge to the user:
```
$ GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'hostname';
$ FLUSH PRIVILEGES;
```

Grant user to a specific database:
```
$ GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'hostname';
$ FLUSH PRIVILEGES;
```

Grant user to a specific database table only:
```
$ GRANT [type_of_permissio(ex-create, update)] ON database_name.table_name TO ‘username’@'hostname;
$ FLUSH PRIVILEGES;
```

Assigned permissions of a user:
```
$ SHOW GRANTS FOR 'username'@'hostname';
```

Revoke permission of a user from a database:
```
$ REVOKE permission ON database_name.* FROM 'username'@'hostname';
$ FLUSH PRIVILEGES;
```

Drop/Delete/Remove a user:
```
$ DROP USER ‘username’@‘hostname’;
```

Note:
"hostname" could be ```localhost```,  ```%``` etc.

### Database and table creation

Show existing databases:
```
SHOW databases;
```

Create a new database:
```
$ CREATE DATABASE db_name
```

Use database:
```
USE db_name;
```

Show existing tables of a connected database:
```
SHOW tables;
```

Create a table(users) to the database:
```
CREATE TABLE users (
  id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  firstname VARCHAR(32) NOT NULL,
  lastname VARCHAR(32) NOT NULL,
  email VARCHAR(50),
  create_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
)
```

### Database character set encoding
Create database specifying a charset(default charset is ```latin1```):
```
mysql> CREATE DATABASE dbname DEFAULT CHARACTER SET utf8mb4 DEFAULT COLLATE utf8mb4_unicode_ci;
```

Check charset of all database from root user:
```
mysql> SELECT SCHEMA_NAME 'database', default_character_set_name 'charset', DEFAULT_COLLATION_NAME 'collation' FROM information_schema.SCHEMATA;
```

Change charset of an exsiting database:
```
mysql> ALTER DATABASE my_test_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```
Note: It will only provides a default for future tables.

Convert existing latin1 tables:
```
mysql> ALTER TABLE tbl CONVERT TO CHARACTER SET utf8mb4;
```
FYI, changes the definition and actively changes the necessary bytes in the columns.

Convert specifi column of latin1 tables:
```
mysql> ALTER TABLE tbl MODIFY col1 ... CHARACTER SET utf8mb4;
```

### Auto increment value reset or change

Delete will not reset the auto increment:
```
$ DELETE FROM table_name;
```

Truncate table will reset the auto increment:
```
$ TRUNCATE TABLE table_name;
```
Note: Use TRUNCATE to empty a table if table data is huge.

Directly reset the auto increment column value:
```
$ ALTER TABLE table_name auto_increment=1
or
$ ALTER TABLE table_name auto_increment=1000
```

### Database constraints

Disbale/Enable foreign key check:
```
SET FOREIGN_KEY_CHECKS = 0;
TRUNCATE table $table_name;
SET FOREIGN_KEY_CHECKS = 1;
```

### Export and import) database

Dump a specific/single database:
```
$ mysqldump -u [username] -p db_name > db_backup.sql
```

Dump all database:
``` 
$ mysqldump -u [username] -p --all-databases > all_db_backup.sql
```

Dump and auto-compressing using gzip (need when db size is large):
```
$ mysqldump -u [username] -p db_name | gzip > db_backup.sql.gz
```

Dump db remotely:
```
$ mysqldump -P 3306 -h [ip_address] -u [username] -p db_name > db_backup.sql
```

Import dumped database:
```
$ mysql -u [username] -p db_name < db_backup.sql;
```

Dump with entering password in shell command:
```
$ mysqldump -u [username] -p[pass] db_name | gzip > db_backup.sql.gz
```

Note:
- Enter password when prompts in the shell after running the any of the above command.
- You can even pass the password direclty in the commnad, Which is strictly prohibited.

Dump specifying max packet size:
```
$ mysqldump --max_allowed_packet=100M -uroot -p db_name > db_name.sql
```

### Troubleshooting

Users details info:
```
$ SELECT  * FROM mysql.user;
$ SELECT User, Host FROM mysql.user
$ SELECT User, Host, Password FROM mysql.user;
```

Update user hostname(accessability from hosts):
```
$ UPDATE mysql.user SET Host='%' WHERE Host='localhost' AND User='user_name';
$ FLUSH PRIVILEGES;
```

