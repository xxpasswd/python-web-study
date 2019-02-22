python 日志系统
===================

日志系统由4个部分组成

- Loggers
- Handlers
- Filters
- Formatters

Loggers
-------------

Loggers是日志系统的入口，所有的日志消息都先进入Loggers进行处理

logger可以设置日志等级，日志等级用来表示何种等级的日志消息将会被logger进行处理，每一个日志消息也有自己的等级，
python总共设有5个日志等级，DEBUG、INFO、WARNING、ERROR、CRITICAL，日志消息的严重程度依次增长，

每一个要被logger处理的日志消息，logger会对比消息的等级和自己的等级，满足和大于自己等级的消息将会被处理，
否则会忽略掉

当日志消息被logger处理后，将会传递给Handler

Handlers
----------------

handler用来对logger传过来的每条消息进行处理，决定这些消息干什么，比如输出到屏幕，写入到文件

handler也有自己的日志等级，当传过来的消息大于等于handler的等级时，就会处理，否则会忽略掉消息

一个logger可以有多个handler

Filters
----------------

Filter用来对传递的日志消息，提供额外的过滤条件

Formatters
---------------------

最终日志消息需要被处理为文本格式，formatter用来控制日志消息的格式

一个简单的例子
--------------------

.. code::

    import logging

    # 创建 一个logger，级别为DEBUG
    logger = logging.getLogger('simple_example')
    logger.setLevel(logging.DEBUG)

    # 创建 一个 handler，用于处理控制台输出，处理级别为DEBUG
    ch = logging.StreamHandler()
    ch.setLevel(logging.DEBUG)

    # 设置输出格式
    formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

    # 给ch添加输出格式
    ch.setFormatter(formatter)

    # 将ch添加到logger上
    logger.addHandler(ch)

    logger.debug('debug message')
    logger.info('info message')
    logger.warn('warn message')
    logger.error('error message')
    logger.critical('critical message')

其他
---------------

1. logging是线程安全的吗？

是线程安全的，但不是进程安全的


python sqlalchemy
==================

sqlalchemy中的三个重要对象

1. engine 引擎，它代表了数据库的核心接口

2. declare 声明，它定义类映射到数据库的表中

3. session 会话，它是orm操作数据库的处理器


python 循环导入
=================

python导入包时，已经执行的语句就不会在执行，导入和执行是不同的，执行后该模块后，
还可以从其他模块中，导入执行一次，该模块总共就执行了两次

.. code::

    **a.py**

    from b import d
    c = 'value c'
    print(d)

    **b.py**

    from a import c
    d = 'value d'
    print(c)

在a中导入b模块的属性，在b中导入a模块属性，造成两个都没有完全导入，从而找不到属性

可以使用底部导入的方式解决问题（即使用一个属性时，必须使包含属性的代码已经运行）

.. code::

    **a.py**
  
    c = 'value c'
    from b import d  # 将d导入移到属性c执行前
    print(d)

    **b.py**

    from a import c
    d = 'value d'
    print(c)

将d导入移到属性c执行前，这样在b中导入属性c时，就能够找到。

**python导入包中的模块时，首先会执行__init__.py文件里面东西**