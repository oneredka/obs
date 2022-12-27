**阅读目录**
```toc

```


### 0. 启动pgsl数据库

pg_ctl -D /xx/pgdata  start

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 1. 查看pgsl版本

pg_ctl --version

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 1. 命令行登录数据库

1

`psql -U username -d dbname -h hostip -p port`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 2. 列出所有数据库

\l 

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 3. 切换数据库

1

`\c dbname`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 4. 列出当前数据库的所有表

\d 

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 5. 查看指定表的所有字段

1

`\d  tablename`

![](https://images0.cnblogs.com/blog2015/408927/201507/221518020218081.png)

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 6. 查看指定表的基本情况

1

`\d+  tablename`

![](https://images0.cnblogs.com/blog2015/408927/201507/221518172717955.png)

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 7. 退出操作

1

`q`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 8. 新建表

例1（主键）

![复制代码](https://common.cnblogs.com/images/copycode.gif)

create table TESTCASE(
id INTEGER, 
task_class INTEGER,
age TEXT,
PRIMARY KEY(id, task_class)
);

![复制代码](https://common.cnblogs.com/images/copycode.gif)

例2（自增SERIAL）

create table CREATETASK_CHKID_N(   
id SERIAL PRIMARY KEY,   
chk_id TEXT,   
n INTEGER  
);

其中SERIAL代表自增，默认从1开始增加，每次自增1。

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 9. 删除表

1

`drop table REL_CROSS_NODE;`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 10. 清空表

delete from [表名]

or

TRUNCATE TABLE  [表名]

区别：Truncate table 表名 (注:不带where语句) 速度快,而且效率高。

因为DELETE 语句每次删除一行，并在事务日志中为所删除的每行记录一项。TRUNCATE TABLE 通过释放存储表数据所用的数据页来删除数据，并且只在事务日志中记录页的释放

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 11. 添加字段

1

`alter table [表名] add column [字段名] [类型];`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 12. 更改字段

alter table [表名] rename column [旧字段名] to [新字段名];

例：把表table_ex字段col_1限制非空去掉：ALTER TABLE table_eg ALTER col_1 drop not NULL

**12.1 更改字段属性，含空格**

如果把字段colname把属性Text转化为int，原来text里面存在空啥的，可以

ALTER TABLE tablename ALTER COLUMN colname TYPE int USING (trim(colname)::integer);

**12.2 更改字段由int4-->int8**

alter table test_data alter column **task_id** type bigint using **task_id**::bigint

**12.3 更新默认值**

alter table alf_authority alter column   visible               set default '1';    

[参考](https://blog.csdn.net/guoruijun_2012_4/article/details/100751374)

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 13. 删除字段

1

`alter table [表名] drop column [字段名];`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 14. 表中插入一行数据

1

`insert into [表名] (字段``1``,字段``2``) values (值``1``,值``2``);`

例如：    

1

`insert into assist_info (``id``, maat_id, block_type) values (``'F006'``,` `'F7775'``, 1)`  

**注**：

-   如果表中字段有大写的字段，则需要对应的加上双引号。例：insert into test (no, "Name") values ('123', 'jihite');
-   值用单引号引起来('')，不能用双引号（""）

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 15. 表中删除一行数据

1

`delete from [表名] where [该行特征];`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 16. 修改表中数据

1

`update [表名] set [目标字段名]=[目标值] where [该行特征]`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 17. 删除表

1

`drop table [表名];`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 18. 退出postgreSql

\q

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 19. 两个查询结果做差 except

1

2

3

4

5

`(select node_id from node where node_id=``1` `or node_id=``2``) except (select node_id from node where node_id=``1``);`

 `node_id`

`---------`

       `2`

`(``1` `row)`

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 20. 复制表

CREATE TABLE test_a_copy AS SELECT * FROM test_a;

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 21.命令导入sql数据文件

psql -h localhost  -d databaseName  -U username -f  filename

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 22. 查询结果存储到输出文件

格式：

\o file_path

这样就会把查询结果存储到输出文件中。例

postgres=> \o /home/jihite/data/iu_data;
postgres=> select test_id from cdb_all_iu_data limit 10;
postgres=> select test_id from cdb_all_iu_data limit 5;

结果

![复制代码](https://common.cnblogs.com/images/copycode.gif)

test_id
--------------
         2143
         2153
         2144
         2156
         2145
         2154
         2146
         2157
         2147
         2155
(10 rows)

test_id
--------------
         2143
         2153
         2144
         2156
         2145
(5 rows)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 23. 数据库的备份&恢复

导出到线下文件

pg_dump --host hostname --port port --username username -t tablename -d dbname >/home/jihite/table.sql 

把线下文件导入到数据库

psql -h 10.125.7.68 -p 5432 -d postgres -U postgres -W postgres -f 2.sql

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 24. \x

![复制代码](https://common.cnblogs.com/images/copycode.gif)

postgres=> \x
Expanded display is on.
postgres=> select *  from cdb_chk_items where chk_id = 'R000000335';
-[ RECORD 1 ]+------------------------------------------------------------------------------------------------
chk_id       | R000000335
chk_desc     | 道路属性与道路属性相关检查
chk_info     | {"FIELDS": {"TRAFFIC_SIGN": ["TYPE", "GEOM"], "ROAD_LINK": ["ROAD_CLASS", "FORM_WAY", "GEOM"]}}
err_desc     | {"ERR2": "roadclass取值错误", "ERR1": "formway取值错误"}
chk_level    | 1
is_opened    | 1
module_name  | TRAFFIC_SIGN
invalid_flag | 1
rel_mode     | MAIN_LAYER:TRAFFIC_SIGN
             :         TRAFFIC_SIGN|A,M|DIRECT
             :         ROAD_LINK|A,M,D|ATTR_REL

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 25. 从表A中把符合条件的记录拷贝到表B

insert into A select * from B where id  in ('a', 'b', 'c');

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 26 建立索引

单字段索引

CREATE INDEX index_name ON table_name (field1);

多字段索引

CREATE INDEX index_name ON table_name (field1,field2);

查看所有表的索引使用情况

![复制代码](https://common.cnblogs.com/images/copycode.gif)

select 
    relname, indexrelname, idx_scan, idx_tup_read, idx_tup_fetch 
from 
    pg_stat_user_indexes 
order by 
    idx_scan asc, idx_tup_read asc, idx_tup_fetch asc;

![复制代码](https://common.cnblogs.com/images/copycode.gif)

查看某个表索引的使用情况

![复制代码](https://common.cnblogs.com/images/copycode.gif)

select 
    relname, indexrelname, idx_scan, idx_tup_read, idx_tup_fetch 
from 
    pg_stat_user_indexes 
where
    relname = table_name 
order by 
    idx_scan asc, idx_tup_read asc, idx_tup_fetch asc;

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 27. 超找数据库的连接信息

select * from pg_stat_activity

包含：客户端user、ip、执行语句，状态、时间

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 28. 查看函数

在postgresql数据库中想查询自定义函数代码则可以在客户端使用\sf func_name,

也可以使用sql语句：select prosrc from pg_proc where proname=’func_name’

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 29. 通过文件导入

psql **** -f ind_statis3.sql

[回到顶部](https://www.cnblogs.com/kaituorensheng/p/4667160.html#_labelTop)

### 30.修改自增ID

 Select nextval('id_seq');
CREATE SEQUENCE topo_id_seq START 2000;
ALTER TABLE "R_LANEINFO_TOPO" ALTER COLUMN "ID" SET DEFAULT nextval('topo_id_seq'::regclass);

duplicate key value violates unique constraint 解决方案