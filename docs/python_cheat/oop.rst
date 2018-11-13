python 面向对象编程
===================

模块导入
---------------------

当需要导入一个全局的类时，其他模块导入的这个类时时候，便会执行

.. code::
    database.py

    class DB:
        pass
    
    db = DB()

    process.py

    from database import db

如上面的代码，在process文件里导入db的时候，db就会执行实例化，有时候，我们需要db在所有的程序都准备好后，在实例化

我们可以通过写一个初始化方法，需要实例化时，在执行初始化方法

.. code::
    database.py

    class DB:
        pass
    
    db = None

    def init_process():
        global db
        db = DB()

    process.py

    from database import db, init_process

    # 需要执行的时候
    init_process()
