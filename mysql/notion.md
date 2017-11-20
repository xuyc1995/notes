# SQL
+ MySQL====RDBMS数据库程序
+ RDBMS指关系型数据库管理系统
+ RDBMS中的数据存储在被称为表（tables）的数据库对象中
+ 表示相关的数据项的集合，由列和行组成
+ SQL对大小写不敏感
## SQL DML和DDL
+ SQL分为两部分：数据操作语言（DML）和数据定义语言（DDL）
+ 查询和更新指令构成了SQL的DML部分：
    + SELECT---从数据库表中获取数据
    + UPDATE---更新数据库表中的数据
    + DELETE---从数据库表中删除数据
    + INSERT INTO---向数据库表中插入数据
+ SQL的数据定义语言（DDL）使我们有能力创建或者删除表格。也可以定义索引，规定表之间的链接，施加表之间的约束
    + CREATE DATABASE--创建新数据库
    + ALTER DATABASE--修改数据库
    + CREATE TABLE--创建新表
    + ALTER TABLE--变更（改变）数据库表
    + DROP TABLE--删除表
    + CREATE INDEX--创建索引（搜索键）
    + DROP INDEX--删除索引
## SELECT语句
+ SELECT 列名称 FROM 表名称
+ SELECT * FROM 表名称--*是选取所有列的快捷键
+ ex:SELECT LastName,FirstName FROM PERSONS
## SELECT DISTINCT
+ DISTINCT 用于返回唯一不同的值（列中若有多个相同的，则返回去重后的）
+ SELECT DISTINCT 列名称 FROM 表名称
## WHERE
+ 如需有条件地从表中选取数据，可将WHERE子句添加到SELECT语句
+ SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
+ 操作符
    + <>---不等于---某些用!=
    + BETWEEN---在某个范围内
    + LIKE---搜索某种形式
+ ex：SELECT * FROM Persons WHERE City='Beijing'
## AND 和OR 运算符
+ 如果第一个条件和第二个条件都成立，则AND运算符显示一条记录
+ 如果第一个条件和第二个条件中只要有一个成立，则OR运算符显示一条记录
+ ex: SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'
+ ex: SELECT * FROM Persons WHERE FirstName='Thomas' OR FirstName='Carter'
+ ex: SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='Carter') AND LastName='Carter'
## ORDER BY 语句
+ 用于根据指定的列对结果集进行排序
+ ORDER BY语句默认按照升序对记录进行排序
+ DESC关键字则为按照降序对记录进行排序
+ ex：SELECT Company, OrderNumber FROM Orders ORDER BY Company（顺序）
+ ex：SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC(倒序)
+ ex: 以字幕顺序显示公司名称Company 并以数字顺序显示顺序号
    + SELECT Company, OrderNumber FROM Orders ORDER BY Company, OrderNumber
## INSERT INTO
+ 用于向表格中插入新的行
+ INSERT INTO 表名称 VALUES（值1，值2，...）
+ INSERT INTO table_name (列1，列2) VALUES (值1，值2，值3，...)
+ 插入新行：INSERT INTO Persons VALUES（‘11’，‘22’）
+ 插入指定列：INSERT INTO Persons （LastName，Address）VALUES ('willson','abs') 
## Update
+ 用于修改表中的数据
+ UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
    + ex: UPDATE Person SET FirstName = ‘aaa’ WHERE FirstName = 'jiu'
+ 更新某一行中的一个列
    + UPDATE Person SET FirstName = ‘aa’ WHERE LastName ='bb'
+ 更新某一行中的若干列
    + UPDATE Person SET FirstName = ‘aa’,Address='gag' WHERE LastName ='bb'
## DELETE
+ 用于删除表中的行
+ DELETE FROM 表名称 WHERE 列名称 = 值
    + ex：DELETE FROM Person WHERE LastName = 'Wilson'   
+ 删除所有行
    + DELETE FROM table_name
    + DELETE * FROM table_name
