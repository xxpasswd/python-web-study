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
    