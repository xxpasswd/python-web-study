Django
==============

将view中的list和dict传递给js
----------------------

1. 在视图中需要对list和dict使用json.dumps()进行处理
2. 在网页中使用safe过滤器

view.py

.. code::

    def home(request):
    List = ['item1', 'item2']
    Dict = {'site': 'python', 'author': 'wpf'}
    return render(request, 'home.html', {
            'List': json.dumps(List),
            'Dict': json.dumps(Dict)
        })

home.html的核心代码

.. code::

    //列表
    var List = {{ List|safe }};
    //字典
    var Dict = {{ Dict|safe }};


在其他模块中使用django
-------------------

需要将django的设置导入

.. code::

    import django

    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "Project.settings")

    if django.VERSION >= (1, 7):
        django.setup()


django 数据库事物处理时，值没有存储
---------------------------

**注意：** 在整个事物里面，model的值是还没有存储的，第一次取出一个model，修改了一部分
值并保存，第二次又取出同一个model，这时候的值就成了原先model的值，存储的时候，不能全部存储
所有的字段，会把第一次修改的值覆盖掉
