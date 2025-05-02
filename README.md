# netology_12-2
# Домашнее задание к занятию «Работа с данными (DDL/DML)»

Задание можно выполнить как в любом IDE, так и в командной строке.

## Задание 1

* 1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
* 1.2. Создайте учётную запись sys_temp.
* 1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
* 1.4. Дайте все права для пользователя sys_temp.
* 1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
* 1.6. Переподключитесь к базе данных от имени sys_temp.  
Для смены типа аутентификации с sha2 используйте запрос:  
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';  
* 1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.
* 1.8. Восстановите дамп в базу данных.
* 1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

## Решение 1

*  1.1.	Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
```
sudo apt install wget lsb-release gnupg
wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.34-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.34-1_all.deb
sudo apt update
sudo apt install mysql-server
sudo systemctl status mysql
sudo systemctl enable mysql
mysql -u root –p
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-7.JPG)

*  1.2.	Создайте учётную запись sys_temp.
```
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-8.JPG) 

* 1.3.	Выполните запрос на получение списка пользователей в базе данных. (скриншот)
```
SELECT user FROM mysql.user;
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-9.JPG) 

* 1.4.	Дайте все права для пользователя sys_temp.
```
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-10.JPG) 

* 1.5.	Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
```
SELECT * FROM information_schema.user_privileges WHERE GRANTEE="'sys_temp'@'localhost'";
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-11.JPG)
```
+------------------------+---------------+------------------------------+--------------+
| GRANTEE                | TABLE_CATALOG | PRIVILEGE_TYPE               | IS_GRANTABLE |
+------------------------+---------------+------------------------------+--------------+
| 'sys_temp'@'localhost' | def           | SELECT                       | YES          |
| 'sys_temp'@'localhost' | def           | INSERT                       | YES          |
| 'sys_temp'@'localhost' | def           | UPDATE                       | YES          |
| 'sys_temp'@'localhost' | def           | DELETE                       | YES          |
| 'sys_temp'@'localhost' | def           | CREATE                       | YES          |
| 'sys_temp'@'localhost' | def           | DROP                         | YES          |
| 'sys_temp'@'localhost' | def           | RELOAD                       | YES          |
| 'sys_temp'@'localhost' | def           | SHUTDOWN                     | YES          |
| 'sys_temp'@'localhost' | def           | PROCESS                      | YES          |
| 'sys_temp'@'localhost' | def           | FILE                         | YES          |
| 'sys_temp'@'localhost' | def           | REFERENCES                   | YES          |
| 'sys_temp'@'localhost' | def           | INDEX                        | YES          |
| 'sys_temp'@'localhost' | def           | ALTER                        | YES          |
| 'sys_temp'@'localhost' | def           | SHOW DATABASES               | YES          |
| 'sys_temp'@'localhost' | def           | SUPER                        | YES          |
| 'sys_temp'@'localhost' | def           | CREATE TEMPORARY TABLES      | YES          |
| 'sys_temp'@'localhost' | def           | LOCK TABLES                  | YES          |
| 'sys_temp'@'localhost' | def           | EXECUTE                      | YES          |
| 'sys_temp'@'localhost' | def           | REPLICATION SLAVE            | YES          |
| 'sys_temp'@'localhost' | def           | REPLICATION CLIENT           | YES          |
| 'sys_temp'@'localhost' | def           | CREATE VIEW                  | YES          |
| 'sys_temp'@'localhost' | def           | SHOW VIEW                    | YES          |
| 'sys_temp'@'localhost' | def           | CREATE ROUTINE               | YES          |
| 'sys_temp'@'localhost' | def           | ALTER ROUTINE                | YES          |
| 'sys_temp'@'localhost' | def           | CREATE USER                  | YES          |
| 'sys_temp'@'localhost' | def           | EVENT                        | YES          |
| 'sys_temp'@'localhost' | def           | TRIGGER                      | YES          |
| 'sys_temp'@'localhost' | def           | CREATE TABLESPACE            | YES          |
| 'sys_temp'@'localhost' | def           | CREATE ROLE                  | YES          |
| 'sys_temp'@'localhost' | def           | DROP ROLE                    | YES          |
| 'sys_temp'@'localhost' | def           | FLUSH_TABLES                 | YES          |
| 'sys_temp'@'localhost' | def           | FLUSH_USER_RESOURCES         | YES          |
| 'sys_temp'@'localhost' | def           | AUDIT_ADMIN                  | YES          |
| 'sys_temp'@'localhost' | def           | FLUSH_OPTIMIZER_COSTS        | YES          |
| 'sys_temp'@'localhost' | def           | REPLICATION_APPLIER          | YES          |
| 'sys_temp'@'localhost' | def           | FLUSH_STATUS                 | YES          |
| 'sys_temp'@'localhost' | def           | TELEMETRY_LOG_ADMIN          | YES          |
| 'sys_temp'@'localhost' | def           | TABLE_ENCRYPTION_ADMIN       | YES          |
| 'sys_temp'@'localhost' | def           | SYSTEM_USER                  | YES          |
| 'sys_temp'@'localhost' | def           | RESOURCE_GROUP_ADMIN         | YES          |
| 'sys_temp'@'localhost' | def           | SHOW_ROUTINE                 | YES          |
| 'sys_temp'@'localhost' | def           | SERVICE_CONNECTION_ADMIN     | YES          |
| 'sys_temp'@'localhost' | def           | BINLOG_ENCRYPTION_ADMIN      | YES          |
| 'sys_temp'@'localhost' | def           | RESOURCE_GROUP_USER          | YES          |
| 'sys_temp'@'localhost' | def           | INNODB_REDO_LOG_ENABLE       | YES          |
| 'sys_temp'@'localhost' | def           | ROLE_ADMIN                   | YES          |
| 'sys_temp'@'localhost' | def           | PASSWORDLESS_USER_ADMIN      | YES          |
| 'sys_temp'@'localhost' | def           | TRANSACTION_GTID_TAG         | YES          |
| 'sys_temp'@'localhost' | def           | PERSIST_RO_VARIABLES_ADMIN   | YES          |
| 'sys_temp'@'localhost' | def           | BINLOG_ADMIN                 | YES          |
| 'sys_temp'@'localhost' | def           | SYSTEM_VARIABLES_ADMIN       | YES          |
| 'sys_temp'@'localhost' | def           | GROUP_REPLICATION_ADMIN      | YES          |
| 'sys_temp'@'localhost' | def           | BACKUP_ADMIN                 | YES          |
| 'sys_temp'@'localhost' | def           | REPLICATION_SLAVE_ADMIN      | YES          |
| 'sys_temp'@'localhost' | def           | APPLICATION_PASSWORD_ADMIN   | YES          |
| 'sys_temp'@'localhost' | def           | SESSION_VARIABLES_ADMIN      | YES          |
| 'sys_temp'@'localhost' | def           | INNODB_REDO_LOG_ARCHIVE      | YES          |
| 'sys_temp'@'localhost' | def           | ENCRYPTION_KEY_ADMIN         | YES          |
| 'sys_temp'@'localhost' | def           | CLONE_ADMIN                  | YES          |
| 'sys_temp'@'localhost' | def           | CONNECTION_ADMIN             | YES          |
| 'sys_temp'@'localhost' | def           | XA_RECOVER_ADMIN             | YES          |
| 'sys_temp'@'localhost' | def           | FLUSH_PRIVILEGES             | YES          |
| 'sys_temp'@'localhost' | def           | GROUP_REPLICATION_STREAM     | YES          |
| 'sys_temp'@'localhost' | def           | AUTHENTICATION_POLICY_ADMIN  | YES          |
| 'sys_temp'@'localhost' | def           | SENSITIVE_VARIABLES_OBSERVER | YES          |
| 'sys_temp'@'localhost' | def           | SET_ANY_DEFINER              | YES          |
| 'sys_temp'@'localhost' | def           | ALLOW_NONEXISTENT_DEFINER    | YES          |
| 'sys_temp'@'localhost' | def           | OPTIMIZE_LOCAL_TABLE         | YES          |
| 'sys_temp'@'localhost' | def           | FIREWALL_EXEMPT              | YES          |
| 'sys_temp'@'localhost' | def           | AUDIT_ABORT_EXEMPT           | YES          |
+------------------------+---------------+------------------------------+--------------+
70 rows in set (0.00 sec)
```

* 1.6.	Переподключитесь к базе данных от имени sys_temp.
```
SYSTEM mysql -u sys_temp -p
SELECT user();
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-12.JPG)
 
