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


类变量
----------------

定义在python类里面，供所有类使用的变量为类变量

.. code::
    class MyClass:
        a = [] # a为一个类变量

上面的a为一个类变量，所有通过此类实例化的对象，都共享此变量

.. code::
    first = MyClass()
    second = MyClass()
    first.a.append(1)
    second.a.append(2)

经过上面的操作后，a的值为[1,2]

这个类变量在子类里面，可以通过self.a 的形式访问

但如果，在子类里面对self.a 进行赋值，则会在子类里面创建一个新的实例变量，通过self.a 访问到的则是在子类里面创建的实例变量

若要访问类变量，可以使用MyClass.a来访问
