jQuery学习记录
=================

基础知识：
---------------

基础语法：**$(selector).action()**

jQuery函数位于一个文档就绪事件中，防止文档未加载完成前就运行函数

.. code::

    $(document).ready(function(){
 
        // 开始写 jQuery 代码...
 
    });

    简洁写法
    $(function(){

        // 开始写 jQuery 代码...

    });

选择器

.. code::

    $(this)     选取当前html元素
    $("p")      选取所有的p元素
    $("#test")  选取id为test的元素
    $(".test")  选取class="test"的元素

选择器的更多语法，`jQuery选择器语法 <http://www.runoob.com/jquery/jquery-selectors.html>`_


jQuery 事件，监听某个组件，当发生事件时，执行代码

比如 click事件，当组件被点击时执行

.. code::

    $("#delete-whitelist").click(function() {
        $("#delete-form").submit();
    });