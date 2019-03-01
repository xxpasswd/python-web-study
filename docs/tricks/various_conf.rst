dockerfile
==================

创建python开发环境的dockerfile
-------------------

.. code::

    FROM python:2.7.15
    # FROM python:3.6
    
    # 安装依赖
    COPY requirements.txt /data/requirements.txt

    # 安装apache、mod-wsgi(python2)举例
    RUN pip install -r /data/requirements.txt -i https://mirrors.aliyun.com/pypi/simple/ \
    && apt-get update && apt-get install -y apache2 libapache2-mod-wsgi \
    && ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
    # 安装nginx、uwsgi举例
    RUN pip install uwsgi -r /data/requirements.txt -i https://mirrors.aliyun.com/pypi/simple/ \
    && apt-get update && apt-get install -y nginx \
    && ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

    WORKDIR /data

**构建命令** 

    docker build . -t image-name

django项目的配置
=================

uwsgi配置
----------------

配置文件 uwsgi.ini

.. code::

    [uwsgi]
    static-map = /static=staticfiles/
    module = wsgi:application
    master = True
    pidfile = order.pid
    http = 0.0.0.0:9088
    processes = 8
    max-requests = 5000
    vacuum = True

    env = PYTHONIOENCODING=UTF-8

**启动命令**

    uwsgi uwsig.ini

apache2配置
---------------

启动脚本 run.sh

.. code::

    #!/bin/bash
    cat >> /etc/apache2/sites-available/sitename.conf <<EOF
    <VirtualHost *:80>
        Alias /static/ /data/BillingManagementSystem/BillingManagementSystem/static/

        <Directory /data/BillingManagementSystem/BillingManagementSystem/static/>
            Require all granted
        </Directory>

        WSGIScriptAlias / /data/BillingManagementSystem/BillingManagementSystem/wsgi_k8s_test.py
        <Directory /data/BillingManagementSystem/BillingManagementSystem/>
        <Files wsgi_k8s_test.py>
            Require all granted
        </Files>
        </Directory>
    </VirtualHost>
    EOF
    chmod -R 777 /data/BillingManagementSystem/logs
    cd /etc/apache2/sites-available &&
    a2ensite sitename.conf &&
    a2dissite 000-default.conf
    service apache2 start
    tail -f  /var/log/apache2/error.log

