数据库
===============

mysql
----------------

数据库操作
+++++++++++++++++

- 连接数据库

.. code::

    mysql -u root -p

- 显示所有的数据库

.. code::

    show databases;

- 使用数据库

.. code::

    use dbname;

- 创建数据库

.. code::

    create database dbname;

- 删除数据库

.. code::

    drop database dbname


数据库表增删改查
+++++++++++

- 查询 **select**

.. code::

    select * from table_name;
    select * from table_name where id='12';
    select * from table_name order by create_time desc;
    select count(*) from table_name;
    select * from table_name group by type;
    select * from table_name where id in (select id from table_name2);
    select * from table_name as t1 left join table_name2 as t2 where t1.id=t2.id;
    select * from table_name t1, table_name2 t2 where t1.id=t2.id

- 新增 **insert**

.. code::

    insert into table_name (id,name,age) values (1,'aa',34);
    insert into table_name values(2,'bb',32);

- 删除 **delete**

.. code::

    delete from table_name where id='2';

- 更改 **update**

.. code::

    update table_name set name='bobby' where id='1';

数据库表操作
++++++++++++++++

- 查看数据库中的表

.. code::

    show tables;

- 查看表中的列

.. code::

    show columns from table_name;
    desc table_name;

- 新建一张表

.. code::

    create table test_table (
        name varchar(30),
        age interger;
        );
        

- 删除一张表

.. code::

    drop table test_table;

- 更改表的某个字段

.. code::

    alter test_table add column address varchar(30) default NULL;
    alter test_table delet column address;
    alter test_table modify column address varchar(100);


索引
++++++++++++++++

删除和创建
***************

.. code::

    创建索引
    CREATE [ONLINE|OFFLINE] [UNIQUE|FULLTEXT|SPATIAL] INDEX index_name
        [index_type]
        ON tbl_name (index_col_name,...)
        [index_option] ...

    index_col_name:
        col_name [(length)] [ASC | DESC]

    删除索引
    DROP INDEX index_name ON tbl_name

设计索引的原则
*****************

- 最适合的索引列应该是where语句后面的列
- 使用唯一索引，比如对于性别使用索引，都会得出大约一半的行
- 使用短索引，可以节省空间，也可能会使查询更快
- 不要多度索引，不是索引越多越好，每个额外索引会占用索引空间，会降低写操作性能

BTREE索引和HASH索引
*****************

- HASH索引只用于=和<=>操作符的比较
- 优化器不能使用HASH索引加速order by操作
- HASH索引不能确定两个值之间有多少行
- HASH索引只能用整个关键字来搜索一行
- 而对于BTREE索引，当使用>,<,>=,<=,BETWEEN,!=,<>和LIKE操作符时都能使用上


mysql 问题解决
+++++++++++++++

1. 出现锁等待

select * from information_schema.innodb_trx