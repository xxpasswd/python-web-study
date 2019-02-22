python 函数传值
===================

- 如果需要传递多个非关键字参数（元组，列表的形式），可以使用*args
- 如果需要传递多个关键字参数（使用字典的形式表示），可以使用**kwargs

.. code::

    args = ['cc','dd']
    kwargs ={'aa':'cc','bb':'dd'}

    def fun(aa,bb):
        print(aa)
        print(bb)

    fun(*args)
    fun(**kwargs)


python 执行系统程序
=======================

- subprocess.run('command')
- subprocess.Popen(['command'])  后台执行，不会阻塞主程序，主程序退出不影响


django逻辑运算符的优先级
=======================

not>and>or