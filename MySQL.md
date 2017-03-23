  
## MySQL  
  
### 数据库设计  
  
* 第一范式：数据库表中所有字段都是单一属性，不可再分的。  
* 第二范式：数据库表中不存在非关键字段对任一关键字段的部分函数依赖（解决数据冗余和数据统一问题，即拆分出重复数据）。  
* 第三范式：数据表中存在非关键字段对任意候选关键字段的传递函数依赖。（对分类单独设计数据表存储）  

> 范式数据库设计思想主要是从数据库性能及空间为主进行考虑的，但适当时候应该利用反范式设计思想对数据进行部分冗余，即用空间换时间。
  
### MySql 存储引擎  
    
| 存储引擎 | 事务支持 | 锁粒度 | 优势 | 短板 |    
| --- | --- | --- | --- | --- |    
| MyISAM | 否 | 表级锁 | 高速 SELECT | 高并发 |    
| Merge | 否 | 表级锁 | 水平分表 | 全表搜索 |    
| InnoDB | 是 | MVCC 的行级锁 | 事务处理 | - |    
| Archive | 否 | 行级锁 | 日志 | 随机读写 |    
| Cluster/NDB | 是 | 行级锁 | 高可用性 | - |    
  
```
ISAM、MyISAM、HEAP（也称为MEMORY）、CSV、BLACKHOLE、ARCHIVE
PERFORMANCE_SCHEMA、InnoDB、 Berkeley、Merge、Federated、Cluster/NDB
```

### 连接 mysql  
  
```  
mysql -u root -p root  
```  
  
### 库相关  
  
```  
// 列出所有数据库  
SHOW DATABASES;  
  
// 新建数据库  
CREATE DATABASE `库名`;  
CREATE DATABASE `库名` DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
  
// 删除数据库  
DROP DATABASE  `库名`;  
  
// 查看当前使用的数据库  
SELECT database();  
  
// 选择使用的数据库  
USE `库名`;  
  
// 删除数据库  
DROP DATABASE `库名`;  
  
// 查看当前库中所有表注释  
SELECT table_name, table_comment FROM information_schema.tables WHERE table_schema=`库名`;  
  
// 显示数据库中所有表的元信息  
SHOW TABLE STATUS FROM `库名`;  
SHOW TABLE STATUS FROM `库名` LIKE `关键字`  
```  
  
### 表相关  
  
```  
// 列表数据表  
SHOW TABLES;  
  
// 创建表  
CREATE TABLE IF NOT EXISTS `表名`(  
    `id` int(10) unsigned NOT NULL PRIMARY KEY AUTO_INCREMENT COMMENT '本条记录 ID',  
    `add_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '新增时间',  
    `update_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',  
    `status` tinyint(1) unsigned NOT NULL DEFAULT '1' COMMENT '本条记录状态 1 - 正常 0 - 删除'  
) COMMENT '表注释';  
  
// 删除表  
DROP TABLE `表名`;  
  
// 查看表结构  
SHOW COLUMNS FROM `表名`;  
DESC `表名`; // 同上  
SHOW FULL COLUMNS FROM `表名`; // 相比上条多出编码、权限、注释等信息  
  
// 查看表索引情况  
SHOW INDEX FROM `表名`;  
  
// 添加主键索引  
ALTER TABLE `表名` ADD PRIMARY KEY (`字段名`)  
  
// 添加唯一索引  
ALTER TABLE `表名` ADD UNIQUE (`字段名`)  
  
// 添加普通索引  
ALTER TABLE `表名` ADD INDEX 索引名 (`字段名`)  
  
// 添加全文索引  
ALTER TABLE `表名` ADD FULLTEXT (`字段名`)  
  
// 添加组合索引  
ALTER TABLE `表名` ADD INDEX 索引名 (`字段名 A`, `字段名 B`, `字段名 C`)  
  
// 查看表的创建 sql 语句  
SHOW CREATE TABLE `表名`;  
  
// 修改表注释  
ALTER TABLE `表名` COMMENT '注释';  
  
// 新增字段  
ALTER TABLE `表名` ADD `字段` int(10) unsigned NOT NULL AFTER `字段`;  
  
// 删除字段  
ALTER TABLE `表名` DROP `字段`;  
  
// 修改字段元数据  
ALTER TABLE `表名` MODIFY `字段` varchar(8); // 修改制定字段的元数据  
ALTER TABLE `表名` CHANGE `老字段名` `新字段名` varchar(20) NOT NULL; // 与 MODIFY 一致并可以修改字段名称  
  
// 修改字段默认值  
AlTER TABLE `表名` ALTER `字段` SET DEFAULT '默认值';  
  
// 删除字段默认值  
ALTER TABLE `表名` DROP `字段` DEFAULT;  
  
// 修改表名  
ALTER TABLE `旧表名` RENAME TO `新表名`;  
  
// 清空表  
TRUNCATE TABLE `表名`;  
```  
  
