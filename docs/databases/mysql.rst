数据库
===============

mysql
----------------

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
- 使用唯一所以，比如对于性别使用索引，都会得出大约一半的行
- 使用短索引，可以节省空间，也可能会使查询更快
- 不要多度索引，不是索引越多越好，每个额外索引会占用索引空间，会降低写操作性能

BTREE索引和HASH索引
*****************

- HASH索引只用于=和<=>操作符的比较
- 优化器不能使用HASH索引加速order by操作
- HASH索引不能确定两个值之间有多少行
- HASH索引只能用整个关键字来搜索一行
- 而对于BTREE索引，当使用>,<,>=,<=,BETWEEN,!=,<>和LIKE操作符时都能使用上