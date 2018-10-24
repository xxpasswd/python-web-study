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