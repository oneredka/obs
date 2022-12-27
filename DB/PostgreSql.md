**阅读目录**
```toc

```


### 0. 启动pgsl数据库

```shell
pg_ctl -D /xx/pgdata  start
```

### 1. 查看pgsl版本

```shell
pg_ctl --version
```

### 2. 命令行登录数据库

```shell
psql -U username -d dbname -h hostip -p port
```

### 3. 新建表

例1（主键）
```sql
create table TESTCASE(
id INTEGER, 
task_class INTEGER,
age TEXT,
PRIMARY KEY(id, task_class)
);
```

例2（自增SERIAL）
```sql
create table CREATETASK_CHKID_N(   
id SERIAL PRIMARY KEY,   
chk_id TEXT,   
n INTEGER  
);
```

`其中SERIAL代表自增，默认从1开始增加，每次自增1。`

### 4. 删除表

```sql
drop table REL_CROSS_NODE;
```

### 5. 清空表

```sql
delete from [表名]
```

or

```sql
TRUNCATE TABLE  [表名]
```

`区别：Truncate table 表名 (注:不带where语句) 速度快,而且效率高。``

因为DELETE 语句每次删除一行，并在事务日志中为所删除的每行记录一项。TRUNCATE TABLE 通过释放存储表数据所用的数据页来删除数据，并且只在事务日志中记录页的释放

### 6. 添加字段

```sql
alter table [表名] add column [字段名] [类型];
```

### 7. 更改字段

```sql
alter table [表名] rename column [旧字段名] to [新字段名];
```

#### 7.1 把表table_ex字段col_1限制非空去掉

```sql
alter table table_eg alter col_1 drop not null;
```

#### 7.2 更改字段属性，含空格

如果把字段colname把属性Text转化为int，原来text里面存在空啥的，可以
```sql
alter table tablename alter column colname type int using (trim(colname)::integer);
```

#### 7.3 更改字段由int4-->int8

```sql
alter table test_data alter column task_id type bigint using task_id::bigint
```

#### 7.4 更新默认值
```sql
alter table alf_authority alter column visible set default '1';    
```

### 8. 删除字段

```sql
alter table [表名] drop column [字段名];
```

### 9. 表中插入一行数据

```sql
insert into [表名] (字段_1, 字段_2) values (值_1, 值_2);
```

**注**：

-   如果表中字段有大写的字段，则需要对应的加上双引号。例：insert into test (no, "Name") values ('123', 'jihite');
-   值用单引号引起来('')，不能用双引号（""）

### 10. 复制表

```sql
create table test_a_copy as select * from test_a;
```

### 11. 从表A中把符合条件的记录拷贝到表B

```sql
insert into table_A select * from table_B where id  in ('a', 'b', 'c');
```

### 12. 建立索引

#### 12.1 单字段索引
```sql
create index index_name on table_name (column_1);
```

#### 12.2 多字段索引

```sql
create index index_name ON table_name (column_1, column_2);
```

### 13. 查看函数
```sql
select prosrc from pg_proc where proname=’func_name’
```
