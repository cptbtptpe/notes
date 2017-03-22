  
## MySQL  
  
### 数据库设计  
  
* 第一范式：数据库表中所有字段都是单一属性，不可再分的。  
* 第二范式：数据库表中不存在非关键字段对任一关键字段的部分函数依赖（解决数据冗余和数据统一问题，即拆分出重复数据）。  
* 第三范式：数据表中存在非关键字段对任意候选关键字段的传递函数依赖。（对分类单独设计数据表存储）  

> 范式数据库设计思想主要是从数据库性能及空间为主进行考虑的，单适当时候应该利用反范式设计思想对数据进行部分冗余，即用空间换时间。
  
### MySql 存储引擎  
  
| 存储引擎 | 事务支持 | 锁粒度 | 优势 | 短板 |
| --- | --- | --- | --- | --- |
| MyISAM | 否 | 表级锁 | SELECT,INSERT | 频繁读写 |  
| MRG_MyISAM | 否 | 表级锁 | 水平分表 | 全表搜索 |
| InnoDB | 是 | MVCC的行级锁 | 事务处理 | 高并发 |
| Archive | 否 | 行级锁 | 日志 | 随机读写 |
| Ndb cluster | 是 | 行级锁 | 高可用性 | 应用 |
  
  
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
SELECT table_name,table_comment FROM information_schema.tables WHERE table_schema=`库名`;  
  
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
    `id` int(10) unsigned NOT NULL PRIMARY KEY AUTO_INCREMENT COMMENT '本条记录ID',  
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
ALTER TABLE `表名` ADD INDEX 索引名 (`字段名A`, `字段名B`, `字段名C`)  
  
// 查看表的创建sql语句  
SHOW CREATE TABLE `表名`;  
  
// 修改表注释  
ALTER TABLE `表名` COMMENT '注释';  
  
// 新增字段  
ALTER TABLE `表名` ADD `字段` int(10) unsigned NOT NULL AFTER `字段`;  
  
// 删除字段  
ALTER TABLE `表名` DROP `字段`;  
  
// 修改字段元数据  
ALTER TABLE `表名` MODIFY `字段` varchar(8); // 修改制定字段的元数据  
ALTER TABLE `表名` CHANGE `老字段名` `新字段名` varchar(20) NOT NULL; // 与MODIFY一致并可以修改字段名称  
  
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
mysqlbinlog --start-datetime='2013-09-10 00:00:00' --stop-datetime='2013-09-10 01:01:01' -d 库名 二进制文件

// 基于 position 值
mysqlbinlog --start-postion=107 --stop-position=1000 -d 库名 二进制文件
```

### 常用查询  
  
```  
// 查询结果默认按行格式打印  
// 查询结果按列格式打印  
SELECT * FROM `表名`\G;  
  
// 根据时间分组  
SELECT DATE_FORMAT(addtime,"%Y-%m-%d") AS days, COUNT(*) AS lively_num  
FROM device_score_lively_xyweather  
WHERE  
    channel_num = 400003  
    AND addtime  
        BETWEEN  
            '2016-06-25 00:00:00'  
        AND  
            '2016-06-28 23:59:59'  
GROUP BY days;  

// GROUP BY 后 LIMIT
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
EXPLAIN `SQL语句`

// 强制使用索引
SELECT * FROM `表名` FORCE INDEX (`索引名`) 
``` 

### MySQL5.7修改密码

```
$ sudo killall -TERM mysqld
$ mysqld_safe --skip-grant-tables & 
$ mysqld_safe --skip-grant-tables --skip-networking &
$ mysql -p
> update mysql.user set authentication_string=password('xxx') where user='root' and Host = 'localhost';
$ sudo service mysql restart
```

### MySQL远程登录

```
$ mysql -u root -pxxx
> use mysql
> update user set host = '%' where user = 'root';
> select host, user from user;
> FLUSH PRIVILEGES;

$ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
注释 bind-address 127.0.0.1
```

### msyql group 后取前N条

```
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

### 按天统计

```  
SELECT  
    DATE_FORMAT(active_time, '%Y-%m-%d') `active_date`, count(*) AS `active`  
FROM  
    active_log  
WHERE  
    active_time BETWEEN '2016-05-16 00:00:00'  
AND '2016-05-22 23:59:59'  
GROUP BY  
    `active_date`  
```  
  
