## SQL 语法

> 一个数据库通常包含一个或多个表，每个表有一个名字标识，表包含带有数据的记录(行)。

**SQL对大小写不敏感**

-   **SELECT**  - 从数据库中提取数据
-   **UPDATE**  - 更新数据库中的数据
-   **DELETE**  - 从数据库中删除数据
-   **INSERT INTO**  - 向数据库中插入新数据
-   **CREATE DATABASE**  - 创建新数据库
-   **ALTER DATABASE**  - 修改数据库
-   **CREATE TABLE**  - 创建新表
-   **ALTER TABLE**  - 变更（改变）数据库表
-   **DROP TABLE**  - 删除表
-   **CREATE INDEX**  - 创建索引（搜索键）
-   **DROP INDEX**  - 删除索引



## SQL SELECT DISTINCT 语句

	SELECT DISTINCT 语句用于返回唯一不同的值
	在表中，一个列可能会包含多个重复值，有时您也许仅仅列出不同的distinct的值。
	
    SELECT DISTINCT _column_name_,_column_name_  
    FROM  _table_name_;


## SQL WHERE 子句

WHERE 子句用于提取那些满足指定条件的记录。

    SELECT _column_name_,_column_name_  
    FROM _table_name_  
    WHERE _column_name operator value_;


## SQL—AND & OR 运算符

如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。
如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。

    SELECT * FROM  Websites  
    WHERE  country='CN'  
    AND  alexa > 50;


## ORDER BY 关键字

ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。

ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

    SELECT * FROM  Websites
    ORDER  BY  alexa  DESC;

	order by 多列
	SELECT * FROM  Websites
	ORDER  BY  country,alexa;


## SQL INSERT INTO 语句

INSERT INTO 语句用于向表中插入新记录。

### SQL INSERT INTO 语法

INSERT INTO 语句可以有两种编写形式。

第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

    INSERT INTO  _table_name_  
    VALUES (_value1_,_value2_,_value3_,...);

第二种形式需要指定列名及被插入的值：

    INSERT INTO  _table_name_  (_column1_,_column2_,_column3_,...)  
    VALUES (_value1_,_value2_,_value3_,...);
	
	实例：
    INSERT  INTO  Websites  (name, url, alexa, country)  
    VALUES  ('百度','https://www.baidu.com/','4','CN');


## SQL UPDATE 语句

UPDATE 语句用于更新表中已存在的记录。

### SQL UPDATE 语法

		UPDATE table_name
		SET column1=value1, column2=value2,...
		Where some_column=some_value;

		实例
		UPDATE Websites
		SET alexa='5000', country='USA'
		WHERE name='GISinfo';


## SQL DELETE 语句

DELETE 语句用于删除表中的行。

### SQL DELETE 语法

    DELETE FROM  _table_name_  
    WHERE  _some_column_=_some_value_;
    
    实例
    DELETE FROM Websites
    WHERE name='Facebook' AND country='USA';


## SQL  SELECT TOP, LIMIT, ROWNUM  子句

## SQL SELECT TOP 子句

SELECT TOP 子句用于规定要返回的记录的数目。

SELECT TOP 子句对于拥有数千条记录的大型表来说，是非常有用的。


1. MySQL语法：

	    SELECT column_name(s) 
	    FROM table_name LIMIT number;

		实例：
		SELECT *
		From Persons
		LIMIT 5;
		
2. Oracle 语法：

	    SELECT column_name(s)
	    FROM table_name
	    WHERE ROWNUM <= number;


## SQL LIKE 操作符

LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。

    SELECT _column_name(s)_  
    FROM _table_name_  
    WHERE _column_name_ LIKE _pattern_;

    SELECT * FROM Websites  
    WHERE name LIKE 'G%';

		Results:
		Google| https://www.google.com/ |1 |USA|


## SQL 约束（Constraints）

-   **NOT NULL**  - 指示某列不能存储 NULL 值。
-   **UNIQUE**  - 保证某列的每行必须有唯一的值。
-   **PRIMARY KEY**  - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
-   **FOREIGN KEY**  - 保证一个表中的数据匹配另一个表中的值的参照完整性。
-   **CHECK**  - 保证列中的值符合指定的条件。
-   **DEFAULT**  - 规定没有给列赋值时的默认值。