### binlog

```
// 获取 binlog 文件列表
show binary logs;

// 查看第一个 binlog 文件的内容
show binlog events;

// 查看指定 binlog 文件的内容
show binlog events in 'mysql-bin.000002';

// 查看当前正在写入的 binlog 文件
show master status;

// 基于开始/结束时间
mysqlbinlog --start-datetime='2013-09-10 00:00:00' --stop-datetime='2013-09-10 01:01:01' -d 库名二进制文件

// 基于 position 值
mysqlbinlog --start-postion=107 --stop-position=1000 -d 库名二进制文件
```

### 常用查询  
  
```  
// 查询结果默认按行格式打印  
// 查询结果按列格式打印  

SELECT * FROM `表名`\G;  
  
// 根据时间分组  

SELECT DATE_FORMAT(addtime, "%Y-%m-%d") AS days, COUNT(*) AS lively_num  
FROM device_score_lively_xyweather  
WHERE  
    channel_num = 400003  
    AND addtime  
        BETWEEN  
            '2016-06-25 00:00:00'  
        AND  
            '2016-06-28 23:59:59'  
GROUP BY days
ORDER BY lively_num;   

// GROUP BY 后 LIMIT (方式一)

SELECT *
FROM
(
    SELECT casrn, goods_id, store_id, goods_mol_id, goods_name, goods_english_name
    FROM ecm_goods
    WHERE
        store_id IN (1, 2, 3)
        AND set_status&1
        AND ~set_status&16
        AND ~set_status&2
    ORDER BY
        set_status&4 DESC,
        rank DESC
) AS temp
GROUP BY store_id
LIMIT 10

// GROUP BY 后 LIMIT (方式二)

SELECT
    a.*,
    b.deep_path,
    b.filename,
    c.deep_path AS hover_deep_path,
    c.filename AS hover_filename
FROM `icon` a
LEFT JOIN `attachment` b ON a.attachment_id = b.id
LEFT JOIN `attachment` c ON a.hover_attachment_id = c.id
WHERE 5 >
(
    SELECT COUNT(*)
    FROM `icon`
    WHERE `group` = a.`group` AND `id` > a.`id` AND `state` = 1
)
ORDER BY a.`sort` ASC, a.`update_time` DESC
```
  
### 慢查询工具  
  
* mysqldumpslow  
* pt-query-digest  
* explain [query sql] 

### 其他

```
// 查看当前状态
status;

SHOW status;

SHOW processlist;

// 查看索引相关使用情况
EXPLAIN `SQL 语句`

// 强制使用索引
SELECT * FROM `表名` FORCE INDEX (`索引名`) 
``` 

### MySQL5.7 修改密码

```
$ sudo killall -TERM mysqld
$ mysqld_safe --skip-grant-tables & 
$ mysqld_safe --skip-grant-tables --skip-networking &
$ mysql -p
> update mysql.user set authentication_string=password('xxx') where user='root' and Host = 'localhost';
$ sudo service mysql restart
```

### MySQL 远程登录

```
$ mysql -u root -pxxx
> use mysql
> update user set host = '%' where user = 'root';
> select host, user from user;
> FLUSH PRIVILEGES;

$ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
注释 bind-address 127.0.0.1
```

### ACID  

* 事务的原子性(Atomicity)

    > 是指一个事务要么全部执行, 要么不执行.也就是说一个事务不可能只执行了一半就停止了.比如你从取款机取钱, 这个事务可以分成两个步骤:1 划卡, 2 出钱.不可能划了卡, 而钱却没出来.这两步必须同时完成.要么就不完成.

* 事务的一致性(Consistency)

    > 是指事务的运行并不改变数据库中数据的一致性.例如, 完整性约束了 a+b=10, 一个事务改变了 a, 那么 b 也应该随之改变.

* 独立性(Isolation)

    > 事务的独立性也有称作隔离性, 是指两个以上的事务不会出现交错执行的状态.因为这样可能会导致数据不一致.

* 持久性(Durability)

    > 事务的持久性是指事务执行成功以后, 该事务所对数据库所作的更改便是持久的保存在数据库之中，不会无缘无故的回滚.

### MySQL 锁    
    
**行级锁－ InnoDB**    

`特点`：开销大，加锁慢，容易出现死锁；锁粒度最小，发生冲突概率最低，并发度最高。    
注意事项：行锁是通过给索引加锁来实现的，只有通过索引条件检索的数据才能使用到行级锁，否则将使用表锁。    