## TOP 子句
+ 用来规定要返回的记录的数目
+ mySQL用法
```
SELECT Column_name(s) 
FROM table_name
LIMIT number

ex:
SELECT *
FROM Persons
LIMIT 5 (返回5条)
```
## LIKE操作符
+ LIKE用于在WHERE子句中搜索列中的指定模式
```
SELECT Column_name(s)
FROM table_name
WHERE column_name LIKE pattern
```
## SQL通配符
+ % 替代一个或者多个字符
+ _ 仅替代一个字符
+ [charlist] 字符列中的任何单一字符
+ [^charlist][!charlist] 不再字符列中的任何单一字符
```
我们希望从上面的 "Persons" 表中选取居住的城市不以 "A" 或 "L" 或 "N" 开头的人：
SELECT * FROM Persons
WHERE City LIKE '[!ALN]%'
```
## IN 操作符
+ 允许在WHERE子句中规定多个值
```
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...)
从上表中选取姓氏为 Adams 和 Carter 的人：
SELECT * FROM Persons
WHERE LastName IN ('Adams','Carter')
```
## BETWEEN 
+ BETWEEN...AND 选取介于两个值之间的数据范围，值可以是文本或者日期
```
SELECT column_name(s)
FROM table_name
WHERE column_name
(NOT) BETWEEN value1 AND value2
```
## Alias(别名)
+ 可以为列名称和表名称指定别名Alias
```
表的SQL Alias语法
SELECT column_name(s)
FROM table_name
AS alias_name
列的SQL Alias语法
SELECT column_name AS alias_name
FROM table_name
ex：假设有两个表，分别是Persons和Product_Orders，分别为他们指定别名p和po，现在希望列出JohnAdams的所有订单
SELECT po.OrderID, p.LastName, p.FirstName
FROM Persons AS p, Product_Orders AS po
WHERE p.LastName='Adams' AND p.FirstName='John'
```
## SQL Join
+ 用于根据两个或多个表中的列之间的关系，cingulate这些表中查询数据
### join和key
+ 有时我们需要从两个或者更多的表中获取结果，则我们需要执行join
+ 数据库中可以通过键将彼此联系起来，主键（Primary Key）是一个列，在这个列中的每一行的值都是唯一的，在表中，每个主键的值都是唯一的。目的是在不重复每个表中的所有数据的情况下，把表间的数据交叉捆绑在一起
+ 引用两个表：
```
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo 
FROM Persons, Orders
WHERE Persons.Id_p = Orders.Id_P
```
### JOIN 
```
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P = Orders.Id_P
ORDER BY Persons.LastName
```
### 不同的SQL JOIN 　
+ JOIN：如果表中有至少一个匹配，则返回行
+ LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行
+ RIGHT JOIN：即使左表中没有匹配，也从右表返回所有的行
+ FULL JOIN： 只要其中一个表中存在匹配，就返回行
## SQL INNER JOIN
+ 在表中存在至少一个匹配时，INNER JOIN 关键字返回行
```
SELECT column_name(s)
FROM table_name1
INNER JOIN table_name2
ON table_name1.column_name = table_name2.column_name
```
## SQL UNION
+ 用于合并两个或多个SELECT语句的结果集（选取的是不同的值，不重复，UNION ALL重复）
## SELECT INTO
+ 从一个表中选取数据，然后把数据插入另一个表中
+ 用于创建表的备份复件或者用于对记录进行存档
## CREATE DATABASE
+ CREATE DATABASE database_name
## CREATE TABLE
```
CREATE TABLE 表名称
(
    列名称1 数据类型,
    列名称2 数据烈性,
    ...
)
```
+ 常见数据类型：
    + integer（size）/int(size)/smallint(size)/tinyint(size)---仅容纳证书，括号内规定数字的最大位数
    + decimal(size,d)/numeric(size,d)---容纳带有小数的数字，size规定数字的最大位数，d规定小数点右侧的最大位数
    + char(size)---容纳固定长度的字符串（可容纳字母，数字及特殊字符），size规定字符串的长度
    + varchar(size)---容纳可变长度的字符串--最大长度是255
    + date（yyyymmdd）---容纳日期
## SQL约束
+ NOT NULL---约束强制列不接受null值，必须包含值，否则无法插入新纪录或者更新记录
    + id_p int NOT NULL
## UNIQUE
+ 约束唯一标识数据库表中的每条记录，UNIQUE和PRIMAEY KEY约束均为列或者列集合提供了唯一性的保证，拥有自定义的UNIQUE约束。
```
Mysql写法：
CREATE TABLE Persons
(
    Id_P int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255),
    UNIQUE (Id_P)
    CONSTRAINT uc_PersonID UNIQUE (Id_P,LastName)---为多个列定义UNIQUE约束
)
撤销UNIQUE
    DROP INDEX uc_PersonID
```
## 
