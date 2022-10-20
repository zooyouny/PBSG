# Create Database and tables 

```
> mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 25
Server version: 8.0.31 Homebrew

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE DATABASE miniter;
Query OK, 1 row affected (0.01 sec)

mysql> USE miniter
Database changed

mysql> CREATE TABLE users (
    -> id INT NOT NULL AUTO_INCREMENT,
    -> name VARCHAR(255) NOT NULL,
    -> email VARCHAR(255) NOT NULL,
    -> hashed_password VARCHAR(255) NOT NULL,
    -> profile VARCHAR(2000) NOT NULL,
    -> created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    -> updated_at TIMESTAMP NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
    -> PRIMARY KEY (id),
    -> UNIQUE KEY email (email)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> CREATE TABLE users_follow_list (
    -> user_id INT NOT NULL,
    -> follow_user_id INT NOT NULL,
    -> created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    -> PRIMARY KEY (user_id, follow_user_id),
    -> CONSTRAINT users_follow_list_user_id_fkey FOREIGN KEY (user_id)REFERENCES users(id),
    -> CONSTRAINT users_follow_list_follow_user_id_fkey FOREIGN KEY (follow_user_id) REFERENCES users(id));
Query OK, 0 rows affected (0.01 sec)

mysql> CREATE TABLE tweets (
    -> id INT NOT NULL AUTO_INCREMENT,
    -> user_id INT NOT NULL,
    -> tweet VARCHAR(300) NOT NULL,
    -> created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    -> PRIMARY KEY (id),
    -> CONSTRAINT tweets_user_id_fkey FOREIGN KEY (user_id) REFERENCES users(id)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+-------------------+
| Tables_in_miniter |
+-------------------+
| tweets            |
| users             |
| users_follow_list |
+-------------------+
3 rows in set (0.00 sec)

mysql> explain users;
+-----------------+---------------+------+-----+-------------------+-----------------------------+
| Field           | Type          | Null | Key | Default           | Extra                       |
+-----------------+---------------+------+-----+-------------------+-----------------------------+
| id              | int           | NO   | PRI | NULL              | auto_increment              |
| name            | varchar(255)  | NO   |     | NULL              |                             |
| email           | varchar(255)  | NO   | UNI | NULL              |                             |
| hashed_password | varchar(255)  | NO   |     | NULL              |                             |
| profile         | varchar(2000) | NO   |     | NULL              |                             |
| created_at      | timestamp     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED           |
| updated_at      | timestamp     | YES  |     | NULL              | on update CURRENT_TIMESTAMP |
+-----------------+---------------+------+-----+-------------------+-----------------------------+
7 rows in set (0.00 sec)

mysql> explain users_follow_list;
+----------------+-----------+------+-----+-------------------+-------------------+
| Field          | Type      | Null | Key | Default           | Extra             |
+----------------+-----------+------+-----+-------------------+-------------------+
| user_id        | int       | NO   | PRI | NULL              |                   |
| follow_user_id | int       | NO   | PRI | NULL              |                   |
| created_at     | timestamp | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED |
+----------------+-----------+------+-----+-------------------+-------------------+
3 rows in set (0.01 sec)

mysql> explain tweets;
+------------+--------------+------+-----+-------------------+-------------------+
| Field      | Type         | Null | Key | Default           | Extra             |
+------------+--------------+------+-----+-------------------+-------------------+
| id         | int          | NO   | PRI | NULL              | auto_increment    |
| user_id    | int          | NO   | MUL | NULL              |                   |
| tweet      | varchar(300) | NO   |     | NULL              |                   |
| created_at | timestamp    | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED |
+------------+--------------+------+-----+-------------------+-------------------+
4 rows in set (0.01 sec)

mysql> exit
Bye
```