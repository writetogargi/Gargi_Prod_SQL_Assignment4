```bash
docker pull mysql/mysql-server:latest
```
```bash
docker run --name=mysql699 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql/mysql-server:8.0
```

```bash
docker ps -a
```



```bash
docker exec -it mysql699 mysql -uroot -p

```

```bash
docker stop mysql699
```

```bash
#delete
docker rm mysql699
```



> mysql> show databases;
> +--------------------+
> | Database           |
> +--------------------+
> | information_schema |
> | mysql              |
> | performance_schema |
> | sys                |
> +--------------------+
> 4 rows in set (0.00 sec)
>
> mysql> 

```sql
create database lab4db;
```

> Query OK, 1 row affected (0.01 sec)

```sql
use lab4db;
```

> Database changed

```sql
create table PASSENGER(
   passenger_id INT NOT NULL AUTO_INCREMENT,
   Passenger_name varchar(20), 
   Category       varchar(20),
   Gender         varchar(20),
   Boarding_City  varchar(20),
   Destination_City   varchar(20),
   Distance            int,
   Bus_Type    varchar(20),
   PRIMARY KEY ( passenger_id )
);
```

> Query OK, 0 rows affected (0.02 sec)

> mysql> desc PASSENGER;
> +------------------+-------------+------+-----+---------+----------------+
> | Field            | Type        | Null | Key | Default | Extra          |
> +------------------+-------------+------+-----+---------+----------------+
> | passenger_id     | int         | NO   | PRI | NULL    | auto_increment |
> | Passenger_name   | varchar(20) | YES  |     | NULL    |                |
> | Category         | varchar(20) | YES  |     | NULL    |                |
> | Gender           | varchar(20) | YES  |     | NULL    |                |
> | Boarding_City    | varchar(20) | YES  |     | NULL    |                |
> | Destination_City | varchar(20) | YES  |     | NULL    |                |
> | Distance         | int         | YES  |     | NULL    |                |
> | Bus_Type         | varchar(20) | YES  |     | NULL    |                |
> +------------------+-------------+------+-----+---------+----------------+
> 8 rows in set (0.00 sec)

```sql
create table PRICE
(
	price_id INT NOT NULL AUTO_INCREMENT,
    Bus_Type   varchar(20),
    Distance   int,
    Price      int,
    PRIMARY KEY ( price_id )
);
```

> Query OK, 0 rows affected (0.03 sec)

> mysql> desc PRICE;
> +----------+-------------+------+-----+---------+----------------+
> | Field    | Type        | Null | Key | Default | Extra          |
> +----------+-------------+------+-----+---------+----------------+
> | price_id | int         | NO   | PRI | NULL    | auto_increment |
> | Bus_Type | varchar(20) | YES  |     | NULL    |                |
> | Distance | int         | YES  |     | NULL    |                |
> | Price    | int         | YES  |     | NULL    |                |
> +----------+-------------+------+-----+---------+----------------+
> 4 rows in set (0.00 sec)
>
> mysql> 

```sql
#PASSENGER
insert into PASSENGER values(1, 'Sejal','AC','F','Bengaluru','Chennai',350,'Sleeper');
insert into PASSENGER values(2, 'Anmol','Non-AC','M','Mumbai','Hyderabad',700,'Sitting');
insert into PASSENGER values(3, 'Pallavi','AC','F','panaji','Bengaluru',600,'Sleeper');
insert into PASSENGER values(4, 'Khusboo','AC','F','Chennai','Mumbai',1500,'Sleeper');
insert into PASSENGER values(5, 'Udit','Non-AC','M','Trivandrum','panaji',1000,'Sleeper');
insert into PASSENGER values(6, 'Ankur','AC','M','Nagpur','Hyderabad',500,'Sitting');
insert into PASSENGER values(7, 'Hemant','Non-AC','M','panaji','Mumbai',700,'Sleeper');
insert into PASSENGER values(8, 'Manish','Non-AC','M','Hyderabad','Bengaluru',500,'Sitting');
insert into PASSENGER values(9, 'Piyush','AC','M','Pune','Nagpur',700,'Sitting');
```



```sql
select * from PASSENGER;
```





```sql
#PRICE
insert into PRICE values(1, 'Sleeper',350,770);
insert into PRICE values(2, 'Sleeper',500,1100);
insert into PRICE values(3, 'Sleeper',600,1320);
insert into PRICE values(4, 'Sleeper',700,1540);
insert into PRICE values(5, 'Sleeper',1000,2200);
insert into PRICE values(6, 'Sleeper',1200,2640);
insert into PRICE values(7, 'Sleeper',1500,2700);
insert into PRICE values(8, 'Sitting',500,620);
insert into PRICE values(9, 'Sitting',600,744);
insert into PRICE values(10, 'Sitting',700,868);
insert into PRICE values(11, 'Sitting',1000,1240);
insert into PRICE values(12, 'Sitting',1200,1488);
insert into PRICE values(13, 'Sitting',1500,1860);
###########################################
select * from PRICE;
```

