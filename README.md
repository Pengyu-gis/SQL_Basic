# SQL_Basic

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




## 数据三范式

> 范式是符合某一种设计要求的总结

**1．第一范式(确保每列保持原子性)**

第一范式是最基本的范式。如果数据库表中的**所有字段值都是不可分割的原子值**，就说明该数据库表满足了第一范式。

**2．第二范式(确保表中的每列都和主键相关)**

第二范式在第一范式的基础之上更进一层。第二范式需要确保数据库表中的**每一列都和主键相关**，**而不能只与主键的某一部分相关**（主要针对联合主键而言）。也就是说在一个数据库表中，**一个表中只能保存一种数据**，不可以把多种数据保存在同一张数据库表中。


比如一个订单信息表，因为订单中可能有多种商品，所以要将订单编号和商品编号作为数据库表的联合主键。
![](https://pic002.cnblogs.com/images/2012/270324/2012040114063976.png)

这样就有一个问题，表中是以订单编号和商品作为联合主键，这样表中商品名称、单位、商品价格等信息不与主键相关，而仅仅与商品编号有关，这就违反了数据库的第二范式。

需要对订单信息进行拆分，把商品信息分离到另一个表中，把订单项目表也分离到另一个表中。
![第二范式](https://pic002.cnblogs.com/images/2012/270324/2012040114082156.png)


**3****．第三范式(确保每列都和主键列直接相关,而不是间接相关)**

第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关。

比如在设计一个订单数据表的时候，可以将客户编号作为一个外键和订单表建立相应的关系。而不可以在订单表中添加关于客户其它信息（比如姓名、所属公司等）的字段。如下面这两个表所示的设计就是一个满足第三范式的数据库表。

![第三范式](https://pic002.cnblogs.com/images/2012/270324/2012040114105477.png)







## 一. 索引的作用：
 1. 索引大大减小了服务器需要扫描的数据量
 2. 索引可以帮助服务区避免排序和临时表
 2. 索引可以将随机IO变成顺序IO

## 二. B-Tree索引：

 1. B+Tree：每一个叶子节点都包含指向下一个叶子节点的指针，从而方便叶子节点的范围遍历。
 2. B-Tree通常意味着所有的值都是按顺序存储的，并且每一个叶子页到根的距离相同，很适合查找范围数据。

## 三. 聚集索引：

 - 我们平时建表的时候都会为表加上主键，在某些关系数据库中，如果建表时不指定主键，数据库会拒绝建表的语句执行。
 
 - 给表加上主键后，表在磁盘上的存储结构就由整齐排列的结构变成了树状结构，也就是【平衡树】结构，换句话说，就是整个表就变成了一个索引，这就是所谓的【聚集索引】。

![聚集索引结构图](https://pic01.sq.seqill.cn/uploads/image/20210723/1627025477661748.jpg)

 - 其中树的所有结点(底部除外)的数据都是由主键字段中的数据构成，也就是通常我们指定主键的id字段。最下面部分是真正表中的数据。

## 四. 非聚集索引：

 - 非聚集索引和聚集索引一样，同样是采取平衡树作为索引的数据结构。

 - 索引树结构中各节点的值来自表中的索引字段，假如给user表的name字段加上索引，那么索引就是由name字段中的值构成的，在数据改变时，DBMS需要一直维护索引结构的正确性。

 - 表中多个字段加上索引 ， 那么就会出现多个独立的索引结构，每个索引（非聚集索引）互相之间不存在关联。
![非聚集索引示例](https://img-blog.csdn.net/2018080818551867?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0Nzc3NjAw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## key 与 index

mysql的key和index多少有点令人迷惑，单独的key和其它关键词结合的key(如：primary key)实际表示的意义是不同，这实际上考察对数据库体系结构的了解的。

key 是数据库的物理结构，它包含两层意义和作用:
 1. 约束（偏重于约束和规范数据库的结构完整性），索引（辅助查询用的）。
 2. mysql的key是同时具有constraint和index的意义，这点和其他数据库表现的可能有区别。

index 是数据库的物理结构，它只是辅助查询的，它创建时会在另外的表空间（mysql中的innodb表空间）以一个类似目录的结构存储。 因此，索引只是索引，它不会去约束索引的字段的行为（那是key要做的事情）。