`死锁`： MyISAM 中是一次性获取所需的全部锁，所以不会出现死锁现象；当 SQL 语句操作了主键索引时，会锁定主键索引；当 SQL 语句操作了非主键索引时，会锁定非主键索引，然后锁定主键索引；在 UPDATE 、 DELETE 操作时， MYSQL 不仅会锁定 WHERE 扫描过的索引，还会锁定相邻的键值（ next － key locking ）    
产生死锁情况：事务 A 锁定主键索引，在等待其他相关索引；事务 B 锁定非主键索引，在等待主键索引。这样就产生了死锁。    

**表级锁－ MyISAM**    

`特点`：开销小，加锁快，不会出现死锁；锁粒度最大，发送冲突概率最大，并发度最低。    

**页级锁－ BDB**    

`特点`：开销和加锁时间介于表锁和行锁之间；会出现死锁，锁粒度适中，并发度一般。    

**隔离级别**    

`脏读`：事务 A 读取了事务 B 还未提交的修改。    

`不可重复读`：两次相同的查询返回了不同的结果。    

`幻读`：两次相同的查询返回了不同的记录条数。    

**乐观锁**    

在事务中，每个读操作不会上锁，但是在执行写操作时候会判断一下在此期间是否有人修改过该数据，如果有，则取消当前更新操作。    

**悲观锁**    

在事务中，每个读操作都会上锁，别人要想更新这个数据需要等待悲观锁结束后才能执行。    

**InnoDB 又分共享锁和排它锁**    

`共享锁`：又称为读锁，是读取操作创建的锁，当数据被加上共享锁后，其他 session 可以并发读取数据，但不能对数据进行修改，不能获取数据上的排他锁，但可以继续加共享锁，只能对数据进行读取操作，不能对数据执行写操作。    

```    
SELECT ＊ FROM table WHERE id = 1 LOCK IN SHARE MODE;    
```    
    
`排他锁`：又称为写锁，当数据被加上排他锁后，其他 session 不能对该数据进行任何加锁操作，也不能进行读写操作。    

```    
SELECT ＊ FROM table WHERE id = 1 FOR UPDATE;    
```

**FOR UPDATE**    

`特点`：仅仅适用于 InnoDB ，并且需要出现在 `BEGIN` 和 `COMMIT` 块中（事务）    

| 上下文 | 锁状态 | 锁描述 |    
| --- | --- | --- |    
| 明确指定主键并存在该记录 | row lock | 行锁 |    
| 明确制定主键但不存在该记录 | no lock | 无锁 |    
| 无主键 | table lock | 表锁 |    
| 主键不明确 | table lock | 表锁 |    
     
表级锁时，不管是否查询到记录，都会锁定表    

### MySQL 的 hint(暗示、提示)

**强制索引 FORCE INDEX**

```
SELECT * FROM table1 FORCE INDEX (field1) …

以上的 SQL 语句只使用建立在 field1 上的索引，而不使用其它字段上的索引。
```

**忽略索引 IGNORE INDEX**

```
SELECT * FROM table1 IGNORE INDEX (field1, field2) …

在上面的 SQL 语句中， table1 表中 field1 和 field2 上的索引不被使用。
```

**关闭查询缓冲 SQL_NO_CACHE**

```
SELECT SQL_NO_CACHE field1, field2 FROM table1;

有一些 SQL 语句需要实时地查询数据，或者并不经常使用(可能一天就执行一两次)
这样就需要把缓冲关了, 不管这条 SQL 语句是否被执行过，服务器都不会在缓冲区中查找，每次都会执行它。
```

**强制查询缓冲 SQL_CACHE**

```
SELECT SQL_CALHE * FROM table1;

如果在 my.ini 中的 query_cache_type 设成 2 ，这样只有在使用了 SQL_CACHE 后，才使用查询缓冲。
```

**优先操作 HIGH_PRIORITY**

```
SELECT HIGH_PRIORITY * FROM table1;

HIGH_PRIORITY 可以使用在 SELECT 和 INSERT 操作中，让 MySQL 知道，这个操作优先进行。
```

**滞后操作 LOW_PRIORITY**

```
UPDATE LOW_PRIORITY table1 SET field1= … WHERE field1= …

LOW_PRIORITY 可以使用在 UPDATE 和 INSERT 操作中，让 MySQL 知道，这个操作滞后。
```

**延时插入 INSERT DELAYED**

```
INSERT DELAYED INTO table1 set field1= …

INSERT DELAYED INTO ，是客户端提交数据给 MySQL ， MySQL 返回 OK 状态给客户端。
而这是并不是已经将数据插入表，而是存储在内存里面等待排队。
当 MySQL 有空余时，再插入。
另一个重要的好处是，来自许多客户端的插入被集中在一起，并被编写入一个块。
这比执行许多独立的插入要快很多。
坏处是，不能返回自动递增的 ID ，以及系统崩溃时， MySQL 还没有来得及插入数据的话，这些数据将会丢失。
```

**强制连接顺序 STRAIGHT_JOIN**

