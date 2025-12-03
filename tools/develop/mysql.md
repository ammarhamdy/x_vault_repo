


# Install MySQL
```shell
sudo apt install mysql-server
```

# Log in to MySQL
```
sudo mysql -u root
```

# Exit
```shell
exit;
```

# Restore the SQL backup

```shell
mysql -u root mydb < backup.sql
```

```shell
mysql -u username -p mydb < backup.sql
```


# Verify
```shell
mysql -u root
SHOW DATABASES;
USE mydb;
SHOW TABLES;
```


# Import the SQL file into that database

```
sudo mysql -u root
CREATE DATABASE promatecms;
exit;
sudo mysql -u root promatecms < mysql-promatecms_db.sql
```

```
sudo mysql -u root
USE promatecms;
SHOW TABLES;
```