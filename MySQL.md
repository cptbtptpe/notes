  
## MySQL  
  
### 连接mysql  
  
```mysql  
mysql -u root -p root  
```  
  
### 库相关  
  
```mysql  
// 列出所有数据库  
SHOW DATABASES;  
  
// 新建数据库  
CREATE DATABASE `库名`;  
  
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
  
```mysql  
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
  
```mysql  
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