```
SELECT table1.field1, table2.field2 FROM table1 STRAIGHT_JOIN table2 WHERE …

由上面的 SQL 语句可知，通过 STRAIGHT_JOIN 强迫 MySQL 按 table1 、 table2 的顺序连接表。
如果你认为按自己的顺序比 MySQL 推荐的顺序进行连接的效率高的话，就可以通过 STRAIGHT_JOIN 来确定连接顺序。
```

**强制使用临时表 SQL_BUFFER_RESULT**

```
SELECT SQL_BUFFER_RESULT * FROM table1 WHERE …

当我们查询的结果集中的数据比较多时，可以通过 SQL_BUFFER_RESULT 选项强制将结果集放到临时表中
这样就可以很快地释放 MySQL 的表锁(这样其它的 SQL 语句就可以对这些记录进行查询了)
并且可以长时间地为客户端提供大记录集。
```

**分组使用临时表 SQL_BIG_RESULT 和 SQL_SMALL_RESULT**

```
SELECT SQL_BUFFER_RESULT field1, COUNT(*) FROM table1 GROUP BY field1;

一般用于分组或 DISTINCT 关键字，这个选项通知 MySQL
如果有必要，就将查询结果放到临时表中，甚至在临时表中进行排序。
SQL_SMALL_RESULT 比起 SQL_BIG_RESULT 差不多，很少使用。
```

### MySQL 索引

* 单列索引：一个索引只包含一个列，一个表可以有多个单列索引。如主键索引、唯一索引、普通索引
* 组合索引：一个组合索引包含两个或两个以上的列

**普通索引**

> 如果是 CHAR 、 VARCHAR 类型， length 可以小于字段的实际长度，如果是 BLOB 和 TEXT 类型就必须指定长度。

**主键索引**

> 不允许有空值，(在 BTREE 中的 InnoDB 引擎中，主键索引起到了至关重要的地位)
>
> 主键索引建立的规则是 int 优于 varchar ，一般在建表的时候创建，最好是与表的其他字段不相关的列或者是业务不相关的列。一般会设为 int 而且是 AUTO_INCREMENT 自增类型。

**唯一索引**

> 与普通索引类似，但是不同的是唯一索引要求所有的类的值是唯一的，这一点和主键索引一样，但是他允许有空值。

**组合索引**