* 1.7.	По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.
```
wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
```
* 1.8.	Восстановите дамп в базу данных.
```
source /home/eskin/sakila-db/sakila-schema.sql
source /home/eskin/sakila-db/sakila-data.sql
SHOW DATABASES;
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-13.JPG)
 
* 1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
```
SHOW TABLES;
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-14.JPG) 
 
## Задание 2

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц.  
Пример: (скриншот/текст)  
```
Название таблицы | Название первичного ключа
customer         | customer_id
```
## Решение 2

```
+---------------+--------------+
| TABLE_NAME    | COLUMN_NAME  |
+---------------+--------------+
| actor         | actor_id     |
| address       | address_id   |
| category      | category_id  |
| city          | city_id      |
| country       | country_id   |
| customer      | customer_id  |
| film          | film_id      |
| film_actor    | actor_id     |
| film_actor    | film_id      |
| film_category | film_id      |
| film_category | category_id  |
| film_text     | film_id      |
| inventory     | inventory_id |
| language      | language_id  |
| payment       | payment_id   |
| rental        | rental_id    |
| staff         | staff_id     |
| store         | store_id     |
+---------------+--------------+
```
```
SELECT TABLE_NAME, COLUMN_NAME FROM INFORMATION_SCHEMA.key_column_usage WHERE table_schema = 'sakila' AND CONSTRAINT_NAME = 'PRIMARY';
```
![](https://github.com/eskin-igor/netology_12-2/blob/main/12-2/12-2-1-17.JPG)
