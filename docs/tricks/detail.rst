ssh 技巧
------------

ssh 客户端配置文件
=======================

当主机较多时，不方便记住所有的IP，密码，端口，我们可以使用ssh客户端配置文件来记录这些服务器

.. code::

    Host 主机别名
    HostName 主机地址
    User 登陆用户名
    Port 端口号
    IdentityFile 私钥路径

在 ~/.ssh/目录下创建一个config文件，在config写入相应的配置后，就可以使用 ssh <主机别名>访问服务器了


supervisor 管理后台进程（后台进程挂了，能够自动启动）
--------------------

supervisor安装：
======================

.. code::

    pip install supervisor

配置文件：
==================

先用命令生成默认配置文件

.. code::

    echo_supervisord_conf > /etc/supervisord.conf

在配置文件中，添加自己的配置

.. code::

    [program:program_name]
    command=python file.py
    autorestart=true
    user=root
    stdout_logfile=/a/path
    stderr_logfile=/a/path

启动supervisor
===============

.. code::

    supervisord -c /etc/supervisord_conf


windows Host配置
-----------------

文件位置：C:\Windows\System32\drivers\etc

刷新host：ipconfig /flushdns