### 按小时统计

```  
SELECT  
    DATE_FORMAT(addtime,'%H') AS `hour`, count(*) AS `total`  
FROM  
    `device_score_lively_xyweather`  
WHERE  
    `date` = '2016-09-07'  
GROUP BY  
    `hour`;  
```  

### ACID  

* 事务的原子性(Atomicity)

    > 是指一个事务要么全部执行,要么不执行.也就是说一个事务不可能只执行了一半就停止了.比如你从取款机取钱,这个事务可以分成两个步骤:1划卡,2出钱.不可能划了卡,而钱却没出来.这两步必须同时完成.要么就不完成.

* 事务的一致性(Consistency)

    > 是指事务的运行并不改变数据库中数据的一致性.例如,完整性约束了a+b=10,一个事务改变了a,那么b也应该随之改变.

* `独立性(Isolation)

    > 事务的独立性也有称作隔离性,是指两个以上的事务不会出现交错执行的状态.因为这样可能会导致数据不一致.

* `持久性(Durability)

    > 事务的持久性是指事务执行成功以后,该事务所对数据库所作的更改便是持久的保存在数据库之中，不会无缘无故的回滚.

### MySQL 锁    
    
**行级锁 － InnoDB**    

`特点`：开销大，加锁慢，容易出现死锁；锁粒度最小，发生冲突概率最低，并发度最高。    
注意事项：行锁说通过给索引加锁来实现的，只有通过索引条件检索的数据才能使用到行级锁，否则将使用表锁。    

`死锁`：MyISAM中是一次性获取所需的全部锁，所以不会出现死锁现象；当SQL语句操作了主键索引时，会锁定主键索引；当SQL语句操作了非主键索引时，会锁定非主键索引，然后锁定主键索引；在UPDATE、DELETE操作时，MYSQL不仅会锁定WHERE扫描过的索引，还会锁定相邻的键值（next－key locking）    
产生死锁情况：事务A锁定主键索引，在等待其他相关索引；事务B锁定非主键索引，在等待主键索引。这样就产生了死锁。    

**表级锁 － MyISAM**    

`特点`：开销小，加锁快，不会出现死锁；锁粒度最大，发送冲突概率最大，并发度最低。    

**页级锁 － BDB**    

`特点`：开销和加锁时间介于表锁和行锁之间；会出现死锁，锁粒度适中，并发度一般。    

**隔离级别**    

`脏读`：事务 A 读取了事务 B 还未提交的修改。    

`不可重复读`：两次相同的查询返回了不同的结果。    

`幻读`：两次相同的查询返回了不同的记录条数。    

**乐观锁**    

在事务中，每个读操作不会上锁，但是在执行写操作时候会判断一下在此期间是否有人修改过该数据，如果有，则取消当前更新操作。    

**悲观锁**    

在事务中，每个读操作都会上锁，别人要想更新这个数据需要等待悲观锁结束后才能执行。    

**InnoDB又分共享锁和排它锁**    

`共享锁`：又称为读锁，是读取操作创建的锁，当数据被加上共享锁后，其他session可以并发读取数据，但不能对数据进行修改，不能获取数据上的排他锁，但可以继续加共享锁，只能对数据进行读取操作，不能对数据执行写操作。    

```    
SELECT ＊ FROM table WHERE id = 1 LOCK IN SHARE MODE;    
```    
    
`排他锁`：又称为写锁，当数据被加上排他锁后，其他session不能对该数据进行任何加锁操作，也不能进行读写操作。    

```    
SELECT ＊ FROM table WHERE id = 1 FOR UPDATE;    
```

**FOR UPDATE**    

`特点`：仅仅适用于 InnoDB，并且需要出现在 `BEGIN` 和 `COMMIT` 块中（事务）    

| 上下文 | 锁状态 | 锁描述 |    
| --- | --- | --- |    
| 明确指定主键并存在该记录 | row lock | 行锁 |    
| 明确制定主键但不存在该记录 | no lock | 无锁 |    
| 无主键 | table lock | 表锁 |    
| 主键不明确 | table lock | 表锁 |    
     
表级锁时，不管是否查询到记录，都会锁定表    