##### 3.

```sql
select Gender, count(Gender) FROM PASSENGER where Distance>=600 group by Gender ;
```

> +--------+---------------+
> | Gender | count(Gender) |
> +--------+---------------+
> | M      |             4 |
> | F      |             2 |
> +--------+---------------+
> 2 rows in set (0.01 sec)

###### 4.

```sql
select min(PRICE) from PRICE where Bus_Type = 'Sleeper';
```

###### 5.

```SQL
select Passenger_Name FROM PASSENGER where Passenger_Name like 'S%' order by Passenger_Name;
```



6.

```sql
select a.Passenger_name,a.Boarding_City,a.Destination_City,a.Bus_type,b.Price from PASSENGER a , PRICE b where (a.Bus_Type = b.Bus_Type and a.Distance = b.Distance);
```



> +----------------+---------------+------------------+----------+-------+
> | Passenger_name | Boarding_City | Destination_City | Bus_type | Price |
> +----------------+---------------+------------------+----------+-------+
> | Sejal          | Bengaluru     | Chennai          | Sleeper  |   770 |
> | Pallavi        | panaji        | Bengaluru        | Sleeper  |  1320 |
> | Hemant         | panaji        | Mumbai           | Sleeper  |  1540 |
> | Udit           | Trivandrum    | panaji           | Sleeper  |  2200 |
> | Khusboo        | Chennai       | Mumbai           | Sleeper  |  2700 |
> | Manish         | Hyderabad     | Bengaluru        | Sitting  |   620 |
> | Ankur          | Nagpur        | Hyderabad        | Sitting  |   620 |
> | Piyush         | Pune          | Nagpur           | Sitting  |   868 |
> | Anmol          | Mumbai        | Hyderabad        | Sitting  |   868 |
> +----------------+---------------+------------------+----------+-------+
> 9 rows in set (0.00 sec)



##### 7.

```sql
Select a.Passenger_name,b.Price from PASSENGER a ,PRICE b where (a.Bus_Type = "Sitting" and b.Bus_Type = "Sitting" and a.Distance = 700 and b.Distance=700);
```

> +----------------+-------+
> | Passenger_name | Price |
> +----------------+-------+
> | Piyush         |   868 |
> | Anmol          |   868 |
> +----------------+-------+
> 2 rows in set (0.00 sec)



###### 8.

```sql
SELECT Price FROM PRICE where distance=(SELECT Distance FROM PASSENGER where passenger_name = "Pallavi");
```



> +-------+
> | Price |
> +-------+
> |  1320 |
> |   744 |
> +-------+
> 2 rows in set (0.00 sec)



##### 9.

```SQL
SELECT distinct(Distance) FROM PASSENGER order by distance desc;
```

> +----------+
> | Distance |
> +----------+
> |     1500 |
> |     1000 |
> |      700 |
> |      600 |
> |      500 |
> |      350 |
> +----------+
> 6 rows in set (0.00 sec)



###### 10.



```SQL
with total as ( select sum(distance) as total from PASSENGER)
    select passenger_Name,(distance / total.total)*100 as percentage_travel from PASSENGER,total ;
```

> +----------------+-------------------+
> | passenger_Name | percentage_travel |
> +----------------+-------------------+
> | Sejal          |            5.3435 |
> | Anmol          |           10.6870 |
> | Pallavi        |            9.1603 |
> | Khusboo        |           22.9008 |
> | Udit           |           15.2672 |
> | Ankur          |            7.6336 |
> | Hemant         |           10.6870 |
> | Manish         |            7.6336 |
> | Piyush         |           10.6870 |
> +----------------+-----



###### 11.

```sql
SELECT Distance, Price,
CASE 
WHEN
 Price > 1000 THEN "Expensive"
 WHEN PRICE <1000 and PRICE > 500 THEN "Average Cost"
 ELSE "cheap" END as Cost FROM PRICE;

```



> - +----------+-------+--------------+
> - | Distance | PRICE | Cost         |
> - +----------+-------+--------------+
> - |      350 |   770 | Average Cost |
> - |      500 |  1100 | Expensive    |
> - |      600 |  1320 | Expensive    |
> - |      700 |  1540 | Expensive    |
> - |     1000 |  2200 | Expensive    |
> - |     1200 |  2640 | Expensive    |
> - |     1500 |  2700 | Expensive    |
> - |      500 |   620 | Average Cost |
> - |      600 |   744 | Average Cost |
> - |      700 |   868 | Average Cost |
> - |     1000 |  1240 | Expensive    |
> - |     1200 |  1488 | Expensive    |
> - |     1500 |  1860 | Expensive    |
> - +----------+-------+--------------+
> - 13 rows in set (0.00 sec)
>
> 
>
> --X--