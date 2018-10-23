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

