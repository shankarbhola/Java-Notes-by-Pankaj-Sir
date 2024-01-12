# JDBC # 
**Java Database Connectivity**

* MySQL Database
* MongoDB
* Apache Derby
* Oracle Database
* etc..

**MySQL Database Installation**
Go to https://dev.mysql.com/downloads/windows/installer/8.0.html
Download mysql-installer-community and install

* create new sql connection 
* login 
**Create new database**

```sql
create database nov_db
```
**Use database**
```sql
use nov_db
```
**Create a table**
```sql
create table registration
(
    name varchar(45),
    city varchar(45),
    email varchar(128),
    mobile varchar(10)
    
)
```
insert value in to table
```sql
insert into registration values
(
	'mike', 'chennai', 'mike@gmail.com', '123456789' 
)
```
**View Values**
```sql
select * from registration
```
```sql
select name, city from registration
```

```mermaid
graph LR

A[Java Code <br>]
B[Database] 
C{{Connector J}}
A<--->C
C<--->B

```

Go to https://dev.mysql.com/downloads/connector/j/
Download connectoe J
* Extract the zip file 
* copy the mysql-connector-j jar file
* open eclips and create a java project
* create a folder named "lib" under the java project
* paste mysql-connector-j jar file inside lib folder