> 一个表中含有多个单列索引不代表是组合索引，通俗一点讲组合索引是：包含多个字段但是只有索引名称。
>
> 如果你建立了组合索引(nickname_account_createdtime_index) 那么他实际包含的是 3 个索引 (nickname) (nickname ， account) (nickname ， account ， created_time)
>
> 在使用查询的时候遵循 mysql 组合索引的 `最左前缀`。 
>
> 最左前缀：及索引 where 时的条件要按照建立索引的时候字段的排序方式
>
> > * 不按索引最左列开始查询（多列索引）例如 index('c1'， 'c2'， 'c3') where \`c2\` = 'aaa' 不使用索引， where \`c2\` = 'aaa' and \`c3\`='sss' 不能使用索引
> > * 查询中某个列有范围查询，则其右边的所有列都无法使用索引（多列查询）
> > > where \`c1\`= 'xxx' and \`c2\` like = 'aa%' and \`c3\`='sss' 改查询只会使用索引中的前两列，因为 like 是范围查询
> > * 不能跳过某个字段来进行查询，这样利用不到索引
> > > 比如我的 sql 是 explain select * from \`award\` where \`nickname\` > 'rSUQFzpkDz3R' and \`account\` = 'DYxJoqZq2rd7' and \`created_time\` = 1449567822; 
> > >
> > > 那么这时候他使用不到其组合索引。
> > >
> > > 因为我的索引是 (nickname ， account ， created_time)，如果第一个字段出现范围符号的查找，那么将不会用到索引，如果我是第二个或者第三个字段使用范围符号的查找，那么他会利用索引，利用的索引是(nickname)，因为上面说了建立组合索引(nickname ， account ， created_time)，会出现三个索引。

**全文索引**

> 文本字段上(text)如果建立的是普通索引，那么只有对文本的字段内容前面的字符进行索引，其字符大小根据索引建立索引时申明的大小来规定。
>
> 如果文本中出现多个一样的字符，而且需要查找的话，那么其条件只能是 where column lick '%xxxx%' 这样做会让普通索引失效。这个时候全文索引就起到了作用了。
> 
> ALTER TABLE tablename ADD FULLTEXT(column1 ， column2)
有了全文索引，就可以用 SELECT 查询命令去检索那些包含着一个或多个给定单词的数据记录了。
>
> SELECT * FROM tablename WHERE MATCH(column1 ， column2) AGAINST('xxx'， 'sss'， 'ddd') 这条命令将把 column1 和 column2 字段里有 xxx 、 sss 和 ddd 的数据记录全部查询出来。

**使用索引的优点**

* 可以通过建立唯一索引或者主键索引，保证数据库表中每一行数据的唯一性。
* 建立索引可以大大提高检索的数据，以及减少表的检索行数。
* 在表连接的连接条件可以加速表与表直接的相连。
* 在分组和排序字句进行数据检索，可以减少查询时间中分组和排序时所消耗的时间(数据库的记录会重新排序)。
* 建立索引，在查询中使用索引可以提高性能。

**使用索引的缺点**

* 在创建索引和维护索引会耗费时间，随着数据量的增加而增加
* 索引文件会占用物理空间，除了数据表需要占用物理空间之外，每一个索引还会占用一定的物理空间
* 当对表的数据进行 INSERT ， UPDATE ， DELETE 的时候，索引也要动态的维护，这样就会降低数据的维护速度，(建立索引会占用磁盘空间的索引文件。一般情况这个问题不太严重，但如果你在一个大表上创建了多种组合索引，索引文件的会膨胀很快)。

**使用索引需要注意的地方**

> 在建立索引的时候应该考虑索引应该建立在数据库表中的某些列上面哪一些索引需要建立，哪一些所以是多余的。

* 在经常需要搜索的列上，可以加快索引的速度
* 主键列上可以确保列的唯一性
* 在表与表的而连接条件上加上索引，可以加快连接查询的速度
* 在经常需要排序(order by)，分组(group by)和的 distinct 列上加索引可以加快排序查询的时间，  (单独 order by 用不了索引，索引考虑加 where 或加 limit)
* 在一些 where 之后的 < <= > >= BETWEEN IN 以及某个情况下的 like 建立字段的索引(B-TREE)
* like 语句的如果你对 nickname 字段建立了一个索引。当查询的时候的语句是 nickname lick '%ABC%' 那么这个索引讲不会起到作用。而 nickname lick 'ABC%' 那么将可以用到索引
* 索引不会包含 NULL 列，如果列中包含 NULL 值都将不会被包含在索引中，复合索引中如果有一列含有 NULL 值那么这个组合索引都将失效，一般需要给默认值 0 或者 ' ' 字符串
* 使用短索引，如果你的一个字段是 char(32) 或者 int(32)，在创建索引的时候指定前缀长度比如前 10 个字符 (前提是多数值是唯一的)那么短索引可以提高查询速度，并且可以减少磁盘的空间，也可以减少 I/0 操作。
* 不要在列上进行运算，这样会使得 mysql 索引失效，也会进行全表扫描
* 选择越小的数据类型越好，因为通常越小的数据类型通常在磁盘，内存， cpu ，缓存中占用的空间很少，处理起来更快。

**什么情况下不创建索引**

* 查询中很少使用到的列不应该创建索引，如果建立了索引然而还会降低 MySQL 的性能和增大了空间需求。
* 很少数据的列也不应该建立索引，比如一个性别字段 0 或者 1 ，在查询中，结果集的数据占了表中数据行的比例比较大， mysql 需要扫描的行数很多，增加索引，并不能提高效率
* 定义为 text 和 image 和 bit 数据类型的列不应该增加索引，
* 当表的修改(UPDATE ， INSERT ， DELETE)操作远远大于检索(SELECT)操作时不应该创建索引，这两个操作是互斥的关系。

### 优化 MySQL

**为查询缓存优化你的查询**

> 大多数的 MySQL 服务器都开启了查询缓存。这是提高性最有效的方法之一，而且这是被 MySQL 的数据库引擎处理的。当有很多相同的查询被执行了多次的时候，这些查询结果会被放到一个缓存中，这样，后续的相同的查询就不用操作表而直接访问缓存结果了。 
>
> 这里最主要的问题是，对于程序员来说，这个事情是很容易被忽略的。因为，我们某些查询语句会让 MySQL 不使用缓存。请看下面的示例： 

``` 
// 查询缓存不开启 
$r = mysql_query("SELECT username FROM user WHERE signup_date >= CURDATE()"); 

