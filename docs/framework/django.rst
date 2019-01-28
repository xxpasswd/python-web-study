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

使用django的事物处理，在一个事物内，将一个查询集的值修改并保存了，而后，又重新将这个查询集获取了一遍，
再保存了一遍，当事物结束时，这时候的值时后面查询时获取的值，而不是修改后的值。