// 开启查询缓存 
$today = date("Y-m-d"); 
$r = mysql_query("SELECT username FROM user WHERE signup_date >= '$today'"); 
```

> 上面两条 SQL 语句的差别就是 CURDATE() ， MySQL 的查询缓存对这个函数不起作用。所以，像 NOW() 和 RAND() 或是其它的诸如此类的 SQL 函数都不会开启查询缓存，因为这些函数的返回是会不定的易变的。所以，你所需要的就是用一个变量来代替 MySQL 的函数，从而开启缓存。 

**EXPLAIN 你的 SELECT 查询**

> 使用 EXPLAIN 关键字可以让你知道 MySQL 是如何处理你的 SQL 语句的。这可以帮你分析你的查询语句或是表结构的性能瓶颈。 
> 
> EXPLAIN 的查询结果还会告诉你你的索引主键被如何利用的，你的数据表是如何被搜索和排序的……等等，等等。

**当只要一行数据时使用 LIMIT 1**

> 当你查询表的有些时候，你已经知道结果只会有一条结果，但因为你可能需要去 fetch 游标，或是你也许会去检查返回的记录数。 
>
> 在这种情况下，加上 LIMIT 1 可以增加性能。这样一样， MySQL 数据库引擎会在找到一条数据后停止搜索，而不是继续往后查少下一条符合记录的数据。

**为搜索字段创建索引**

> 索引并不一定就是给主键或是唯一的字段。如果在你的表中，有某个字段你总要会经常用来做搜索，那么，请为其建立索引吧。
>
> 另外，你应该也需要知道什么样的搜索是不能使用正常的索引的。例如，当你需要在一篇大的文章中搜索一个词时，如：“ WHERE post_content LIKE ‘%apple%'”，索引可能是没有意义的。你可能需要使用 MySQL 全文索引或是自己做一个索引（比如说：搜索关键词或是 Tag 什么的） 

**在 JOIN 表的时候适当进行索引**

> 如果你的应用程序有很多 JOIN 查询，你应该确认两个表中 JOIN 的字段是被建过索引的。这样， MySQL 内部会启动为你优化 JOIN 的 SQL 语句的机制。 
>
> 而且，这些被用来 JOIN 的字段，应该是相同的类型的。例如：如果你要把 DECIMAL 字段和一个 INT 字段 JOIN 在一起， MySQL 就无法使用它们的索引。对于那些 STRING 类型，还需要有相同的字符集才行。（两个表的字符集有可能不一样） 

```
// 在 state 中查找 company 
$r = mysql_query("SELECT company_name FROM users 
LEFT JOIN companies ON (users.state = companies.state) 
WHERE users.id = $user_id"); 

// 两个 state 字段应该是被建过索引的，而且应该是相当的类型，相同的字符集。
```

**千万不要 ORDER BY RAND()**

> 想打乱返回的数据行？随机挑一个数据？真不知道谁发明了这种用法，但很多新手很喜欢这样用。但你确不了解这样做有多么可怕的性能问题。 
> 
> 如果你真的想把返回的数据行打乱了，你有 N 种方法可以达到这个目的。这样使用只让你的数据库的性能呈指数级的下降。这里的问题是： MySQL 会不得不去执行 RAND()函数（很耗 CPU 时间），而且这是为了每一行记录去记行，然后再对其排序。就算是你用了 Limit 1 也无济于事（因为要排序） 
> 下面的示例是随机挑一条记录 

```
// 千万不要这样做： 
$r = mysql_query("SELECT username FROM user ORDER BY RAND() LIMIT 1"); 

// 这要会更好： 
$r = mysql_query("SELECT count(*) FROM user"); 
$d = mysql_fetch_row($r); 
$rand = mt_rand(0, $d[0] - 1); 

$r = mysql_query("SELECT username FROM user LIMIT $rand, 1");
```

**避免 SELECT \***

> 从数据库里读出越多的数据，那么查询就会变得越慢。并且，如果你的数据库服务器和 WEB 服务器是两台独立的服务器的话，这还会增加网络传输的负载。 
> 所以，你应该养成一个需要什么就取什么的好的习惯。 

```
// 不推荐 
$r = mysql_query("SELECT * FROM user WHERE user_id = 1"); 
$d = mysql_fetch_assoc($r); 
echo "Welcome {$d['username']}"; 

// 推荐 
$r = mysql_query("SELECT username FROM user WHERE user_id = 1"); 
$d = mysql_fetch_assoc($r); 
echo "Welcome {$d['username']}";
```

**永远为每张表设置一个 ID**

> 我们应该为数据库里的每张表都设置一个 ID 做为其主键，而且最好的是一个 INT 型的（推荐使用 UNSIGNED ），并设置上自动增加的 AUTO_INCREMENT 标志。 
>
> 就算是你 users 表有一个主键叫 email 的字段，你也别让它成为主键。使用 VARCHAR 类型来当主键会使用得性能下降。另外，在你的程序中，你应该使用表的 ID 来构造你的数据结构。 
>
> 而且，在 MySQL 数据引擎下，还有一些操作需要使用主键，在这些情况下，主键的性能和设置变得非常重要，比如，集群，分区…
>
> 在这里，只有一个情况是例外，那就是 `关联表` 的 `外键`，也就是说，这个表的主键，通过若干个别的表的主键构成。我们把这个情况叫做 `外键`。比如：有一个 `学生表` 有学生的 ID ，有一个 `课程表` 有课程 ID ，那么，`成绩表` 就是 `关联表` 了，其关联了学生表和课程表，在成绩表中，学生 ID 和课程 ID 叫 `外键` 其共同组成主键。 

**使用 ENUM 而不是 VARCHAR**

> ENUM 类型是非常快和紧凑的。在实际上，其保存的是 TINYINT ，但其外表上显示为字符串。这样一来，用这个字段来做一些选项列表变得相当的完美。 
>
> 如果你有一个字段，比如 `性别`，`国家`，`民族`，`状态` 或 `部门`，你知道这些字段的取值是有限而且固定的，那么，你应该使用 ENUM 而不是 VARCHAR 。 
>
> MySQL 也有一个 `建议`（见第十条）告诉你怎么去重新组织你的表结构。当你有一个 VARCHAR 字段时，这个建议会告诉你把其改成 ENUM 类型。使用 PROCEDURE ANALYSE() 你可以得到相关的建议。 

**从 PROCEDURE ANALYSE() 取得建议**

> PROCEDURE ANALYSE() 会让 MySQL 帮你去分析你的字段和其实际的数据，并会给你一些有用的建议。只有表中有实际的数据，这些建议才会变得有用，因为要做一些大的决定是需要有数据作为基础的。 
>
> 例如，如果你创建了一个 INT 字段作为你的主键，然而并没有太多的数据，那么， PROCEDURE ANALYSE()会建议你把这个字段的类型改成 MEDIUMINT 。或是你使用了一个 VARCHAR 字段，因为数据不多，你可能会得到一个让你把它改成 ENUM 的建议。这些建议，都是可能因为数据不够多，所以决策做得就不够准。

**尽可能的使用 NOT NULL**

> 除非你有一个很特别的原因去使用 NULL 值，你应该总是让你的字段保持 NOT NULL 。这看起来好像有点争议，请往下看。 
>
> 首先，问问你自己 `EMPTY` 和 `NULL` 有多大的区别（如果是 INT ，那就是 0 和 NULL ）？如果你觉得它们之间没有什么区别，那么你就不要使用 NULL 。（你知道吗？在 Oracle 里， NULL 和 EMPTY 的字符串是一样的！) 

不要以为 NULL 不需要空间，其需要额外的空间，并且，在你进行比较的时候，你的程序会更复杂。当然，这里并不是说你就不能使用 NULL 了，现实情况是很复杂的，依然会有些情况下，你需要使用 NULL 值。 

**无缓冲的查询**

> 正常的情况下，当你在当你在你的脚本中执行一个 SQL 语句的时候，你的程序会停在那里直到没这个 SQL 语句返回，然后你的程序再往下继续执行。你可以使用无缓冲查询来改变这个行为。 
>
> 关于这个事情，在 PHP 的文档中有一个非常不错的说明： mysql_unbuffered_query() 函数： 
>
> > mysql_unbuffered_query() 发送一个 SQL 语句到 MySQL 而并不像 mysql_query()一样去自动 fethch 和缓存结果。这会相当节约很多可观的内存，尤其是那些会产生大量结果的查询语句，并且，你不需要等到所有的结果都返回，只需要第一行数据返回的时候，你就可以开始马上开始工作于查询结果了。 
>
> 然而，这会有一些限制。因为你要么把所有行都读走，或是你要在进行下一次的查询前调用 mysql_free_result() 清除结果。而且， mysql_num_rows() 或 mysql_data_seek() 将无法使用。所以，是否使用无缓冲的查询你需要仔细考虑。 

**把 IP 地址存成 UNSIGNED INT**

> 很多程序员都会创建一个 VARCHAR(15) 字段来存放字符串形式的 IP 而不是整形的 IP 。如果你用整形来存放，只需要 4 个字节，并且你可以有定长的字段。而且，这会为你带来查询上的优势，尤其是当你需要使用这样的 WHERE 条件： IP between ip1 and ip2 。 
>
> 我们必需要使用 UNSIGNED INT ，因为 IP 地址会使用整个 32 位的无符号整形。 
>
> 而你的查询，你可以使用 INET_ATON() 来把一个字符串 IP 转成一个整形，并使用 INET_NTOA() 把一个整形转成一个字符串 IP 。在 PHP 中，也有这样的函数 ip2long() 和 long2ip()。 

```
UPDATE users SET ip = INET_ATON('{$_SERVER['REMOTE_ADDR']}') WHERE user_id = $user_id;
```

**固定长度的表会更快**

> 如果表中的所有字段都是“固定长度”的，整个表会被认为是 `static` 或 `fixed-length`。例如，表中没有如下类型的字段： VARCHAR ， TEXT ， BLOB 。只要你包括了其中一个这些字段，那么这个表就不是 `固定长度静态表` 了，这样， MySQL 引擎会用另一种方法来处理。 
>
> 固定长度的表会提高性能，因为 MySQL 搜寻得会更快一些，因为这些固定的长度是很容易计算下一个数据的偏移量的，所以读取的自然也会很快。而如果字段不是定长的，那么，每一次要找下一条的话，需要程序找到主键。 
>
> 并且，固定长度的表也更容易被缓存和重建。不过，唯一的副作用是，固定长度的字段会浪费一些空间，因为定长的字段无论你用不用，他都是要分配那么多的空间。 
>
> 使用 `垂直分割` 技术（见下一条），你可以分割你的表成为两个一个是定长的，一个则是不定长的。

**垂直分割**

> `垂直分割` 是一种把数据库中的表按列变成几张表的方法，这样可以降低表的复杂度和字段的数目，从而达到优化的目的。（以前，在银行做过项目，见过一张表有 100 多个字段，很恐怖） 
>
> 示例一：在 Users 表中有一个字段是家庭地址，这个字段是可选字段，相比起，而且你在数据库操作的时候除了个人信息外，你并不需要经常读取或是改写这个字段。那么，为什么不把他放到另外一张表中呢？这样会让你的表有更好的性能，大家想想是不是，大量的时候，我对于用户表来说，只有用户 ID ，用户名，口令，用户角色等会被经常使用。小一点的表总是会有好的性能。 
>
> 示例二：你有一个叫 `last_login` 的字段，它会在每次用户登录时被更新。但是，每次更新时会导致该表的查询缓存被清空。所以，你可以把这个字段放到另一个表中，这样就不会影响你对用户 ID ，用户名，用户角色的不停地读取了，因为查询缓存会帮你增加很多性能。 
>
> 另外，你需要注意的是，这些被分出去的字段所形成的表，你不会经常性地去 JOIN 他们，不然的话，这样的性能会比不分割时还要差，而且，会是极数级的下降。 

**拆分大的 DELETE 或 INSERT 语句**

> 如果你需要在一个在线的网站上去执行一个大的 DELETE 或 INSERT 查询，你需要非常小心，要避免你的操作让你的整个网站停止相应。因为这两个操作是会锁表的，表一锁住了，别的操作都进不来了。 
>
> Apache 会有很多的子进程或线程。所以，其工作起来相当有效率，而我们的服务器也不希望有太多的子进程，线程和数据库链接，这是极大的占服务器资源的事情，尤其是内存。 
> 
> 如果你把你的表锁上一段时间，比如 30 秒钟，那么对于一个有很高访问量的站点来说，这 30 秒所积累的访问进程/线程，数据库链接，打开的文件数，可能不仅仅会让你泊 WEB 服务 Crash ，还可能会让你的整台服务器马上掛了。 
>
> 所以，如果你有一个大的处理，你定你一定把其拆分，使用 LIMIT 条件是一个好的方法。下面是一个示例：

```
while (1) { 
    
    //每次只做 1000 条 
    mysql_query("DELETE FROM logs WHERE log_date <= '2009-11-01' LIMIT 1000"); 
    
    // 没得可删了，退出！ 
    if (mysql_affected_rows() == 0) { 
        break; 
    } 
    
    // 每次都要休息一会儿 
    usleep(50000); 
}
```

**越小的列会越快**

> 对于大多数的数据库引擎来说，硬盘操作可能是最重大的瓶颈。所以，把你的数据变得紧凑会对这种情况非常有帮助，因为这减少了对硬盘的访问。 
>
> 参看 MySQL 的文档 Storage Requirements 查看所有的数据类型。 
> 
> 如果一个表只会有几列罢了（比如说字典表，配置表），那么，我们就没有理由使用 INT 来做主键，使用 MEDIUMINT, SMALLINT 或是更小的 TINYINT 会更经济一些。如果你不需要记录时间，使用 DATE 要比 DATETIME 好得多。 
> 
> 当然，你也需要留够足够的扩展空间，不然，你日后来干这个事，你会死的很难看，参看 Slashdot 的例子（ 2009 年 11 月 06 日），一个简单的 ALTER TABLE 语句花了 3 个多小时，因为里面有一千六百万条数据。

**选择正确的存储引擎**

> 在 MySQL 中有两个存储引擎 MyISAM 和 InnoDB ，每个引擎都有利有弊。酷壳以前文章《 MySQL: InnoDB 还是 MyISAM?》讨论和这个事情。 
> 
> MyISAM 适合于一些需要大量查询的应用，但其对于有大量写操作并不是很好。甚至你只是需要 update 一个字段，整个表都会被锁起来，而别的进程，就算是读进程都无法操作直到读操作完成。另外， MyISAM 对于 SELECT COUNT(*) 这类的计算是超快无比的。 
>
> InnoDB 的趋势会是一个非常复杂的存储引擎，对于一些小的应用，它会比 MyISAM 还慢。他是它支持 `行锁` ，于是在写操作比较多的时候，会更优秀。并且，他还支持更多的高级应用，

**使用一个对象关系映射器 ORM**

> 使用 ORM (Object Relational Mapper)，你能够获得可靠的性能增涨。一个 ORM 可以做的所有事情，也能被手动的编写出来。但是，这需要一个高级
